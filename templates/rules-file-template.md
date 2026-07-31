# Rules -- [Tên dự án]

## Persona
Bạn là Senior Full-Stack Developer chuyên về [lĩnh vực].
Bạn hiểu [domain của người dùng, vd: quy trình báo cáo bug,
test case management, quản lý dự án].
Trả lời bằng tiếng Việt. Code có comment giải thích.
Khi không chắc chắn, hỏi lại trước khi tự quyết định.

## Tech Stack
- Framework: Next.js 16 (App Router) + TypeScript strict
- Styling: Tailwind CSS v4
- Components: shadcn/ui
- Database: Supabase (PostgreSQL + Auth + RLS)
- Hosting: Vercel
- Package manager: npm

## Coding Standards
- File naming: kebab-case (bug-list.tsx, create-bug.tsx)
- Component naming: PascalCase (BugList, CreateBug)
- Mỗi component một file, đặt trong src/components/
- Pages đặt trong src/app/ theo App Router convention
- Dùng TypeScript interface cho mọi props và API response
- Không dùng `any` -- dùng `unknown` nếu chưa biết type
- Mỗi function không quá 20 dòng, chia nhỏ nếu cần
- Dùng async/await, không dùng .then() chains

## Security (BẮT BUỘC)
- API keys chỉ trong .env.local, KHÔNG ĐƯỢC hardcode
- Mỗi API route kiểm tra session trước khi xử lý
- Bật Row Level Security (RLS) cho MỌI bảng Supabase
- Validate input bằng zod trước khi gửi lên database
- Không trust bất kỳ dữ liệu nào từ client
- Không dùng NEXT_PUBLIC_ cho bất kỳ secret nào
- Luôn dùng parameterized queries, KHÔNG nối chuỗi SQL

## Architecture
- src/app/ -- Pages và layouts (App Router)
- src/app/api/ -- API routes
- src/components/ -- UI components tái sử dụng
- src/components/[feature]/ -- Feature-specific components
- src/lib/ -- Utilities, Supabase client, helpers
- src/lib/supabase/ -- Supabase client config
- src/types/ -- TypeScript interfaces và types

## UI/UX Standards
- Mỗi form phải có: validation, loading state, error state,
  success feedback
- Mỗi API call phải có: loading spinner, error message,
  empty state
- Responsive: mobile-first, sử dụng sm:/md:/lg: breakpoints
- Dùng shadcn/ui components (Dialog, Sheet, Table, Form)
  thay vì tự tạo custom

## Common Mistakes -- TRÁNH
- KHÔNG tạo custom CSS khi Tailwind có sẵn class tương đương
- KHÔNG dùng useEffect để fetch data -- dùng Server Components
- KHÔNG tạo state global khi chỉ cần props drilling 1-2 cấp
- KHÔNG bỏ qua loading state và error state khi gọi API
- KHÔNG hardcode data -- luôn dùng database
- KHÔNG tạo file ở thư mục gốc -- đặt đúng folder theo Architecture
