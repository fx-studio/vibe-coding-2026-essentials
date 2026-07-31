# Chương 7: Web hoạt động thế nào

Bạn nhờ AI thêm tính năng "chỉ người đăng nhập mới xem được danh sách bug". Nó làm xong, bản preview chạy được. Nhưng khi bạn mở lại app sáng hôm sau, màn hình trống trơn và console in ra một dòng đỏ: `401 từ API`. Bạn dán nguyên câu đó cho AI. Nó xin lỗi, sửa vài dòng, và lỗi vẫn còn.

Câu hỏi thật sự lúc này không phải "sửa thế nào", mà là "lỗi này của ai?". Của bạn — vì bạn chưa đăng nhập? Của AI — vì code nó viết sai? Hay của dịch vụ bên thứ ba mà app đang gọi — vì bên đó đang trục trặc? Ba khả năng này cần ba cách xử lý hoàn toàn khác nhau, và nếu không phân biệt được, bạn sẽ ngồi thử mò cho tới khi may mắn.

Cái số `401` đó không phải mật mã. Nó là một câu nói rất rõ ràng, chỉ là bằng ngôn ngữ của web. Đọc hết chương này, bạn sẽ nhìn vào `401` và biết ngay chuyện gì đang xảy ra, nên hỏi AI điều gì, và lỗi thuộc về phía nào. Để tới đó, ta cần một tấm bản đồ về cách web vận hành — và cách dễ nhất để dựng bản đồ đó là bước vào một nhà hàng.

## Nhà hàng: bản đồ của cả cái web

Hãy tưởng tượng một nhà hàng. Có bốn nhân vật. **Khách** ngồi ở bàn, xem thực đơn và gọi món. **Bồi bàn kiêm đầu bếp** nhận order, vào bếp nấu. **Kho nguyên liệu** phía sau chứa mọi thứ để nấu. Và **thực đơn** — cuốn sổ liệt kê nhà hàng phục vụ được những gì và gọi ra sao.

Web hoạt động y hệt bốn nhân vật này, chỉ đổi tên:

- **Browser** (trình duyệt — Chrome, Safari, Firefox) là *khách*. Đây là phần chạy trên máy hoặc điện thoại của người dùng — thứ họ nhìn thấy và bấm vào. Dân trong nghề gọi nó là **frontend**.
- **Server** (máy chủ) là *bồi bàn kiêm đầu bếp*. Nó nhận yêu cầu, xử lý mọi logic quan trọng: kiểm tra mật khẩu, tính toán số liệu, quyết định ai được xem gì. Phần này gọi là **backend**.
- **Database** (cơ sở dữ liệu) là *kho nguyên liệu*. Nơi lưu trữ dữ liệu có cấu trúc.
- **API** là *thực đơn* — bộ quy tắc cho biết được phép gọi gì và gọi thế nào. Ta sẽ mở kỹ thực đơn này ở nửa sau chương.

![HÌNH 7.1](../figures/images/hinh-7-1.png)

*HÌNH 7.1: Sơ đồ nhà hàng — Khách (Browser/Frontend) gửi order tới Bồi bàn (Server/Backend), Bồi bàn lấy nguyên liệu từ Kho (Database), nấu xong mang món (Response) ra cho Khách. Mỗi vai được dán cả nhãn đời thường lẫn thuật ngữ kỹ thuật.*

Điểm mấu chốt đầu tiên: **frontend chạy trên thiết bị của người dùng, backend chạy trên server ở xa**. Khi 100 người mở cùng một app, có 100 bản frontend chạy trên 100 máy khác nhau, nhưng thường chỉ có một backend ngồi một chỗ phục vụ tất cả. Hệ quả rất thực tế: nếu frontend nặng (quá nhiều ảnh lớn, quá nhiều code), người dùng phải chờ — và như mọi Tester đều biết, người dùng không thích chờ. Còn nếu logic quan trọng đặt sai chỗ, ta sẽ gặp đúng loại lỗi bảo mật mà chương này sắp cảnh báo.

Điểm mấu chốt thứ hai: mọi thứ diễn ra theo một chu trình lặp đi lặp lại. Khách gọi món, bếp nấu, món ra. Trên web gọi là **request** (yêu cầu) đi và **response** (phản hồi) về. Bạn click một link — request đi, response về. Submit một form — request đi, response về. Cuộn trang để tải thêm — request đi, response về. Cả internet chạy trên nguyên tắc đơn giản này.

Về phần kho nguyên liệu: cứ hình dung database như một file Excel cực mạnh. Mỗi **table** (bảng) là một sheet, mỗi **row** (dòng) là một bản ghi, mỗi **column** (cột) là một trường. Một app quản lý bug có bảng `bugs` với các cột `title`, `severity`, `status`, `assigned_to` — trông hệt cái bảng bug bạn vẫn quản lý trên Jira hay Excel. Tư duy về dữ liệu mà bạn đã có sẵn chính là lợi thế lớn nhất khi làm việc với AI.

> 🧪 **Dành cho Tester/QA:** Nếu bạn từng dùng một công cụ test API và bấm "Send", bạn đã tự tay chạy đúng chu trình request-response này rồi — chỉ khác là làm thủ công thay vì để browser tự làm. Mọi thứ trong chương này chỉ đang gọi tên những gì bạn đã thấy trên màn hình công cụ đó.

## HTTP: ngôn ngữ khách và bếp nói với nhau

Browser và server trò chuyện bằng một bộ quy tắc tên là **HTTP** (*HyperText Transfer Protocol* — giao thức truyền siêu văn bản). Nghe hàn lâm, nhưng bản chất chỉ là quy ước để gửi và nhận dữ liệu. Mỗi request mang theo một **method** (phương thức) nói rõ khách muốn làm gì:

- **GET** — "Cho tôi xem cái này." Mở một trang là browser gửi GET. Giống hỏi bồi bàn: "Cho xem thực đơn."
- **POST** — "Tôi gửi thông tin này cho bạn." Điền form rồi Submit là POST. Giống đưa order cho bồi bàn.
- **PUT** — "Cập nhật cái này." Sửa profile là PUT. Giống bảo bồi bàn đổi món chính từ gà sang cá.
- **DELETE** — "Xóa cái này." Xóa một bài viết là DELETE. Giống hủy một món đã gọi.

Xử lý xong, server gửi response kèm một **status code** (mã trạng thái) — con số ba chữ số cho biết kết quả. Ta sẽ đọc kỹ các con số này ở phần sau, vì đó chính là chìa khóa của lỗi `401` đầu chương.

```http
GET /api/bugs?status=open HTTP/1.1
Host: myapp.example.app

--- Response ---
HTTP/1.1 200 OK
Content-Type: application/json

[
  {"id": 1, "title": "Login button không hoạt động", "severity": "High"},
  {"id": 2, "title": "Hình ảnh bị vỡ trên mobile", "severity": "Medium"}
]
```

Đoạn trên là một request GET xin danh sách bug đang mở. Server trả về status `200` (thành công) cùng dữ liệu dạng JSON — định dạng bạn sẽ gặp liên tục và sẽ mổ kỹ ở cuối chương.

## URL: địa chỉ của mọi thứ trên web

Mỗi ngày bạn gõ URL vào thanh địa chỉ, nhưng đã bao giờ mổ nó ra xem gồm những gì chưa?

```
https://myapp.example.app:443/dashboard?team=qa&status=open
```

- **`https://`** là giao thức. "Https" là phiên bản có mã hóa của HTTP — dữ liệu được mã hóa khi truyền. Hầu hết web hiện đại đều dùng https.
- **`myapp.example.app`** là tên miền (**domain**) — "địa chỉ nhà" của app trên internet.
- **`:443`** là cổng (**port**), như số phòng trong một tòa nhà. 443 là cổng mặc định của https nên thường bị ẩn đi.
- **`/dashboard`** là đường dẫn (**path**) — trang cụ thể bạn muốn xem.
- **`?team=qa&status=open`** là tham số truy vấn (**query parameters**) — thông tin bổ sung, kiểu "cho tôi xem dashboard, nhưng chỉ team QA và chỉ item đang open".

![HÌNH 7.2](../figures/images/hinh-7-2.png)

*HÌNH 7.2: Mổ xẻ một URL — mỗi phần (protocol, domain, port, path, query) được tô một màu khác nhau kèm chú thích vai trò.*

Có một điều hay: ở nhiều framework web hiện đại, cấu trúc URL gần như tương ứng một-một với cấu trúc thư mục của dự án — tạo folder `dashboard`, bỏ đúng file trang vào đó là bạn có ngay đường dẫn `/dashboard`. Cơ chế này gọi là **file-based routing** (định tuyến dựa trên file), và ta sẽ xem cấu trúc thư mục thật ở Chương 10.

Cũng ở Chương 10, ta sẽ nói kỹ hơn một chuyện chỉ cần biết sơ lúc này: có trang được server "nấu sẵn" HTML rồi mới gửi cho browser (gọi là **server-side rendering**), có trang server chỉ gửi một khung gọn cùng code để browser tự "nấu" giao diện tại chỗ (gọi là **client-side rendering**). Sự khác biệt này giải thích vì sao cùng một app mà có trang tải nhanh, có trang tải chậm lần đầu rồi sau đó mượt hẳn. Với chương này, chỉ cần nhớ hai kiểu đó tồn tại là đủ.

## API: mở cuốn thực đơn ra đọc

Giờ quay lại thứ ta đã treo ở đầu: cuốn **thực đơn**. Khi vào nhà hàng, bạn không chạy thẳng vào bếp tự nấu, cũng không hét "cho tôi cái gì đó ngon ngon". Bạn nhận thực đơn — nó liệt kê rõ nhà hàng làm được món gì và gọi ra sao — rồi chọn từ đó.

**API** (*Application Programming Interface*) chính là cuốn thực đơn ấy. Nó là một bản "hợp đồng" giữa phía gọi (frontend) và phía phục vụ (backend): "Đây là những gì tôi làm được cho bạn. Gửi yêu cầu đúng format này, tôi trả kết quả theo format kia." Khi AI dựng app cho bạn, nó không chỉ vẽ giao diện — nó còn tạo ra các API để giao diện đó nói chuyện được với server và database. Mỗi khi bạn thấy trong code có chữ `fetch` hay `api`, đó là lúc app đang gọi thực đơn.

Kiểu API phổ biến nhất hiện nay là **REST** (*Representational State Transfer*). Ý tưởng cốt lõi rất đơn giản: mọi "thứ" trong app (users, bugs, projects) có một địa chỉ URL riêng, gọi là **endpoint** (điểm cuối), và bạn tác động lên nó bằng các method HTTP. Ví dụ với app quản lý bug:

```
/api/bugs          -- danh sách tất cả bug
/api/bugs/42       -- chi tiết bug số 42
/api/users         -- danh sách tất cả user
/api/users/7       -- thông tin user số 7
```

Để ý quy tắc: số nhiều cho danh sách (`bugs`, `users`), thêm ID để chỉ một cái cụ thể (`bugs/42`). Đây là quy ước chung của REST, và AI tuân theo nó khi sinh code — nên khi bạn nhìn một loạt endpoint, bạn đoán được ngay cái nào làm gì.

> 📋 **Dành cho PM/BA:** Khi bạn viết requirement cho một tính năng, thực chất bạn đang mô tả một API. "Người dùng xem được danh sách bug theo severity" nghĩa là cần một endpoint nhận tham số `severity` và trả về danh sách bug tương ứng. Nghĩ theo hướng này, spec của bạn sẽ khớp gần như một-một với thứ AI cần sinh ra — và bạn sẽ phát hiện sớm những chỗ mình quên chưa mô tả.

## Bốn method, một vòng đời: CRUD

Bốn method GET, POST, PUT, DELETE ở phần trước, khi đặt vào bối cảnh API, ghép thành một vòng đời hoàn chỉnh mà dân trong nghề gọi là **CRUD** (*Create, Read, Update, Delete* — Tạo, Đọc, Cập nhật, Xóa). Đây là bốn thao tác mà gần như mọi app đều cần. Lấy đúng app quản lý bug mà Tester nào cũng quen:

```
CRUD          Method     Endpoint          Giống như trên Jira
----------    -------    --------------    -----------------------------
Create        POST       /api/bugs         Bấm "New Bug", điền form báo lỗi
Read          GET        /api/bugs         Mở trang danh sách, thấy mọi bug
Read          GET        /api/bugs/42      Mở chi tiết bug #42
Update        PUT        /api/bugs/42      Đổi status Open → In Progress
Delete        DELETE     /api/bugs/42      Xóa một bug bị trùng
```

Bảng này là một trong những thứ đáng nhớ nhất chương. Mỗi lần thấy AI tạo một tính năng, tự hỏi "cái này thuộc CRUD nào?" là bạn hiểu ngay nó đang làm gì.

> 🧪 **Dành cho Tester/QA:** Test API thực chất là test đúng bốn thao tác CRUD này. Tạo mới có thành công không? Đọc có trả về đủ và đúng dữ liệu không? Cập nhật có lưu lại thật không? Xóa có xóa thật không? Đây chính là bộ khung test case bạn đã dùng cho ứng dụng, giờ áp thẳng vào từng endpoint.

## Status code: nhà hàng trả lời bạn thế nào

Đây là phần trả lời cho lỗi `401` đầu chương. Sau khi xử lý xong, server luôn kèm một status code vào response. Con số ba chữ số này chính là câu bếp nói với khách về kết quả. Những mã bạn sẽ gặp thường xuyên nhất:

- **200 OK** — thành công. Món đã ra.
- **201 Created** — tạo mới thành công. Bạn thấy mã này khi POST xong một bản ghi.
- **301 Moved** — chuyển hướng. "Nhà hàng đổi địa chỉ, mời qua chỗ mới."
- **400 Bad Request** — "Tôi không hiểu order của bạn." Dữ liệu gửi lên sai format hoặc thiếu trường bắt buộc, ví dụ tạo bug mà không có title.
- **401 Unauthorized** — "Bạn chưa xuất trình thẻ VIP." Bạn chưa đăng nhập, hoặc token đã hết hạn. API từ chối phục vụ vì **không biết bạn là ai**.
- **403 Forbidden** — "Bạn có thẻ VIP, nhưng khu này không cho bạn vào." Bạn đã đăng nhập nhưng **không có quyền** cho thao tác này — ví dụ Tester không được xóa cả project.
- **404 Not Found** — "Món này không có trong thực đơn." Endpoint không tồn tại, hoặc bản ghi không tìm thấy.
- **422 Unprocessable Entity** — "Tôi hiểu order, nhưng không nấu được." Dữ liệu đúng format nhưng không hợp lệ, ví dụ `severity` là "Super Duper Critical" thay vì High/Medium/Low.
- **500 Internal Server Error** — "Bếp bị cháy." Lỗi ở phía server, không phải lỗi của bạn.

Đừng cố học thuộc từng số. Mẹo nằm ở **chữ số đầu tiên**: `2xx` là tin vui, `3xx` là chuyển hướng, `4xx` là lỗi phía client (bên gọi gửi sai gì đó), `5xx` là lỗi phía server (bên phục vụ có vấn đề). Chỉ cần nhớ "2 là tốt, 4 là lỗi của mình, 5 là lỗi của server" là đủ dùng trong phần lớn tình huống.

Giờ áp vào lỗi đầu chương. `401` bắt đầu bằng số `4` — nghĩa là request gửi lên thiếu hoặc sai thứ gì đó, **không phải** dịch vụ bên thứ ba bị sập (cái đó sẽ là `5xx`). Cụ thể `401` nói: "Tôi không biết bạn là ai." Vậy nguyên nhân gần như chắc chắn là app chưa gửi kèm thông tin đăng nhập, hoặc thông tin đó đã hết hạn qua đêm — đúng như tình huống "sáng hôm sau mở lại thì trắng màn hình". Ta sẽ chốt nốt mảnh ghép cuối cùng ở phần headers ngay dưới đây.

> 🧪 **Dành cho Tester/QA:** Mỗi status code là một test case đợi bạn viết. Một app tốt không chỉ chạy khi mọi thứ suôn sẻ (`200`, `201`) — nó phải xử lý cả đường lỗi: gặp `401` thì hiện "Vui lòng đăng nhập lại", gặp `403` thì "Bạn không có quyền", gặp `500` thì "Có lỗi xảy ra, thử lại sau". Khi soát code AI sinh ra, hãy hỏi thẳng: "Đã xử lý các trường hợp 400, 401, 403, 404 và 500 chưa?" Nếu AI chỉ viết cho đường thành công, đó chính là danh sách bug bạn sắp báo.

## Headers: thông tin gửi kèm mà bạn không thấy

Khi gọi món, ngoài tên món bạn còn cung cấp vài thông tin ngầm: ngồi bàn số mấy, có dị ứng gì, thanh toán bằng gì. Tương tự, mỗi request và response đều có phần **headers** — thông tin đi kèm nằm ngoài nội dung chính. Hai header đáng nhớ nhất:

**Content-Type** cho biết định dạng dữ liệu. Giá trị hay gặp nhất là `application/json`, nghĩa là dữ liệu gửi/nhận theo format JSON. **Authorization** chứa thông tin xác thực, thường ở dạng `Bearer <token>` — một chuỗi ký tự dài mà server dùng để xác nhận bạn là ai và có quyền gì. Đây chính là "thẻ VIP" ở phần status code. Sau khi đăng nhập, mỗi lần app gọi API, header này lẽ ra phải tự động được đính kèm.

```http
POST /api/bugs HTTP/1.1
Host: myapp.example.app
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6...

{
  "title": "Login button không phản hồi",
  "severity": "high",
  "assigned_to": "minh@team.com"
}
```

Và đây là mảnh ghép cuối cho lỗi `401`: nếu header `Authorization` này **không được gửi**, hoặc token trong đó đã hết hạn, server không nhận ra bạn và trả về `401`. Rất thường gặp là AI viết đúng phần giao diện nhưng quên đính token vào request, hoặc quên xử lý tình huống token hết hạn qua đêm. Giờ bạn biết cách hỏi lại cho trúng: "Request này đã gửi kèm header Authorization chưa? Khi token hết hạn thì app xử lý thế nào?" — thay vì chỉ dán mỗi chữ `401` và hy vọng.

> ⚠️ **Lưu ý:** Đừng lẫn `401` với `403` — hai mã này nghe giống nhau nhưng dẫn tới hai hướng sửa khác hẳn. `401` là "chưa biết bạn là ai" → vấn đề nằm ở đăng nhập/token. `403` là "biết bạn rồi, nhưng bạn không được phép" → vấn đề nằm ở phân quyền. Sửa `403` bằng cách nhét thêm token là vô ích, và ngược lại. Khi báo bug hay nhờ AI, ghi rõ mã nào để không đi sai đường ngay từ đầu.

## JSON: ngôn ngữ chung của dữ liệu

Cuối cùng, hãy nói về "món ăn" mà nhà hàng bưng ra — tức dữ liệu API trả về. Trên web hiện đại, dữ liệu gần như luôn ở dạng **JSON**. Nó giống một tờ phiếu giao hàng mà cả người lẫn máy đều đọc được, với vài quy tắc đơn giản.

**Object** dùng dấu ngoặc nhọn `{}`, chứa các cặp "khóa: giá trị":

```json
{
  "title": "Login button không phản hồi",
  "severity": "high",
  "status": "open"
}
```

Mỗi *key* (khóa) là tên trường, luôn nằm trong nháy kép; mỗi *value* (giá trị) là nội dung, có thể là chuỗi, số, true/false, null, array, hoặc một object khác. **Array** dùng ngoặc vuông `[]`, chứa một danh sách có thứ tự:

```json
{
  "team": "QA",
  "members": ["Minh", "Lan", "Duc", "Hoa"]
}
```

Phần hay nhất — và hơi rối nhất — là **lồng nhau** (nested): object chứa object, array chứa nhiều object:

```json
{
  "project": "Bug Tracker",
  "bugs": [
    {
      "id": 1,
      "title": "Login button không phản hồi",
      "severity": "high",
      "assigned_to": { "name": "Minh", "role": "tester" }
    },
    {
      "id": 2,
      "title": "Hình ảnh bị vỡ trên mobile",
      "severity": "medium",
      "assigned_to": { "name": "Lan", "role": "developer" }
    }
  ]
}
```

Đoạn trên mô tả một project có hai bug. Mỗi bug là một object trong array `bugs`, và mỗi bug lại chứa một object `assigned_to`. Cách đọc JSON lồng nhau mà không bị lạc: bắt đầu từ ngoặc ngoài cùng, xác định các key ở tầng đầu (`project`, `bugs`), rồi đi sâu vào từng key — giống mở một hộp quà lớn, thấy nhiều hộp nhỏ, mở từng hộp nhỏ ra xem.

![HÌNH 7.3](../figures/images/hinh-7-3.png)

*HÌNH 7.3: Đọc JSON lồng nhau — từ object gốc, một mũi tên chỉ vào bugs (array), rồi vào phần tử `[0]` (object đầu), rồi vào title (giá trị "Login button không phản hồi"). Mỗi bước có chú thích.*

JSON không chỉ nằm trong response API. Nó ở khắp dự án của bạn: file mô tả dự án và danh sách thư viện, các file cấu hình — phần lớn đều là JSON hoặc cấu trúc rất giống. Và đây là đoạn code bạn sẽ gặp đi gặp lại khi AI xử lý dữ liệu:

```typescript
// Lấy danh sách bug từ API rồi đọc dữ liệu
const response = await fetch('/api/bugs?status=open')
const data = await response.json()

// data giờ là một object JSON
// data.bugs[0].title = "lấy data, vào bugs, phần tử đầu (số 0), lấy title"
```

Hai dòng đầu gọi API và chuyển response thành JSON. Dòng cuối cho thấy cách truy cập: `data.bugs[0].title` nghĩa là "lấy data, vào trường `bugs`, lấy phần tử đầu tiên (đánh số từ 0), rồi lấy `title`". Hiểu được đúng một dòng này là bạn đã nắm phần lớn cách đọc code xử lý API — và quan trọng hơn, nhận ra được khi nào AI đang lần theo đường dẫn sai (ví dụ viết `data.title` trong khi `title` nằm sâu bên trong `bugs`).

> 💡 **Tip:** JSON khi bị "ép" thành một dòng dài ngoằng thì gần như không đọc nổi. Có những công cụ miễn phí, chạy ngay trên trình duyệt, giúp "trải" JSON ra cho thẳng hàng (prettify) và tô màu — dán response vào là đọc rõ như bản vẽ. Đây là thói quen nên có ngay từ đầu khi soi dữ liệu API.

> 🧰 **Đề xuất công cụ:** *Tính đến 2026-07.* Để gửi thử request và xem response mà không phải viết code, nhóm công cụ test API hiện có Postman, Insomnia, Hoppscotch (chạy trong trình duyệt); để làm đẹp JSON có các trang JSON formatter online và tính năng sẵn trong hầu hết code editor. Tên và tính năng đổi khá nhanh — kiểm tra trang chủ trước khi chọn, và cân nhắc trước khi dán dữ liệu thật của công ty lên công cụ online.

## Ghép lại: từ lỗi 401 tới bức tranh tổng thể

Giờ ghép mọi thứ. Khi bạn mô tả cho AI: "Tạo app theo dõi bug có danh sách, bộ lọc và biểu đồ", nó dựng **frontend** (form nhập bug, bảng danh sách, biểu đồ — chạy trên browser người dùng) và cấu hình **backend cùng database** (tạo bảng `bugs`, dựng các API endpoint, thiết lập xác thực). Khi người dùng tạo bug, browser gửi **POST** kèm token trong header lên endpoint, server lưu vào database và trả `201`. Khi xem danh sách, browser gửi **GET**, server query database và trả về JSON, browser render thành bảng.

Hiểu chu trình này đổi được ba thứ trong công việc hằng ngày. **Một**, bạn mô tả yêu cầu chính xác hơn — tách rõ đâu là việc của frontend, đâu là của backend, đâu là của database. **Hai**, bạn debug đúng chỗ — nhìn status code là biết lỗi thuộc phía nào trước khi mở bất cứ dòng code nào; ta sẽ đi sâu vào kỹ năng đọc lỗi này ở Chương 14. **Ba**, bạn nói cùng ngôn ngữ với đội dev, dù không viết code.

Và cái `401` đầu chương? Giờ nó không còn là mật mã. Số `4` báo lỗi nằm ở phía request chứ không phải dịch vụ bên thứ ba bị sập. Chữ "Unauthorized" báo request thiếu danh tính — nhiều khả năng token không được đính kèm hoặc đã hết hạn. Không phải lỗi "của AI" một cách chung chung, mà là một câu hỏi cụ thể bạn đưa cho AI: "Đảm bảo mọi request có gắn header Authorization, và xử lý cả trường hợp token hết hạn." Đó là khác biệt giữa ngồi thử mò và biết mình đang tìm gì.

> 🔒 **Bảo mật:** Một quy tắc vàng: **không bao giờ tin dữ liệu gửi từ frontend**. Bất cứ thứ gì browser gửi lên đều có thể bị người dùng chỉnh sửa, nên mọi kiểm tra quan trọng phải xảy ra ở backend. Khi nhờ AI tạo form, luôn kèm câu: "Thêm kiểm tra dữ liệu (validation) ở phía server cho mọi trường." Và token trong header Authorization là chìa khóa vào hệ thống — không để lộ nó trong code, ảnh chụp màn hình hay log. Ta sẽ bàn kỹ cách quản lý token an toàn ở Chương 12.

## Tóm tắt

- Web chạy theo chu trình request-response: browser (frontend) gửi yêu cầu, server (backend) xử lý — có thể lấy dữ liệu từ database — rồi trả kết quả về. Ẩn dụ nhà hàng: khách, bồi bàn/bếp, kho, thực đơn.
- Frontend chạy trên thiết bị người dùng; backend chạy trên server ở xa và giữ mọi logic quan trọng. Database lưu dữ liệu có cấu trúc, tư duy như một file Excel mạnh.
- HTTP methods GET/POST/PUT/DELETE ghép thành vòng đời CRUD (Create, Read, Update, Delete) — bốn thao tác cơ bản của mọi app.
- API là "thực đơn" — hợp đồng giữa frontend và backend; REST tổ chức dữ liệu thành các endpoint (URL), số nhiều cho danh sách, thêm ID để chỉ một cái cụ thể.
- Status code cho biết kết quả qua chữ số đầu: 2xx tốt, 4xx lỗi phía client, 5xx lỗi phía server. 401 là "chưa biết bạn là ai" (đăng nhập/token), 403 là "không có quyền" (phân quyền) — đừng lẫn hai mã.
- Headers mang thông tin đi kèm: Content-Type (định dạng dữ liệu) và Authorization (token xác thực). Thiếu hoặc hết hạn token là nguyên nhân phổ biến của lỗi 401.
- JSON là định dạng dữ liệu phổ biến nhất: `{}` cho object, `[]` cho array, lồng nhau nhiều tầng. Đọc từ ngoặc ngoài cùng đi vào trong.

## Bài tập

**BT 7.1 — Chẩn đoán status code**

Với mỗi tình huống sau, ghi ra status code khả dĩ nhất (chọn từ 200, 201, 400, 401, 403, 404, 500) và một câu giải thích lỗi thuộc phía nào (client hay server) cùng hướng xử lý đầu tiên:

1. Người dùng tạo bug mới thành công.
2. App gọi API danh sách bug nhưng chưa đăng nhập.
3. Tester đã đăng nhập, bấm nút "Xóa project" nhưng không được phép.
4. Form gửi lên thiếu trường `title` bắt buộc.
5. API gọi tới một endpoint bị gõ sai tên.

*Đầu ra mong đợi:* Một bảng 5 dòng, mỗi dòng gồm: tình huống, status code, phía gây lỗi, câu hỏi/hướng xử lý đầu tiên. Đối chiếu lại với ẩn dụ "thẻ VIP" cho 401 và 403.

**BT 7.2 — Đọc JSON lồng nhau**

Cho JSON sau mô tả một dự án:

```json
{
  "project": "E-Commerce App",
  "team": {
    "lead": "Hoa",
    "members": [
      { "name": "Minh", "role": "tester", "tasks": 12 },
      { "name": "Lan", "role": "developer", "tasks": 8 },
      { "name": "Duc", "role": "tester", "tasks": 15 },
      { "name": "Nga", "role": "ba", "tasks": 6 }
    ]
  },
  "stats": { "total_bugs": 47, "resolved": 31, "open": 16 }
}
```

Trả lời: Team có bao nhiêu thành viên? Ai là lead? Những ai có role "tester"? Tổng số tasks của cả team là bao nhiêu? Tỉ lệ bug đã resolved là bao nhiêu phần trăm? Cuối cùng, viết đường dẫn kiểu `data.…` để lấy đúng `tasks` của thành viên thứ hai.

*Đầu ra mong đợi:* Câu trả lời cho từng câu hỏi, kèm đường dẫn truy cập đúng cú pháp. Bắt đầu từ ngoặc ngoài cùng, xác định các key tầng đầu (`project`, `team`, `stats`) rồi đi sâu vào; `team.members` là array — đếm số phần tử trong đó.

## Tiếp theo

Bạn đã có tấm bản đồ: browser, server, database nói chuyện với nhau ra sao, và cách đọc một cái `401` cho đúng. Nhưng những trang web bạn thấy — bố cục gọn gàng, nút bấm đúng chỗ, chữ nghĩa rõ ràng — đều bắt đầu từ một ngôn ngữ đơn giản đến bất ngờ: HTML, cùng với CSS để tạo kiểu dáng.

Chương 8 dạy bạn *đọc hiểu* giao diện — không phải để tự viết, mà để khi AI sinh ra một trang, bạn biết nhìn vào đâu, hiểu cái gì, và chỉ đúng chỗ cần AI sửa.
