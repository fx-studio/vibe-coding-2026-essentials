# Phụ lục B: Checklist bảo mật trước khi deploy

Bảo mật không phải là thứ nghĩ đến một lần rồi xong. Nó giống kiểm tra sức khỏe định kỳ — mỗi lần đưa app lên mạng là một lần "khám bệnh". Phụ lục này là checklist để bạn tick trước khi deploy, dựng trên hai công cụ tư duy đã học ở phần chất lượng và bảo mật: **10 lỗi bảo mật AI hay sinh ra** và **khung SHIELD** sáu lớp (cả hai ở Chương 16).

Cách dùng: in ra, hoặc copy vào một file riêng trong project. Checklist chia theo bốn giai đoạn của vòng đời một app — trước khi code, trong khi code, trước khi deploy, và sau khi deploy. Mỗi khi bắt đầu hoặc kết thúc một giai đoạn, chạy qua các ô tương ứng. Ô nào còn trả lời "Chưa" là một việc cần làm trước khi đi tiếp. Danh sách trông dài, nhưng khi đã quen bạn sẽ chạy hết trong 10–15 phút — và nó cứu bạn khỏi những sự cố có thể mất hàng ngày, hàng tuần để dọn.

> 🔒 **Bảo mật:** Checklist này viết cho các app dựng bằng vibe coding trên tech stack của sách. Nếu bạn dùng nền tảng backend khác, các nguyên tắc vẫn nguyên vẹn — chỉ đổi tên cơ chế cụ thể. Ví dụ, "RLS" (Row Level Security — phân quyền đọc/ghi ngay tại tầng database) là tên gọi của một nền tảng; nền tảng khác có cơ chế tương đương với tên khác. Điều không đổi là câu hỏi: *database có tự từ chối trả dữ liệu của người này cho người kia không?*

## Giai đoạn 1: Trước khi code — xây nền móng an toàn

Giai đoạn này ứng với bước **Define** trong quy trình năm giai đoạn (Chương 3): viết PRD, thiết kế cấu trúc dữ liệu, chuẩn bị môi trường. Nhiều lỗ hổng nghiêm trọng bắt nguồn từ chỗ bỏ qua bảo mật ngay từ khâu thiết kế — như xây nhà mà quên tính chỗ đặt khóa cửa.

### Checklist PRD và thiết kế

- [ ] PRD có một mục **Security Requirements** riêng, không trộn lẫn với functional requirements
- [ ] Đã xác định dữ liệu nào là **nhạy cảm** (tên, email, mật khẩu, số điện thoại, dữ liệu tài chính)
- [ ] Đã xác định **ai được truy cập gì** — phân quyền theo vai trò nếu cần (admin, user, viewer)
- [ ] Đã xác định **quy định pháp lý** liên quan (GDPR, Nghị định 13/2023/NĐ-CP nếu app có dữ liệu cá nhân)
- [ ] Wireframe/mockup chỉ rõ trang nào **yêu cầu đăng nhập**, trang nào để public

### Checklist môi trường làm việc

- [ ] Có một project database **riêng cho development**, tách khỏi project production (không lấy production ra "thử")
- [ ] File `.gitignore` đã có dòng `.env*` **trước commit đầu tiên**
- [ ] Đã tạo file `.env.example` liệt kê tên các biến cần thiết, không chứa giá trị thật
- [ ] Rules file của project có phần **quy tắc bảo mật** — ví dụ: "Mọi API endpoint phải kiểm tra đăng nhập. Không viết cứng API key. Luôn dùng truy vấn tham số hóa." (cách viết rules file: Chương 6)

> 📋 **Dành cho PM/BA:** Khi viết PRD — cho team hoặc cho chính mình — hãy thêm một mục "Security Requirements" với ít nhất ba câu trả lời: (1) dữ liệu nào cần bảo vệ, (2) ai được truy cập gì, (3) quy định pháp lý nào áp dụng. Ba câu này định hình toàn bộ cách AI sinh code về sau; bỏ trống chúng thì AI mặc định làm "cho chạy được", không làm "cho an toàn". Cách viết PRD để AI hiểu đúng nằm ở Chương 5.

## Giai đoạn 2: Trong khi code — dựng từng tầng bảo vệ

Đây là giai đoạn dài nhất, ứng với bước **Build** và **Debug** (Chương 3). Mỗi lần AI sinh code mới, chạy qua các ô dưới trước khi commit. Hãy xem chúng như một bộ lọc — code phải qua bộ lọc mới được ghi vào lịch sử Git.

### Authentication và Authorization — SHIELD: S + H (chi tiết ở Chương 12)

- [ ] Mọi API endpoint có kiểm tra người dùng đã đăng nhập chưa
- [ ] Endpoint trả về **401** nếu chưa đăng nhập, **403** nếu đã đăng nhập nhưng không đủ quyền
- [ ] Người dùng chỉ thấy **dữ liệu của mình**, không phải toàn bộ database — lọc theo `user_id` hoặc dựa vào RLS (Chương 11)
- [ ] Dùng dịch vụ auth có sẵn cho việc đăng nhập — **KHÔNG** tự xây hệ thống auth từ đầu
- [ ] Trang cần bảo vệ tự redirect về trang đăng nhập nếu chưa login
- [ ] Có một lớp middleware kiểm tra đăng nhập cho mọi nhóm route cần bảo vệ

### Input Validation — SHIELD: I (chi tiết ở Chương 16)

- [ ] Mọi form có **kiểm tra phía client** (hiện lỗi ngay khi người dùng nhập sai)
- [ ] Mọi API endpoint có **kiểm tra phía server** — **KHÔNG** chỉ dựa vào phía client, vì client dễ bị bỏ qua
- [ ] Email, mật khẩu và các trường nhạy cảm có ràng buộc cụ thể (độ dài tối thiểu/tối đa, định dạng)
- [ ] **Không có** chỗ nào chèn HTML thô từ dữ liệu người dùng mà chưa làm sạch (`dangerouslySetInnerHTML`)
- [ ] Nếu có upload file: kiểm tra loại file, giới hạn kích thước, và đổi tên file thành chuỗi ngẫu nhiên

### Secrets và biến môi trường — SHIELD: E (chi tiết ở Chương 12)

- [ ] **Không có** API key, mật khẩu, hay token nào bị viết cứng trong code (tìm các chuỗi như `sk_`, `pk_`, `eyJ`, hay URL có chứa key)
- [ ] Mọi secret nằm trong file môi trường ở máy dev, hoặc trong bảng cấu hình của nền tảng hosting ở production
- [ ] Chỉ đặt tiền tố `NEXT_PUBLIC_` cho những giá trị **không bí mật** (ví dụ: URL công khai của database, anon key)
- [ ] Service role key, mật khẩu database, secret token **KHÔNG** được đặt tiền tố `NEXT_PUBLIC_` (nếu không, chúng lộ ra trình duyệt)

> ⚠️ **Lưu ý:** Nếu bạn đã lỡ push một API key lên repo dù chỉ một lần, hãy coi key đó đã lộ. Vào dịch vụ tạo key, **tạo key mới và hủy key cũ ngay hôm nay** — bot quét repo công khai có thể phát hiện key lộ trong vài phút. Xóa key khỏi commit sau đó không cứu được: nó đã nằm trong lịch sử và có thể đã bị đọc.

### Dependencies và packages

- [ ] Mọi package AI gợi ý đã được **tra trên kho package công khai** (số lượt tải, thời gian tồn tại, có phải package thật không) — tránh package "ảo" AI bịa ra
- [ ] Đã chạy lệnh kiểm tra lỗ hổng của trình quản lý package, và không còn lỗ hổng mức **critical** hay **high** chưa xử lý
- [ ] Không cài package mà bạn không hiểu chức năng — hỏi AI giải thích trước khi cài

### Code review — SHIELD: H (chi tiết ở Chương 13)

- [ ] Đã xem **diff** trước khi commit — AI có sửa file nào bạn không yêu cầu không?
- [ ] Đã yêu cầu AI **tự review bảo mật** đoạn vừa tạo (prompt: "Review bảo mật code này, trả lời trung thực, đừng chiều ý tôi")
- [ ] Không commit đoạn code mà bạn **không giải thích được** chức năng
- [ ] Mỗi tính năng mới được test ít nhất **happy path + hai edge case** trước khi merge (tư duy test case: Chương 15)

## Giai đoạn 3: Trước khi deploy — kiểm tra tổng thể

Đây là "đợt khám cuối" trước khi app lên production, ứng với bước **Ship** (Chương 3). Bạn chạy toàn bộ SHIELD một lần nữa trên project hoàn chỉnh. Nếu giai đoạn 2 là kiểm từng viên gạch, giai đoạn 3 là kiểm cả ngôi nhà trước khi bàn giao.

### SHIELD tổng thể (khung đầy đủ ở Chương 16)

- [ ] **S — Separation:** project database dev và prod là **hai project riêng biệt**
- [ ] **S — Separation:** biến môi trường trên nền tảng hosting là của **production**, không phải key của dev
- [ ] **H — Human in the loop:** đã review diff toàn bộ code trước khi merge vào nhánh chính
- [ ] **I — Input validation:** mọi API endpoint có kiểm tra phía server
- [ ] **E — Environment:** file `.env` không nằm trong lịch sử Git (kiểm tra bằng `git log --all --full-history -- "*.env*"`)
- [ ] **E — Environment:** cấu hình CORS **không dùng wildcard** `*` ở production
- [ ] **E — Environment:** HTTPS đã bật (phần lớn nền tảng hosting bật sẵn; kiểm tra lại nếu dùng tên miền riêng)
- [ ] **L — Logging:** có ghi lại sự kiện đăng nhập (cả thành công và thất bại)
- [ ] **L — Logging:** có ghi lại các lần truy cập bị từ chối vì thiếu quyền
- [ ] **D — Defense:** RLS được **bật trên tất cả bảng** (Chương 11)
- [ ] **D — Defense:** lệnh kiểm tra lỗ hổng trả về 0 lỗi critical/high

### Checklist tầng database (chi tiết ở Chương 11)

- [ ] Tất cả bảng đều **bật RLS**
- [ ] Policy của RLS kiểm tra danh tính người đăng nhập — **không** để điều kiện luôn đúng (`true`) cho thao tác đọc/ghi trên bảng có dữ liệu nhạy cảm
- [ ] Service role key **chỉ dùng ở phía server**, không bao giờ xuất hiện trong code chạy ở trình duyệt
- [ ] Đã bật xác nhận email khi đăng ký (tránh tài khoản spam)

### Checklist triển khai (chi tiết ở Chương 12)

- [ ] Biến môi trường được cấu hình đúng cho **production**, không nhầm sang môi trường preview hay development
- [ ] Đã đặt hạn mức chi tiêu trên nền tảng hosting và các dịch vụ API, để một vòng lặp lỗi không tạo ra hóa đơn bất ngờ
- [ ] Nếu dùng tên miền riêng, đã cấu hình SSL/HTTPS đúng

> 🧪 **Dành cho Tester/QA:** Giai đoạn này là nơi tư duy QA tỏa sáng. Hãy đối xử với checklist như một **test plan** trước release: mỗi ô "Chưa" là một bug/action item cụ thể, có người phụ trách và ngày hết hạn. Và nhớ rằng security testing với functional testing bổ trợ nhau — một app "chạy đúng" nhưng không an toàn cũng nguy hiểm ngang một app "an toàn" nhưng đầy bug. Đừng ký nghiệm thu khi mới xong một nửa.

## Giai đoạn 4: Sau khi deploy — duy trì và giám sát

Deploy không phải là kết thúc, chỉ là bắt đầu của giai đoạn vận hành. Như một nhà hàng đã khai trương vẫn phải kiểm vệ sinh và bảo trì mỗi ngày. Nhiều lỗ hổng xuất hiện *sau* khi deploy: một thư viện cũ bị phát hiện có lỗi, hoặc bạn thêm tính năng mới mà quên kiểm tra bảo mật.

### Checklist định kỳ (mỗi tuần hoặc mỗi lần cập nhật lớn)

- [ ] Chạy lại lệnh kiểm tra lỗ hổng và xử lý mọi cảnh báo mới
- [ ] Xem nhật ký đăng nhập của dịch vụ auth — có bất thường không (nhiều lần đăng nhập thất bại từ cùng một IP)?
- [ ] Xem thống kê truy cập của nền tảng hosting — có luồng traffic bất thường không?
- [ ] Nếu đã gắn một dịch vụ quét bảo mật tự động, xem báo cáo mới nhất
- [ ] Cập nhật các thư viện lên phiên bản ổn định mới nhất

### Checklist xử lý sự cố

- [ ] Nếu nghi ngờ bị tấn công: **tạo lại toàn bộ API key** ngay lập tức
- [ ] Đọc log để xác định phạm vi ảnh hưởng
- [ ] Thông báo người dùng nếu dữ liệu cá nhân của họ có thể đã bị ảnh hưởng
- [ ] Ghi lại sự cố và cách xử lý vào một **nhật ký sự cố** để phòng lần sau

### Checklist khi thêm tính năng mới

- [ ] Mọi tính năng mới chạy lại **checklist giai đoạn 2** (trong khi code)
- [ ] Nếu tính năng mới đụng tới dữ liệu nhạy cảm hoặc quyền truy cập, chạy lại thêm **checklist giai đoạn 3**
- [ ] Commit **trước khi** bắt đầu tính năng mới, tạo một điểm quay về an toàn (Chương 13)

> 🧰 **Đề xuất công cụ:** *Tính đến 2026-07.* Ngoài lệnh kiểm tra lỗ hổng có sẵn trong trình quản lý package, có hai nhóm dịch vụ quét bảo mật đáng biết cho giai đoạn giám sát: nhóm quét dependency và code mỗi khi bạn push lên repo (ví dụ Snyk), và nhóm phân tích chất lượng code toàn diện gồm cả lỗ hổng (ví dụ SonarCloud). Prompt security audit ở cuối phụ lục chạy tốt nhất trong một AI IDE đọc được toàn bộ codebase. Bậc miễn phí và tính năng của các dịch vụ này đổi liên tục — kiểm tra trang chủ trước khi phụ thuộc, đừng tin con số trong bất kỳ cuốn sách nào.

## 10 lỗi bảo mật AI code thường gặp — bảng tra cứu nhanh

Bảng dưới tóm tắt 10 lỗi (chi tiết từng lỗi ở Chương 16), kèm cách kiểm tra nhanh và mức độ nghiêm trọng. Dùng để tra khi review code AI sinh ra.

| # | Lỗi | Mức độ | Cách kiểm tra nhanh |
|---|-----|--------|---------------------|
| 1 | Phân quyền hỏng (broken access control) | Critical | Mở từng file API, tìm chỗ kiểm tra đăng nhập. Không có = lỗi. |
| 2 | Secret viết cứng | Critical | Tìm `sk_`, `pk_`, `eyJ`, URL chứa key trong code. |
| 3 | SQL injection | Critical | Tìm SQL thô ghép chuỗi trực tiếp từ input người dùng. |
| 4 | Thiếu kiểm tra input (XSS) | High | Tìm `dangerouslySetInnerHTML`. Thử nhập `<script>alert(1)</script>` vào form. |
| 5 | Package "ảo" (slopsquatting) | High | Tra mọi package trên kho công khai trước khi cài. |
| 6 | Cấu hình mở quá rộng | High | Tìm `origin: '*'` trong cấu hình CORS. Kiểm tra RLS trên database. |
| 7 | Bỏ qua xác thực | High | Rà mọi endpoint và trang — có chỗ nào thiếu kiểm tra đăng nhập? |
| 8 | Thư viện lỗi thời | Medium | Chạy lệnh kiểm tra lỗ hổng. Xem phiên bản trong file khai báo package. |
| 9 | Code thừa | Medium | Có file nào bạn không hiểu chức năng? Hỏi AI giải thích hoặc xóa. |
| 10 | Thiếu tuân thủ pháp lý | Medium | App có xử lý dữ liệu cá nhân? Đã xác định quy định áp dụng chưa? |

> 💡 **Tip:** Copy bảng này vào rules file của project (Chương 6) để AI tự kiểm khi sinh code. Thêm một dòng: "Trước khi hoàn thành, kiểm tra code không mắc 10 lỗi bảo mật phổ biến: [liệt kê]." Càng cụ thể, AI càng ít "sáng tạo" ra những lỗi bạn không muốn.

## Prompt mẫu: nhờ AI chạy security audit

Thay vì tự rà thủ công từng mục, bạn có thể nhờ AI. Prompt dưới gộp SHIELD và 10 lỗi phổ biến thành một bài kiểm tra toàn diện:

```
"Hãy thực hiện security audit cho project này. Kiểm tra:

SHIELD:
- S: Project có tách biệt dev/prod không?
- H: Có quy trình review trước merge không?
- I: Liệt kê tất cả API endpoint và form. Cái nào chưa có
  kiểm tra phía server?
- E: File .env có trong .gitignore không? CORS có dùng wildcard không?
- L: Có ghi log cho sự kiện đăng nhập và truy cập bị từ chối không?
- D: Chạy kiểm tra lỗ hổng dependency. RLS có bật trên mọi bảng không?

10 lỗi phổ biến:
- Có phân quyền hỏng (API thiếu kiểm tra đăng nhập) không?
- Có secret viết cứng không?
- Có SQL thô ghép chuỗi không?
- Có chèn HTML thô chưa làm sạch không?
- Có package nào lạ hoặc mới xuất hiện không?
- CORS có dùng wildcard * không?
- Có endpoint nào bỏ qua xác thực không?
- Kiểm tra lỗ hổng có báo lỗi critical/high không?
- Có file nào không rõ chức năng không?

Cho điểm từng mục 0–3. Gợi ý cách khắc phục cho mục dưới 2.
Trả lời trung thực, đừng chiều ý tôi."
```

Prompt dài nhưng cần thiết — nó cho AI đủ ngữ cảnh để audit có hệ thống thay vì trả lời qua loa. Chạy trong một AI IDE đọc được toàn bộ codebase để AI thấy hết các file.

## Tóm tắt

- Checklist bảo mật trải bốn giai đoạn — trước khi code, trong khi code, trước khi deploy, sau khi deploy — bao phủ toàn bộ vòng đời app.
- Giai đoạn "trước khi code" lo phần thiết kế an toàn: PRD có mục bảo mật, môi trường dev/prod tách biệt, rules file có quy tắc bảo mật.
- Giai đoạn "trong khi code" soi từng dòng: đăng nhập và phân quyền, kiểm tra input, secret, dependency, và review diff.
- Giai đoạn "trước deploy" chạy trọn khung SHIELD và kiểm RLS, CORS, lỗ hổng dependency trên project hoàn chỉnh.
- Giai đoạn "sau deploy" giữ bảo mật lâu dài: cập nhật thư viện, giám sát log, và có sẵn quy trình xử lý sự cố.
- Bảng 10 lỗi và prompt audit giúp bạn tra nhanh khi review và nhờ AI hỗ trợ soát.

## Đọc sâu từng phần

Checklist này gom kiến thức rải trong nhiều chương. Muốn hiểu sâu:

- **10 lỗi bảo mật và khung SHIELD:** Chương 16
- **Auth, secrets, biến môi trường, triển khai:** Chương 12
- **Row Level Security và tầng database:** Chương 11
- **Rules file:** Chương 6
- **Quy trình năm giai đoạn (Define–Build–Ship):** Chương 3
- **Viết PRD để AI hiểu đúng:** Chương 5
- **Tư duy test case:** Chương 15
- **Git và review diff:** Chương 13
