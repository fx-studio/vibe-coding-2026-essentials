# Phụ lục A: Thư viện 30 prompt mẫu

Ở Chương 4 bạn đã học năm quy tắc vàng để viết prompt hiệu quả. Phụ lục này gom lại 30 prompt sẵn sàng dùng, tổ chức theo năm giai đoạn của quy trình vibe coding mà Chương 3 đã trình bày: Define, Scaffold, Build, Debug và Ship.

Hãy nghĩ phụ lục này như một tủ đựng dụng cụ. Bạn không cần đọc từ đầu đến cuối, mà mở ra khi cần, tìm đúng prompt cho tình huống, tùy chỉnh cho project của mình, rồi dùng ngay. Mỗi prompt đã áp dụng các quy tắc từ Chương 4: cung cấp đủ context, mô tả "tại sao" trước "cái gì", và yêu cầu AI lên kế hoạch trước khi code.

Các prompt dưới đây được viết trung lập với công cụ. Chúng mô tả *ý định* của bạn, không gắn với một AI IDE hay một dịch vụ cụ thể nào — nhờ vậy chúng không lỗi thời khi công cụ đổi giao diện hay đổi tên. Chỗ nào cần một loại công cụ (ví dụ "công cụ dựng app từ prompt", "nền tảng hosting"), prompt gọi theo loại chứ không nêu tên sản phẩm.

> 💡 **Tip:** Cách dùng tốt nhất: copy prompt, thay các phần trong [ngoặc vuông] thành thông tin cụ thể của project bạn, rồi dán vào AI. Theo thời gian, bạn sẽ tùy chỉnh chúng thành thư viện prompt cá nhân — giống như developer có snippet library, vibe coder có prompt library.

> 🧰 **Đề xuất công cụ:** *Tính đến 2026-07.* Các prompt này chạy được với hầu hết AI IDE và công cụ dựng app từ prompt phổ biến. Tên sản phẩm cụ thể và tính năng của chúng đổi rất nhanh, nên phụ lục không nêu tên — xem trang [Đề xuất công cụ](../de-xuat-cong-cu.md) để có danh sách được cập nhật và tự kiểm chứng trước khi chọn.

---

## Nhóm 1: PRD và Planning (Prompt 1–5)

Giai đoạn Define là quan trọng nhất trong quy trình vibe coding (Chương 3, Chương 5). Những prompt sau giúp bạn xác định rõ ràng sản phẩm trước khi viết bất kỳ dòng code nào.

### Prompt 1 — Tạo PRD từ ý tưởng

**Khi nào dùng:** Khi bạn có ý tưởng nhưng chưa biết bắt đầu từ đâu.

```text
Bạn là Senior Product Manager. Tôi muốn xây dựng [mô tả app].
Đối tượng sử dụng là [ai]. Vấn đề họ gặp là [vấn đề gì].

Hãy viết Product Requirements Document (PRD) bao gồm:
1. Problem statement (1 đoạn)
2. User personas (2-3 người dùng điển hình)
3. Core features (tối đa 5 tính năng cho MVP)
4. User stories với acceptance criteria
5. Data structure (bảng nào, cột nào, quan hệ nào)
6. Out of scope (những gì KHÔNG làm)

Lưu ý: đây là MVP, chỉ những tính năng thiết yếu nhất.
```

**Kết quả mong đợi:** Một PRD có cấu trúc, đủ chi tiết để bắt đầu build, đủ tinh gọn để không bị scope creep.

### Prompt 2 — Review và phản biện PRD

**Khi nào dùng:** Sau khi có PRD (tự viết hoặc AI tạo), cần một góc nhìn phản biện.

```text
Đây là PRD của tôi cho [tên app]:
[Dán PRD vào đây]

Hãy đóng vai một Tech Lead khác tính với 10 năm kinh nghiệm.
Phân tích PRD này và chỉ ra:
1. Assumptions sai hoặc thiếu cơ sở
2. Edge cases chưa được xử lý
3. Rủi ro kỹ thuật với tech stack Next.js + Supabase
4. Tính năng nào nên bỏ khỏi MVP
5. Tính năng nào còn thiếu mà quan trọng
6. Lỗi bảo mật tiềm ẩn

Đừng ngại nói thẳng. Phát hiện vấn đề bây giờ tốt hơn
là khi đã code xong.
```

**Kết quả mong đợi:** Danh sách các điểm cần sửa trong PRD trước khi bắt đầu code.

### Prompt 3 — Thiết kế database schema

**Khi nào dùng:** Sau khi có PRD, trước khi tạo project.

```text
Dựa trên PRD sau, hãy thiết kế database schema cho Supabase:
[Dán PRD hoặc mô tả core features]

Yêu cầu:
- Dùng PostgreSQL syntax
- Mỗi bảng có id (UUID), created_at, updated_at
- Xác định rõ primary key, foreign key, relationships
- Gợi ý indexes cho các cột thường được filter/search
- Viết Row Level Security (RLS) policies cho từng bảng
- Thêm comments giải thích mục đích từng bảng và cột

Trả về SQL để chạy trực tiếp trên Supabase.
```

**Kết quả mong đợi:** SQL script sẵn sàng chạy trên database.

### Prompt 4 — Tạo user flow diagram

**Khi nào dùng:** Khi cần hình dung trải nghiệm người dùng trước khi build.

```text
Dựa trên các user stories sau:
[Dán user stories]

Hãy tạo user flow bằng text diagram cho từng story:
- Bắt đầu từ đâu (trang nào?)
- Người dùng thực hiện hành động gì?
- Hệ thống phản hồi gì?
- Các trường hợp lỗi: người dùng nhập sai, mất mạng, chưa đăng nhập
- Kết thúc ở đâu?

Dùng format: [Trang] -> (Hành động) -> [Kết quả]
```

**Kết quả mong đợi:** User flow dạng text, dễ hiểu, dễ chuyển thành wireframe.

### Prompt 5 — Xác định tech stack cho project cụ thể

**Khi nào dùng:** Khi không chắc stack mặc định (Next.js + Supabase + một nền tảng hosting) có phù hợp.

```text
Tôi muốn xây dựng [mô tả app] với các yêu cầu:
- Đối tượng sử dụng: [ai, bao nhiêu người]
- Tính năng đặc biệt: [realtime, file upload, payment...]
- Ngân sách: [free / X mỗi tháng]
- Trình độ kỹ thuật: [người mới / có kinh nghiệm vibe coding]

So sánh 2-3 tech stack phù hợp, mỗi stack gồm:
Framework, Database, Auth, Deploy, và lý do chọn.
Chỉ ra stack nào bạn khuyến nghị và tại sao.
```

**Kết quả mong đợi:** Bảng so sánh tech stack với khuyến nghị cụ thể.

---

## Nhóm 2: Scaffolding (Prompt 6–10)

Giai đoạn Scaffold tạo khung project ban đầu. Những prompt này đảm bảo project khởi đầu đúng cách.

### Prompt 6 — Khởi tạo project đầy đủ

**Khi nào dùng:** Bắt đầu project mới trong AI IDE của bạn.

```text
Tạo project Next.js với TypeScript, Tailwind CSS,
và shadcn/ui. Cấu trúc thư mục:
- app/ với layout.tsx có navbar responsive
- components/ với thư mục ui/ cho shadcn
- lib/ với supabase client config
- types/ với các type chính từ PRD

Cài đặt shadcn/ui components: Button, Card, Input,
Dialog, Table, Badge, Dropdown Menu.

File .env.example với các biến cần thiết (không điền giá trị).
File .gitignore đầy đủ.

Chạy được ngay với "npm run dev", không lỗi.
```

**Kết quả mong đợi:** Project chạy được ngay, cấu trúc sạch, sẵn sàng build features.

### Prompt 7 — Tạo rules file cho project

**Khi nào dùng:** Ngay sau khi khởi tạo project, trước khi build features.

```text
Tạo rules file cho project [tên project] với nội dung:

1. Persona: Bạn là Senior Full-stack Developer chuyên Next.js + Supabase
2. Tech stack: Next.js, TypeScript, Tailwind CSS, shadcn/ui, Supabase
3. Coding standards:
   - TypeScript strict mode, không dùng any
   - Server Components mặc định, "use client" chỉ khi cần hooks
   - Tailwind classes, không inline styles
   - Components nhỏ, mỗi file dưới 150 dòng
4. Security: luôn validate input với Zod, dùng parameterized queries,
   không hardcode secrets
5. Naming: camelCase cho biến/hàm, PascalCase cho components,
   kebab-case cho file

Lưu rules file vào đúng vị trí quy ước của công cụ AI bạn dùng
(mỗi công cụ có một vị trí riêng cho file này).
```

**Kết quả mong đợi:** Rules file hoàn chỉnh, áp dụng tự động cho mọi phiên làm việc.

> 📋 **Dành cho PM/BA:** Rules file giống như "Definition of Done" trong Scrum — nó đảm bảo mọi thành viên trong nhóm (kể cả AI) tuân thủ cùng một tiêu chuẩn. Xem Chương 6 để hiểu thêm.

### Prompt 8 — Tạo layout và navigation

**Khi nào dùng:** Sau khi scaffold xong, cần layout chính cho app.

```text
Tạo layout chính cho app [tên app] với:
- Navbar responsive: logo bên trái, menu links giữa,
  user avatar/login button bên phải
- Sidebar (nếu cần): danh mục chính, có thể collapse
- Main content area với max-width và padding phù hợp
- Footer đơn giản
- Mobile: hamburger menu, sidebar biến thành bottom sheet
- Dark mode toggle

Dùng shadcn/ui components. Responsive với Tailwind breakpoints.
Trạng thái đăng nhập/chưa đăng nhập khác nhau trên navbar.
```

**Kết quả mong đợi:** Layout hoàn chỉnh, responsive, có dark mode.

### Prompt 9 — Kết nối Supabase ban đầu

**Khi nào dùng:** Khi cần setup kết nối database cho project.

```text
Setup kết nối Supabase cho project Next.js này:

1. Tạo file lib/supabase/client.ts (client-side)
2. Tạo file lib/supabase/server.ts (server-side)
3. Tạo file lib/supabase/middleware.ts cho auth
4. Cập nhật middleware.ts ở root để check auth
5. Tạo type từ database schema

Dùng thư viện tích hợp Supabase chính thức cho Server Components
(tránh thư viện auth-helpers đã bị deprecated).
Đảm bảo cookies được xử lý đúng cho Server Components.
Biến môi trường: NEXT_PUBLIC_SUPABASE_URL và
NEXT_PUBLIC_SUPABASE_ANON_KEY.
```

**Kết quả mong đợi:** Supabase client sẵn sàng dùng cho cả client và server components.

### Prompt 10 — Tạo data seed cho development

**Khi nào dùng:** Khi cần dữ liệu mẫu để test trong quá trình build.

```text
Tạo SQL seed data cho database schema sau:
[Dán schema hoặc mô tả các bảng]

Yêu cầu:
- 10-20 rows mỗi bảng với dữ liệu thực tế (không lorem ipsum)
- Dữ liệu phải có quan hệ hợp lệ giữa các bảng
- Bao gồm cả edge cases: trường trống, giá trị dài, ký tự đặc biệt
- Viết dạng SQL INSERT chạy trực tiếp trên Supabase
- Thêm comment giải thích mỗi nhóm dữ liệu

Dữ liệu theo ngữ cảnh [tiếng Việt / tiếng Anh / cả hai].
```

**Kết quả mong đợi:** Script SQL tạo dữ liệu mẫu hoàn chỉnh, sẵn sàng test.

---

## Nhóm 3: UI và Frontend (Prompt 11–16)

Giai đoạn Build chiếm 60% thời gian (Chương 3). Những prompt frontend sau giúp bạn tạo giao diện chuyên nghiệp.

### Prompt 11 — Tạo form phức tạp

**Khi nào dùng:** Khi cần form nhập liệu có validation.

```text
Tạo form [tên form] với các trường:
[Liệt kê trường: tên, kiểu dữ liệu, bắt buộc/không]

Yêu cầu:
- Dùng shadcn/ui Form component với React Hook Form
- Validation bằng Zod: [liệt kê quy tắc validation]
- Hiển thị lỗi dưới mỗi trường khi validation fail
- Loading state khi submit (disable button, hiện spinner)
- Success/error toast sau khi submit
- Responsive: 1 cột trên mobile, 2 cột trên desktop

Không submit trực tiếp lên database — tạo hàm onSubmit
nhận FormData, tôi sẽ kết nối sau.
```

**Kết quả mong đợi:** Form hoàn chỉnh với validation, UX tốt, sẵn sàng kết nối backend.

### Prompt 12 — Tạo bảng dữ liệu với filter và sort

**Khi nào dùng:** Khi cần hiển thị danh sách dữ liệu dạng bảng.

```text
Tạo data table hiển thị [loại dữ liệu] với:
- Các cột: [liệt kê cột và kiểu dữ liệu]
- Search box tìm kiếm theo [trường nào]
- Filter dropdown theo [trường nào]
- Sort theo [cột nào], mặc định [thứ tự nào]
- Pagination: 10 items/trang, hiện số trang
- Row actions: [Edit, Delete, View...]
- Empty state khi không có dữ liệu
- Loading skeleton khi đang fetch

Dùng shadcn/ui Table. Responsive: trên mobile chuyển
thành card list thay vì bảng ngang.
```

**Kết quả mong đợi:** Bảng dữ liệu chuyên nghiệp với đầy đủ tính năng filter, sort, pagination.

### Prompt 13 — Tạo dashboard với KPI cards và charts

**Khi nào dùng:** Khi cần trang tổng quan hiển thị số liệu.

```text
Tạo dashboard page cho [tên app] với:

1. KPI Cards (hàng trên cùng): [liệt kê 3-4 chỉ số]
   - Mỗi card: icon, số, label, % thay đổi so với kỳ trước
2. Chart area: [loại biểu đồ: bar/line/pie] hiển thị [dữ liệu gì]
   - Dùng một thư viện chart cho React, responsive, có tooltip khi hover
3. Recent activity list: 5-10 items gần nhất
4. Quick actions: [1-2 nút hành động nhanh]

Dùng dữ liệu mock trước. Tôi sẽ kết nối API sau.
Layout grid responsive: mobile 1 cột, desktop 2-3 cột.
```

**Kết quả mong đợi:** Dashboard page đẹp, responsive, sẵn sàng kết nối dữ liệu thật.

### Prompt 14 — Tạo detail page với tabs

**Khi nào dùng:** Khi cần trang chi tiết cho một item (bug, task, project...).

```text
Tạo detail page cho [loại item] với:
- Header: tên item, status badge, action buttons (Edit, Delete)
- Tabs: [liệt kê các tab, ví dụ: Overview, Comments, History]
- Tab Overview: hiển thị tất cả thông tin chính dạng read-only
- Tab Comments: danh sách comment + form thêm comment mới
- Tab History: activity log theo thời gian (timeline)
- Back button để quay lại danh sách
- Loading state khi fetch dữ liệu

Dùng dynamic route [id]. Fetch dữ liệu trong Server Component.
Client Components chỉ cho phần interactive (tabs, forms).
```

**Kết quả mong đợi:** Detail page chuyên nghiệp với tabs, sẵn sàng kết nối dữ liệu.

### Prompt 15 — Cải thiện UI/UX hiện tại

**Khi nào dùng:** Khi app đã chạy nhưng giao diện chưa đẹp hoặc UX chưa tốt.

```text
Đây là code của component [tên component]:
[Dán code]

Hãy cải thiện UI/UX:
1. Spacing và alignment nhất quán
2. Color contrast đủ WCAG AA
3. Hover/focus states cho mọi element tương tác
4. Transition/animation nhẹ (không quá mức)
5. Empty states, loading states, error states
6. Responsive cho mobile

Giữ nguyên logic và functionality. Chỉ thay đổi phần visual.
Giải thích từng thay đổi và lý do.
```

**Kết quả mong đợi:** Component đẹp hơn, UX tốt hơn, với giải thích để học.

### Prompt 16 — Tạo responsive mobile layout

**Khi nào dùng:** Khi cần tối ưu giao diện cho mobile.

```text
Component này hiển thị tốt trên desktop nhưng chưa tốt trên mobile:
[Dán code]

Hãy sửa để responsive theo mobile-first approach:
- Mobile (< 640px): [mô tả layout mobile mong muốn]
- Tablet (640-1024px): [mô tả layout tablet]
- Desktop (> 1024px): giữ nguyên như hiện tại

Dùng Tailwind breakpoints (sm:, md:, lg:).
Touch targets tối thiểu 44x44px cho mobile.
Font size phù hợp cho từng breakpoint.
```

**Kết quả mong đợi:** Component responsive, UX tốt trên mọi kích thước màn hình.

---

## Nhóm 4: Backend và Database (Prompt 17–21)

### Prompt 17 — Tạo API route CRUD

**Khi nào dùng:** Khi cần tạo API cho một resource (users, bugs, tasks...).

```text
Tạo API routes cho resource [tên] trong Next.js App Router:

1. GET /api/[tên] -- lấy danh sách (có pagination, filter, sort)
2. POST /api/[tên] -- tạo mới (validate input với Zod)
3. GET /api/[tên]/[id] -- lấy chi tiết
4. PUT /api/[tên]/[id] -- cập nhật
5. DELETE /api/[tên]/[id] -- xóa (soft delete)

Yêu cầu:
- Dùng Supabase server client
- Kiểm tra authentication
- Validate input trước khi xử lý
- Trả về JSON nhất quán: { data, error, message }
- HTTP status codes chính xác
- Try-catch với error handling rõ ràng
```

**Kết quả mong đợi:** CRUD API hoàn chỉnh, bảo mật, sẵn sàng dùng cho frontend.

### Prompt 18 — Tạo authentication flow

**Khi nào dùng:** Khi cần thêm đăng nhập/đăng ký vào app.

```text
Implement authentication flow hoàn chỉnh với Supabase Auth:

1. Trang /login: form email + password, nút đăng nhập bằng
   nhà cung cấp OAuth (Google, GitHub...)
2. Trang /signup: form đăng ký với email verification
3. Middleware kiểm tra auth cho tất cả route /dashboard/*
4. Redirect chưa login -> /login, đã login -> /dashboard
5. Hiển thị user info trên navbar (avatar, tên)
6. Nút logout
7. Trang /forgot-password

Dùng Supabase Auth, không tự viết cơ chế auth riêng.
Handle edge cases: email đã tồn tại, password yếu, token hết hạn.
```

**Kết quả mong đợi:** Auth flow hoàn chỉnh, xử lý lỗi tốt, an toàn.

> 🔒 **Bảo mật:** Luôn yêu cầu AI check Row Level Security khi tạo API. Một API không có RLS giống như nhà không có khóa cửa — ai cũng vào được. Xem Chương 16 để hiểu sâu hơn về bảo mật.

### Prompt 19 — Viết RLS policies

**Khi nào dùng:** Sau khi tạo bảng trong Supabase, trước khi build features.

```text
Viết Row Level Security (RLS) policies cho bảng [tên bảng]
trong Supabase:

Cấu trúc bảng:
[Dán schema hoặc mô tả cột]

Quy tắc truy cập:
- Users chỉ được đọc dữ liệu của mình (user_id = auth.uid())
- Users chỉ được tạo dữ liệu mới với user_id là chính mình
- Users chỉ được sửa dữ liệu của mình
- Admin (role = 'admin') được đọc/sửa tất cả
- Dữ liệu public (ví dụ: [trường nào]) ai cũng đọc được

Trả về SQL để chạy trực tiếp trên Supabase.
Thêm comment giải thích từng policy.
```

**Kết quả mong đợi:** RLS policies bảo mật, giải thích rõ ràng.

### Prompt 20 — Tối ưu database query

**Khi nào dùng:** Khi trang load chậm hoặc có nhiều API calls.

```text
Đây là query hiện tại của tôi:
[Dán code query/API]

Trang này mất [X giây] để load. Hãy tối ưu:
1. Giảm số lượng queries (dùng join thay vì nhiều select)
2. Chỉ select các cột cần thiết (không select *)
3. Thêm index cho cột được filter/sort thường xuyên
4. Dùng pagination thay vì load tất cả
5. Cache kết quả nếu phù hợp

Giải thích từng thay đổi và dự kiến cải thiện bao nhiêu.
```

**Kết quả mong đợi:** Query nhanh hơn, code sạch hơn, với giải thích.

### Prompt 21 — Tạo file upload

**Khi nào dùng:** Khi cần tính năng upload ảnh, file đính kèm.

```text
Implement file upload cho [mục đích: avatar, attachment...]:

1. Component upload: drag-and-drop + click to browse
2. Validation: max [X]MB, chỉ cho phép [.jpg, .png, .pdf...]
3. Upload lên kho lưu trữ file của Supabase, bucket "[tên bucket]"
4. Hiển thị progress bar khi upload
5. Preview trước khi upload (với ảnh)
6. Lưu URL vào database sau khi upload thành công
7. Xóa file cũ khi upload file mới (nếu là avatar)

Storage policy: chỉ user đã đăng nhập được upload,
ai cũng đọc được files public.
```

**Kết quả mong đợi:** File upload hoàn chỉnh với UX tốt và bảo mật.

---

## Nhóm 5: Debugging (Prompt 22–25)

Giai đoạn Debug chiếm 15% thời gian (Chương 3). Những prompt này giúp bạn sửa lỗi hiệu quả hơn.

### Prompt 22 — Debug lỗi có error message

**Khi nào dùng:** Khi gặp lỗi và có error message cụ thể. Đây là prompt quan trọng nhất trong nhóm debug.

```text
Tôi gặp lỗi này:

Error: [Dán NGUYÊN VĂN error message, không tóm tắt]

Code gây lỗi (file [tên file]):
[Dán code liên quan]

Hành vi mong đợi: [Mô tả app nên làm gì]
Hành vi thực tế: [Mô tả đang xảy ra]
Đã thử: [Liệt kê những gì đã thử mà không được]

Hãy:
1. Giải thích lỗi này nghĩa là gì (bằng ngôn ngữ đơn giản)
2. Chỉ ra nguyên nhân gốc (root cause)
3. Đưa ra cách fix cụ thể
4. Giải thích tại sao cách fix này hoạt động
```

**Kết quả mong đợi:** Hiểu được lỗi, fix được lỗi, và học được điều mới.

> 🧪 **Dành cho Tester/QA:** Format prompt debug này giống hệt báo cáo bug của QA: Steps to Reproduce (code), Expected Result, Actual Result, và Environment info. Kinh nghiệm viết bug report của bạn là lợi thế lớn khi debug — xem Chương 14 để thực hành thêm.

### Prompt 23 — Debug lỗi không có error message

**Khi nào dùng:** Khi app không báo lỗi nhưng hành vi sai (UI không cập nhật, data không lưu...).

```text
App không báo lỗi nhưng hoạt động sai:

Mong đợi: [Mô tả hành vi đúng]
Thực tế: [Mô tả hành vi sai]

Các file liên quan:
File 1 - [tên file]:
[Dán code]

File 2 - [tên file]:
[Dán code]

Thông tin thêm:
- Console có hiện gì: [có/không, nếu có thì gì]
- Network tab có request fail: [có/không]
- Lỗi xảy ra khi nào: [luôn luôn / chỉ khi...]

Hãy phân tích và tìm nguyên nhân.
```

**Kết quả mong đợi:** Tìm được lỗi "ẩn" và cách fix.

### Prompt 24 — Fix lỗi deployment

**Khi nào dùng:** Khi app chạy tốt trên localhost nhưng lỗi khi đưa lên nền tảng hosting.

```text
App chạy tốt trên localhost nhưng lỗi khi deploy lên nền tảng hosting.

Build log:
[Dán build log, chỉ phần error]

Các file liên quan:
- next.config.js: [Dán code]
- package.json (scripts và dependencies): [Dán code]
- .env.local (chỉ tên biến, KHÔNG có giá trị): [Liệt kê]

Environment variables đã set trên nền tảng hosting: [Liệt kê tên biến]

Hãy phân tích và fix lỗi deploy.
Lưu ý: không thay đổi gì không liên quan đến lỗi deploy.
```

**Kết quả mong đợi:** App deploy thành công, hiểu được sự khác biệt giữa local và production.

### Prompt 25 — Thoát vòng xoáy debug

**Khi nào dùng:** Khi đã debug quá ba vòng mà vẫn không fix được (quy tắc ba vòng, Chương 14).

```text
Tôi đang mắc kẹt trong vòng xoáy debug. Đã thử [X] lần
mà vẫn không fix được. Đây là tình hình:

Vấn đề ban đầu: [Mô tả]
Fix đã thử và kết quả:
1. [Thử gì] -> [Kết quả]
2. [Thử gì] -> [Kết quả]
3. [Thử gì] -> [Kết quả]

Code hiện tại (đã bị sửa nhiều lần):
[Dán code]

Hãy:
1. Dừng lại, KHÔNG fix tiếp trên code này
2. Phân tích nguyên nhân gốc sai ở đâu
3. Đề xuất approach hoàn toàn mới
4. Nếu cần, gợi ý revert về commit [hash] và làm lại từ đầu
```

**Kết quả mong đợi:** Thoát khỏi vòng xoáy, có approach mới hiệu quả hơn.

---

## Nhóm 6: Security (Prompt 26–27)

### Prompt 26 — Security audit toàn diện

**Khi nào dùng:** Trước khi deploy hoặc sau khi build xong MVP.

```text
Hãy thực hiện security audit cho project này theo
SHIELD Framework (Chương 16):

[Dán code các file quan trọng: middleware, API routes,
Supabase config, .env.example]

Kiểm tra 6 lớp:
S - Separation: AI có truy cập production không?
H - Human in the Loop: có review process không?
I - Input Validation: mọi input có được validate không?
E - Environment: env vars, HTTPS, CORS đúng chưa?
L - Logging: có security logging không?
D - Defense in Depth: dependencies có lỗi không?

Với mỗi lỗi tìm thấy: mô tả, mức độ nghiêm trọng
(Critical/High/Medium/Low), và cách fix cụ thể.
```

**Kết quả mong đợi:** Danh sách lỗi bảo mật xếp theo độ nghiêm trọng với cách fix.

### Prompt 27 — Fix lỗi bảo mật cụ thể

**Khi nào dùng:** Khi biết có lỗi bảo mật cần fix.

```text
Project của tôi có lỗi bảo mật: [mô tả lỗi, ví dụ:
API endpoint không check auth, SQL injection risk...]

Code hiện tại:
[Dán code có lỗi]

Hãy:
1. Giải thích rủi ro cụ thể (attacker có thể làm gì)
2. Fix lỗi với code cụ thể
3. Thêm test case để đảm bảo lỗi không tái xuất
4. Kiểm tra có lỗi tương tự ở file khác trong project không
```

**Kết quả mong đợi:** Lỗi được fix, hiểu được rủi ro, có test case phòng ngừa.

---

## Nhóm 7: Deployment (Prompt 28–29)

### Prompt 28 — Setup deployment pipeline

**Khi nào dùng:** Khi muốn tự động hóa quá trình deploy.

```text
Setup deployment pipeline cho project Next.js + Supabase
trên một nền tảng hosting:

1. Cấu hình project: framework, build command, env vars
2. Kết nối với repo: auto deploy khi push nhánh chính
3. Preview deployments cho mỗi branch/PR
4. Environment variables: chia riêng Development/Preview/Production
5. Redirect rules (nếu cần)
6. Headers: security headers (CSP, HSTS...)

Giải thích nguyên lý từng bước (không cần thao tác bấm nút
cụ thể, vì mỗi nền tảng có giao diện khác nhau).
```

**Kết quả mong đợi:** Pipeline hoàn chỉnh, deploy tự động, an toàn.

### Prompt 29 — Chuẩn bị app cho production

**Khi nào dùng:** Khi app đã test xong, sẵn sàng cho người dùng thật.

```text
App của tôi đã test xong trên preview, sẵn sàng production.
Hãy tạo production checklist:

1. Performance: các trang load dưới 3 giây không?
2. SEO: meta tags, Open Graph, sitemap
3. Security: HTTPS, headers, env vars không lộ
4. Error handling: 404 page, error boundary, offline state
5. Analytics: setup một dịch vụ analytics
6. Monitoring: làm sao biết khi app gặp lỗi?
7. Backup: database có được backup không?

Với mỗi mục, cho biết trạng thái (Done/Todo) và
code cụ thể để implement nếu chưa làm.
```

**Kết quả mong đợi:** Checklist đầy đủ, app sẵn sàng cho production.

---

## Nhóm 8: Testing (Prompt 30)

### Prompt 30 — Tạo test cases toàn diện

**Khi nào dùng:** Sau khi build xong một feature, trước khi chuyển sang feature tiếp theo.

```text
Hãy viết test cases cho feature [tên feature]:

Chức năng: [Mô tả chức năng]
User roles: [Admin, User, Guest...]

Tạo bảng test cases bao gồm:
1. Happy path: 3-5 kịch bản chính
2. Edge cases: 3-5 trường hợp biên
3. Error states: 3-5 kịch bản lỗi
4. Security: 2-3 kiểm tra bảo mật (RBAC, injection...)

Mỗi test case gồm: ID, Mô tả, Steps, Input, Expected Result.

Bonus: viết 2-3 test script tự động cho happy path
quan trọng nhất (ví dụ bằng Playwright).
```

**Kết quả mong đợi:** Bộ test cases đầy đủ, sẵn sàng test thủ công và tự động.

> 🧪 **Dành cho Tester/QA:** Prompt này là "vũ khí" của bạn. Kết hợp kinh nghiệm QA với AI để tạo test cases nhanh gấp nhiều lần. Xem Chương 15 để hiểu thêm về tư duy test case cho vibe coding.

---

## Cách dùng hiệu quả thư viện prompt này

Thư viện 30 prompt trên bao phủ toàn bộ quy trình xây dựng ứng dụng. Có vài điều quan trọng cần nhớ khi dùng.

Thứ nhất, **đừng copy nguyên văn mà không tùy chỉnh**. Phần trong [ngoặc vuông] là chỗ bạn điền thông tin cụ thể. Càng cụ thể, AI càng cho kết quả tốt. Prompt "Tạo form đăng ký" sẽ cho kết quả kém hơn prompt "Tạo form đăng ký nhân viên với 8 trường bao gồm họ tên, email, phòng ban (dropdown), và ngày bắt đầu làm việc".

Thứ hai, **kết hợp nhiều prompt theo trình tự**. Một dự án thực tế sẽ dùng Prompt 1 (PRD) trước, rồi Prompt 3 (database), rồi Prompt 6 (scaffold), rồi Prompt 11–14 (UI), rồi Prompt 17–18 (backend), rồi Prompt 26 (security), và cuối cùng Prompt 29 (production). Trình tự này phản ánh đúng năm giai đoạn của Chương 3.

Thứ ba, **lưu lại và cải tiến**. Khi một prompt cho kết quả tốt, lưu vào file `my-prompts.md` trong project. Khi kết quả chưa tốt, hãy sửa và thử lại. Theo thời gian, bạn sẽ có thư viện prompt cá nhân hiệu quả hơn bất kỳ template nào.

> 📋 **Dành cho PM/BA:** Nếu bạn quản lý nhóm, hãy tạo thư viện prompt chung cho team. Giống như team có coding standards và Definition of Done, có "Prompt Standards" giúp mọi người tạo ra kết quả nhất quán. Đây là một trong những trách nhiệm mới của Vibe PM (Chương 19).

## Tổng kết

| Nhóm | Số lượng | Giai đoạn |
|------|----------|-----------|
| PRD và Planning | 5 prompt | Define |
| Scaffolding | 5 prompt | Scaffold |
| UI và Frontend | 6 prompt | Build |
| Backend và Database | 5 prompt | Build |
| Debugging | 4 prompt | Debug |
| Security | 2 prompt | Trước Ship |
| Deployment | 2 prompt | Ship |
| Testing | 1 prompt | Mọi giai đoạn |
| **Tổng** | **30 prompt** | |

Hãy quay lại Chương 4 để ôn lại năm quy tắc vàng trước khi dùng các prompt này. Và nhớ: prompt tốt nhất là prompt bạn tự viết, dựa trên kinh nghiệm của chính mình.
