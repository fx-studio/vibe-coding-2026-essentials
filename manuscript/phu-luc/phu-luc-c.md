# Phụ lục C: Thuật ngữ Anh–Việt

Viết về công nghệ thì không tránh được thuật ngữ tiếng Anh. Nhưng mục tiêu của bảng này không phải bắt bạn học thuộc định nghĩa -- mà là để bạn hiểu đúng một từ khi gặp nó trong bối cảnh thực tế: khi đọc code AI sinh ra, khi trao đổi với developer, hay khi viết bug report.

Bảng dưới đây gom mọi thuật ngữ kỹ thuật xuất hiện trong cuốn sách này, sắp theo thứ tự A–Z. Mỗi mục gồm ba phần: tên tiếng Anh, giải thích ngắn bằng tiếng Việt (kèm ẩn dụ khi cần), và số chương giới thiệu thuật ngữ đó lần đầu. Bạn không cần đọc từ đầu đến cuối -- hãy dùng nó như bảng tra cứu: gặp từ lạ thì lật đến đây tìm theo chữ cái đầu tiên.

> 💡 **Tip:** Cột **Ch.** ghi chương đầu tiên thuật ngữ xuất hiện. Nếu muốn xem thuật ngữ được dùng trong ngữ cảnh đầy đủ, mở lại chương đó.

---

## A

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Acceptance criteria** | Tiêu chí chấp nhận -- điều kiện để tính năng được coi là hoàn thành. Giống như "checklist bàn giao" khi nhận nhà mới: có đủ phòng, có nước nóng, cửa khóa được. | 1 |
| **Access control testing** | Kiểm tra phân quyền -- xác nhận mỗi role chỉ truy cập được những gì được phép. | 20 |
| **Activity log** | Nhật ký tự động ghi lại mọi thay đổi trên issue (ai thay đổi gì, khi nào). | 20 |
| **Agentic engineering** | Lập trình hỗ trợ AI với giám sát chuyên nghiệp -- bước tiến hóa từ vibe coding. | 1 |
| **Agentic workflow** | Quy trình AI tự động -- AI tự lập kế hoạch, thực thi, và kiểm tra. | 18 |
| **AI agent** | AI tự tạo file, viết code, chạy commands và iterate tự động (khác với AI assistant chỉ gợi ý). | 18 |
| **AI assistant** | AI gợi ý code để người dùng copy-paste, không tự thực thi. | 18 |
| **API (Application Programming Interface)** | "Hợp đồng" giữa frontend và backend, quy định cách gửi request và nhận response. Đọc là "ey-pi-ai." | 1 |
| **API route (Next.js)** | File `route.ts` trong `app/api/`, xử lý logic backend (nhận data, truy vấn DB). | 6 |
| **App Router** | Hệ thống routing của Next.js dựa trên cấu trúc thư mục `app/`. | 6 |
| **Arrow function** | Cách viết function ngắn gọn với dấu `=>`, AI ưa thích dùng. | 9 |
| **Async/await** | Cơ chế chờ đợi dữ liệu từ API hoặc server -- giống như đặt món rồi ngồi chờ. | 9 |
| **Attribute** | Thuộc tính bổ sung thông tin cho HTML element, ví dụ `class`, `id`, `href`. | 8 |
| **Auth provider** | Nhà cung cấp dịch vụ xác thực dùng sẵn. | 12 |
| **Authentication** | Đăng nhập/đăng ký -- xác minh "bạn là ai." | 12 |
| **Autonomy** | Khả năng AI agent tự hành động mà không cần người dùng can thiệp từng bước. | 18 |

## B

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Backend** | Phần xử lý logic và dữ liệu chạy trên server -- "nhà bếp" của ứng dụng web. | 3 |
| **Backend-as-a-Service (BaaS)** | Dịch vụ backend dùng ngay, không cần tự xây. | 11 |
| **Bearer token** | Chuỗi ký tự xác thực gửi trong header Authorization dạng `Bearer <token>`. | 7 |
| **Branch** | Nhánh phát triển song song -- "vũ trụ song song" cho code. Bạn thử nghiệm trên branch riêng mà không ảnh hưởng bản gốc. | 12 |
| **Broken access control** | Lỗi API không kiểm tra quyền truy cập của người dùng -- lỗi bảo mật #1 theo OWASP. | 16 |
| **Browser** | Trình duyệt -- Chrome, Safari, Firefox. Đọc là "brao-zơ." | 7 |

## C

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Callback flow** | Sự kiện chạy từ component con lên cha qua function callback. | 9 |
| **CLI (Command Line Interface)** | Giao diện dòng lệnh, cách gọi khác của terminal. | 6 |
| **Client Component** | Component chạy trên browser, có thể dùng hooks như `useState`. Cần thêm `"use client"`. | 10 |
| **Column** | Cột/trường thông tin trong table (database). | 7 |
| **Commit** | Lưu snapshot code tại một thời điểm -- "save game" trong Git. | 3 |
| **Component** | Thành phần UI tái sử dụng được -- giống khối LEGO, lắp ghép thành giao diện. | 1 |
| **Component library** | Thư viện thành phần giao diện dùng lại được. | 6 |
| **Component tree** | Cấu trúc phân cấp cha-con của tất cả component trong ứng dụng. | 9 |
| **Context (prompting)** | Ngữ cảnh, thông tin nền AI cần để hiểu yêu cầu của bạn. | 2 |
| **Context window** | Lượng text mà AI xử lý cùng lúc -- giống như "bộ nhớ làm việc" của AI. | 3 |
| **CORS (Cross-Origin Resource Sharing)** | Cơ chế bảo mật browser khi gọi API khác domain. | 14 |
| **Critical path (code)** | Những function/component được gọi nhiều nhất, cần ưu tiên hiểu và review. | 19 |
| **CRUD** | Create, Read, Update, Delete -- bốn thao tác cơ bản của mọi ứng dụng. | 7 |
| **CSRF (Cross-Site Request Forgery)** | Loại tấn công lừa browser gửi request giả mạo. | 12 |
| **CSS (Cascading Style Sheets)** | Bảng định kiểu xếp tầng -- ngôn ngữ trang trí giao diện web. Đọc là "xi-ét-ét." | 2 |

## D

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Data structure** | Cấu trúc dữ liệu -- cách tổ chức dữ liệu: bảng nào, cột nào, quan hệ nào. | 5 |
| **Database** | Cơ sở dữ liệu -- nơi lưu trữ dữ liệu có cấu trúc, giống "Excel nâng cao." | 2 |
| **Debug spiral** | Vòng xoáy debug -- hiện tượng fix liên tục làm code phức tạp hơn. | 14 |
| **Decomposition** | Chia nhỏ yêu cầu thành các phần quản lý được. | 1 |
| **Defense-in-depth** | Nguyên tắc phòng thủ nhiều tầng, kiểm tra auth ở nhiều nơi. | 20 |
| **Dependencies** | Danh sách thư viện mà project sử dụng, liệt kê trong `package.json`. | 5 |
| **Deploy** | Triển khai lên server/internet -- đưa app từ máy tính của bạn lên cho mọi người dùng. Đọc là "đi-ploi." | 2 |
| **DevTools** | Công cụ nhà phát triển trong trình duyệt -- mở bằng F12. | 12 |
| **Diff** | Bản thay đổi giữa phiên bản cũ và mới của code -- dòng xanh là thêm, dòng đỏ là xóa. | 1 |
| **Discard (Git)** | Bỏ thay đổi chưa commit, đưa file về trạng thái trước đó. | 13 |
| **Domain** | Tên miền -- "địa chỉ nhà" trên internet. | 2 |
| **Domain knowledge** | Kiến thức chuyên ngành -- lợi thế lớn nhất của Tester/PM/BA trong vibe coding. | 2 |
| **Dynamic route** | Đường dẫn động, dùng `[id]` để đại diện cho nhiều giá trị URL. | 10 |

## E

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Edge case** | Trường hợp biên/ngoại lệ -- tình huống bất thường ngoài kịch bản lý tưởng. | 2 |
| **Element** | Một thành phần HTML hoàn chỉnh (tag mở + nội dung + tag đóng). | 8 |
| **Encapsulation** | Đóng gói -- nguyên tắc mỗi component quản lý phạm vi riêng của mình. | 9 |
| **Endpoint** | Địa chỉ URL trả về dữ liệu, ví dụ `/api/users`, `/api/bugs/42`. | 5 |
| **Environment variables** | Biến môi trường -- thông tin bí mật (API key, DB password) trong `.env.local`. | 3 |
| **Error prompt** | Prompt debug gồm lỗi + code + expected behavior. | 2 |
| **Extension (file)** | Phần đuôi tên file (`.ts`, `.tsx`, `.json`...) cho biết loại nội dung. | 10 |

## F

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **File-based routing** | Định tuyến dựa trên cấu trúc thư mục -- tạo file = tạo trang web (Next.js). | 7 |
| **Flexbox (flex)** | Chế độ layout xếp phần tử theo hàng/cột. | 8 |
| **Foreign key** | Khóa ngoại -- trường trong bảng này trỏ đến bảng khác, tạo liên kết dữ liệu. | 5 |
| **Frontend** | Phần giao diện chạy trên browser của người dùng -- "phòng khách" của ứng dụng web. | 7 |
| **Function** | Hàm -- khối code thực hiện một hành động cụ thể, có thể gọi lại nhiều lần. | 4 |

## G

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **GDPR** | Quy định bảo vệ dữ liệu chung của EU. | 16 |
| **Git** | Hệ thống quản lý phiên bản -- "save game" cho code. Đọc là "ghít." | 6 |
| **git reset --hard** | Lệnh quay về commit cũ và xóa hoàn toàn lịch sử sau đó -- dùng cẩn thận! | 13 |
| **git revert** | Lệnh tạo commit mới để undo thay đổi của commit trước, giữ nguyên lịch sử. | 13 |
| **.gitignore** | File danh sách những file/thư mục Git sẽ không theo dõi (vd: `.env.local`, `node_modules`). | 10 |
| **Grid** | Chế độ layout dạng lưới. | 8 |

## H

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Happy path** | Con đường hạnh phúc -- kịch bản lý tưởng khi mọi thứ đều đúng. | 2 |
| **Hardcode** | Viết cứng dữ liệu vào code thay vì lưu trong database. | 5 |
| **Hardcoded secrets** | Bí mật (API key, password) viết cứng trong code -- lỗi bảo mật nghiêm trọng. | 16 |
| **Headers (HTTP)** | Thông tin đi kèm request/response: Content-Type, Authorization. | 7 |
| **HTML (HyperText Markup Language)** | Ngôn ngữ đánh dấu cấu trúc nội dung web. Đọc là "ếch-ti-em-eo." | 2 |
| **HTTP (HyperText Transfer Protocol)** | Giao thức truyền siêu văn bản -- "ngôn ngữ" để browser nói chuyện với server. | 7 |
| **Hybrid IT Professional** | Người hiểu cả business context lẫn technical implementation. | 2 |
| **Hydration** | Quá trình kết nối HTML từ server với JavaScript trên browser. | 14 |

## I

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **IDE (Integrated Development Environment)** | Môi trường phát triển tích hợp -- phần mềm để viết code. Đọc là "ai-đi-i." | 1 |
| **Incremental building** | Xây dựng từng bước, mỗi prompt một tính năng. | 2 |
| **Index (database)** | "Mục lục" giúp tìm kiếm nhanh trên cột được đánh index. | 11 |
| **Intent** | Ý định -- điều bạn muốn đạt được, trọng tâm của vibe coding. | 1 |
| **Iterate** | Vòng lặp prompt-review-chỉnh sửa -- quy trình cốt lõi của vibe coding. | 3 |

## J

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **JavaScript** | Ngôn ngữ lập trình thêm "hành vi" cho web, chạy trên mọi trình duyệt. | 1 |
| **JSON (JavaScript Object Notation)** | Định dạng dữ liệu phổ biến -- cách máy tính "nói chuyện" với nhau. Đọc là "jay-sơn." | 7 |
| **JSX** | Cú pháp cho phép viết HTML bên trong JavaScript/TypeScript. | 8 |

## L

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Lifting state up** | Nâng state lên component cha để chia sẻ với các component khác. | 9 |
| **Living document** | Tài liệu sống -- tài liệu được cập nhật liên tục theo tiến trình dự án. | 5 |
| **LLM (Large Language Model)** | Mô hình ngôn ngữ lớn -- "bộ não" của AI. Đọc là "eo-eo-em." | 17 |
| **Local repo** | Repo nằm trên máy tính cá nhân. | 13 |
| **localhost** | Địa chỉ máy tính của bạn, dùng để xem app đang phát triển (`localhost:3000`). | 14 |
| **Lost in the middle** | Hiện tượng AI nhớ tốt đầu và cuối prompt nhưng kém ở giữa. | 6 |

## M

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Many-to-many** | Quan hệ nhiều đối nhiều giữa các bảng, cần bảng trung gian. | 11 |
| **Margin** | Khoảng cách bên ngoài element. | 8 |
| **Markup language** | Ngôn ngữ đánh dấu (khác với ngôn ngữ lập trình). | 8 |
| **MCP (Model Context Protocol)** | "USB-C cho AI" -- chuẩn kết nối AI với dịch vụ bên ngoài. | 14 |
| **MCP Client** | Lớp trung gian tích hợp sẵn trong AI tool, chuyển tiếp yêu cầu đến MCP Server. | 18 |
| **MCP Host** | Phía người dùng (AI tool), nơi gửi yêu cầu qua MCP. | 18 |
| **MCP Server** | Chương trình cung cấp kết nối giữa AI tool và dịch vụ bên ngoài qua chuẩn MCP. | 18 |
| **Merge** | Gộp nhánh -- kết hợp code từ branch này vào branch khác. | 6 |
| **Merge conflict** | Xung đột khi hai branch sửa cùng một file. | 13 |
| **Method (HTTP)** | Phương thức yêu cầu: GET, POST, PUT, DELETE. | 7 |
| **Middleware (Next.js)** | File chạy trước mọi request, dùng để kiểm tra auth và redirect. | 12 |
| **Mobile-first** | Nguyên tắc viết style cho mobile trước, thêm prefix cho màn hình lớn hơn. | 8 |
| **Multi-agent teams** | Nhiều AI agents chuyên môn hóa làm việc song song trên cùng project. | 1 |
| **MVP (Minimum Viable Product)** | Sản phẩm khả dụng tối thiểu -- phiên bản nhỏ nhất còn giá trị. | 1 |

## N

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **npm (Node Package Manager)** | Công cụ quản lý thư viện cho project JavaScript/TypeScript. | 8 |
| **npm audit** | Lệnh kiểm tra lỗ hổng bảo mật trong dependencies của project. | 16 |

## O

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **OAuth (Open Authorization)** | Cơ chế đăng nhập bằng tài khoản bên thứ ba (Google, GitHub). | 12 |
| **One-to-many** | Quan hệ một đối nhiều, ví dụ một user có nhiều bug. | 11 |
| **Orchestrator** | Vai trò mới -- người chỉ huy AI thay vì tự tay code. | 2 |
| **ORM (Object-Relational Mapper)** | Công cụ ánh xạ đối tượng vào cơ sở dữ liệu, viết TypeScript thay SQL. | 11 |
| **OWASP Top 10** | Danh sách 10 lỗ hổng bảo mật ứng dụng web phổ biến nhất. | 12 |

## P

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Padding** | Khoảng đệm bên trong element. | 8 |
| **Path** | Đường dẫn -- trang cụ thể trên website. | 2 |
| **Persona** | Vai trò/nhân vật mà AI đóng khi nhận prompt. | 4 |
| **PEV loop** | Plan-Execute-Verify -- vòng lặp kỷ luật cho vibe coding. | 1 |
| **Policy (RLS)** | Chính sách truy cập -- quy tắc xác định ai được đọc/ghi dữ liệu nào. | 11 |
| **Port** | Cổng kết nối -- giống số phòng trong tòa nhà. | 7 |
| **Portfolio** | Bộ sưu tập dự án -- "hồ sơ năng lực" của bạn. | 20 |
| **PRD (Product Requirements Document)** | Tài liệu mô tả yêu cầu sản phẩm -- "bản vẽ nhà" trước khi code. | 2 |
| **Prefix (Tailwind)** | Tiền tố điều kiện như `sm:`, `md:`, `lg:`, `dark:`, `hover:`. | 8 |
| **Preview deployment** | Phiên bản thử nghiệm, tự động tạo cho mỗi branch khác main. | 12 |
| **Primary key** | Khóa chính -- giá trị duy nhất của mỗi dòng, "căn cước công dân" trong database. | 11 |
| **Prompt** | Câu lệnh cho AI -- "ngôn ngữ lập trình" của vibe coder. Đọc là "prômt." | 1 |
| **Prop drilling** | Truyền props xuyên qua nhiều tầng component trung gian. | 9 |
| **Props** | Dữ liệu truyền vào một component. Đọc là "props." | 6 |
| **Props flow** | Dữ liệu chạy từ component cha xuống con qua props. | 9 |
| **Protected route** | Trang yêu cầu đăng nhập mới truy cập được. | 16 |
| **Prototype** | Bản mẫu chạy được để demo ý tưởng. | 1 |

## Q

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Query parameters** | Tham số truy vấn gửi kèm URL. | 7 |

## R

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Reasoning** | Khả năng phân tích vấn đề sâu, cân nhắc trade-off -- điểm mạnh của các model lớn. | 18 |
| **Refactor** | Tái cấu trúc code hiện tại mà không thay đổi hành vi -- dọn dẹp và tổ chức lại. | 2 |
| **ReferenceError** | Lỗi khi dùng biến chưa được khai báo. | 9 |
| **Regression testing** | Kiểm tra lại các tính năng cũ sau khi sửa lỗi để đảm bảo không bị ảnh hưởng. | 14 |
| **Render** | Vẽ/hiển thị giao diện trên browser. | 7 |
| **Repository (repo)** | Project folder có kèm theo lịch sử thay đổi Git. | 3 |
| **Request** | Yêu cầu mà browser gửi đến server. | 7 |
| **Responsive design** | Thiết kế đáp ứng -- giao diện tự điều chỉnh theo kích thước màn hình. | 8 |
| **REST API** | Kiểu API phổ biến nhất, tổ chức dữ liệu thành endpoint theo tài nguyên. | 7 |
| **Row** | Dòng/bản ghi trong table (database). | 7 |
| **Row Level Security (RLS)** | Cơ chế bảo mật cấp dòng dữ liệu — chỉ cho xem dữ liệu của mình. | 11 |
| **Rules file** | Tệp quy tắc áp dụng cho mọi tương tác AI trong dự án -- "văn hóa công ty" cho AI. | 3 |

## S

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Scaffold** | Tạo khung project ban đầu từ prompt. Đọc là "xkéf-fôld." | 3 |
| **Scope creep** | Phạm vi dự án phồng to dần, mất kiểm soát. | 2 |
| **Security vulnerability** | Lỗ hổng bảo mật -- điểm yếu trong code mà kẻ tấn công có thể khai thác. | 16 |
| **Semantic HTML** | HTML có ngữ nghĩa, dùng tên thẻ mô tả chức năng (`header`, `nav`, `main`). | 8 |
| **Separation of Duties** | Nguyên tắc phân tách trách nhiệm: AI không truy cập production. | 16 |
| **Server** | Máy chủ -- nơi xử lý logic và trả dữ liệu. | 2 |
| **Server Component** | Component chạy trên server, gửi HTML xuống browser (mặc định trong Next.js). | 10 |
| **Session** | Phiên làm việc sau khi đăng nhập. | 4 |
| **SHIELD Framework** | Hệ thống kiểm tra bảo mật sáu lớp: Separation, Human in the Loop, Input Validation, Environment, Logging, Defense in Depth. | 16 |
| **Slopsquatting** | Kỹ thuật tấn công đăng ký package name mà AI hay hallucinate, chứa mã độc. | 16 |
| **Spending limit** | Giới hạn chi tiêu trên dịch vụ API -- "cầu dao tự động" chống hóa đơn bất ngờ. | 12 |
| **SQL (Structured Query Language)** | Ngôn ngữ truy vấn có cấu trúc, dùng để "nói chuyện" với database. Đọc là "xi-kiu-eo." | 4 |
| **SQL injection** | Tấn công bảo mật bằng cách chèn SQL độc hại vào ứng dụng. | 4 |
| **Stack trace** | "Hành trình" của lỗi qua các file, bắt đầu bằng "at..." | 2 |
| **State** | Trạng thái -- dữ liệu thay đổi bên trong component. | 6 |
| **Status code** | Mã trạng thái phản hồi từ server (200 OK, 404 Not Found, 500 Server Error). | 7 |
| **Syntax** | Cú pháp -- cách viết code chính xác theo ngôn ngữ lập trình. | 1 |
| **SyntaxError** | Lỗi khi viết sai cú pháp code. | 9 |

## T

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Table (database)** | Bảng dữ liệu -- tương đương sheet trong Excel. | 7 |
| **Tag** | Thẻ đánh dấu trong HTML, thường đi theo cặp mở-đóng. | 8 |
| **Tech stack** | Bộ công nghệ -- tập hợp các công cụ và framework dùng cho dự án. | 3 |
| **Technical debt** | Nợ kỹ thuật -- "nợ" chất lượng tích lũy khi ưu tiên tốc độ. | 19 |
| **Temperature** | Thông số điều chỉnh mức độ ngẫu nhiên khi AI chọn token: thấp = chính xác, cao = sáng tạo. | 17 |
| **Terminal** | Ứng dụng giao diện text để tương tác với máy tính bằng lệnh. | 9 |
| **Test case table** | Bảng tổ chức test cases gồm Input, Action, Expected/Actual Result, Pass/Fail. | 15 |
| **Token** | Đơn vị text nhỏ nhất AI xử lý -- khoảng bốn ký tự tiếng Anh. | 6 |
| **Type** | Kiểu dữ liệu -- nhãn mác cho biến, xác định loại dữ liệu được phép chứa. | 7 |
| **TypeError** | Lỗi khi dùng sai kiểu dữ liệu. | 3 |
| **TypeScript** | JavaScript có thêm khai báo kiểu dữ liệu (type), giúp bắt lỗi sớm. | 6 |

## U

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **URL** | Địa chỉ tài nguyên trên web. Đọc là "iu-a-eo." | 3 |
| **useContext** | React hook chia sẻ dữ liệu với toàn bộ cây component không cần truyền props từng tầng. | 9 |
| **User enumeration** | Kỹ thuật tấn công dò tìm email/username đã đăng ký trong hệ thống. | 16 |
| **User story** | Câu chuyện người dùng -- mô tả nhu cầu theo format: As a [role], I want [feature] so that [benefit]. | 1 |
| **useState** | React hook tạo state (trạng thái) cho component. | 9 |
| **UUID (Universally Unique Identifier)** | Chuỗi ký tự duy nhất dùng làm ID. | 11 |

## V

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Validation** | Kiểm tra dữ liệu đầu vào -- "bảo vệ cánh cổng" trước khi dữ liệu vào hệ thống. | 1 |
| **Variable** | Biến -- nơi lưu trữ dữ liệu có tên, dùng `const` (hằng) hoặc `let` (biến). | 12 |
| **Vibe coding** | Lập trình theo cảm xúc/ý định -- dùng ngôn ngữ tự nhiên để chỉ đạo AI viết code. | 1 |
| **Vibe PM** | PM sử dụng AI IDE cho công việc sản phẩm. | 2 |
| **Vibe testing** | Xu hướng QA dùng ngôn ngữ tự nhiên để tạo test automation. | 2 |

## W

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **Wireframe** | Bản phác giao diện -- layout các màn hình trước khi build. | 2 |

## X

| Thuật ngữ | Giải thích | Ch. |
|---|---|---|
| **XSS (Cross-Site Scripting)** | Tấn công chèn script độc hại vào trang web qua input người dùng. | 16 |

---

> 📋 **Dành cho PM/BA:** Bảng này giúp bạn hiểu đúng những gì developer và AI đang "nói chuyện" trong lúc làm việc. Bạn không cần nhớ hết -- nhưng biết tra cứu khi cần sẽ giúp bạn tham gia code review và các buổi trao đổi kỹ thuật tự tin hơn nhiều.

> 🧪 **Dành cho Tester/QA:** Rất nhiều thuật ngữ ở đây gắn thẳng với công việc hằng ngày của bạn -- từ *acceptance criteria* đến *regression testing*, từ *edge case* đến *SQL injection*. Hiểu chúng giúp bạn viết bug report chính xác hơn và trao đổi hiệu quả hơn với developer, dù developer đó là con người hay AI.

Danh sách này chỉ gồm các thuật ngữ **khái niệm** thật sự xuất hiện trong sách -- tên sản phẩm và công cụ cụ thể được để trong các box *Đề xuất công cụ* của từng chương, vì chúng thay đổi nhanh và cần bạn tự kiểm chứng. Khi gặp một từ không rõ nghĩa, hãy quay lại đây tra theo chữ cái đầu tiên. Bạn không cần học thuộc -- chỉ cần biết nó nằm ở đâu.
