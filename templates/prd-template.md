# PRD: [Tên ứng dụng]

## 1. Mục tiêu
[1-2 câu mô tả app làm gì và giải quyết vấn đề gì.]

Ví dụ: "Ứng dụng quản lý bug nội bộ giúp team QA 10 người
báo cáo, theo dõi, và quản lý lỗi phần mềm một cách hiệu quả,
thay thế quy trình báo cáo bằng email/spreadsheet hiện tại."

## 2. Đối tượng sử dụng
- Ai dùng: [mô tả người dùng cụ thể]
- Số lượng dự kiến: [bao nhiêu người]
- Trình độ kỹ thuật: [không biết code / biết cơ bản / developer]

## 3. Vai trò người dùng (User roles)
| Vai trò | Quyền hạn |
|---------|----------|
| [Role 1] | [có thể làm gì] |
| [Role 2] | [có thể làm gì] |

Ví dụ:
| Vai trò | Quyền hạn |
|---------|----------|
| QA Engineer | Tạo bug, sửa bug của mình, đổi status, xem tất cả bug |
| Team Lead | Tất cả quyền của QA + assign bug, xóa bug, xem dashboard |

## 4. Tính năng chính (Key features)

### 4.1 [Tên tính năng 1]
- Mô tả: [tính năng này làm gì]
- Acceptance criteria:
  - [Tiêu chí 1: mô tả cụ thể, có thể kiểm tra được]
  - [Tiêu chí 2]
  - [Tiêu chí 3]

### 4.2 [Tên tính năng 2]
- Mô tả: [tính năng này làm gì]
- Acceptance criteria:
  - [Tiêu chí 1]
  - [Tiêu chí 2]

### 4.3 [Tên tính năng 3]
[tương tự]

## 5. Màn hình chính (Screens)
1. [Màn hình 1]: [mô tả ngắn -- có những thành phần gì]
2. [Màn hình 2]: [mô tả ngắn]
3. [Màn hình 3]: [mô tả ngắn]
4. [Màn hình 4]: [mô tả ngắn]

## 6. Data requirements

### Bảng [tên bảng 1]
| Cột | Kiểu | Bắt buộc | Mô tả |
|-----|------|---------|------|
| id | uuid | có | khóa chính, tự động tạo |
| [tên cột] | [kiểu] | [có/không] | [giải thích] |
| created_at | timestamp | có | ngày tạo, tự động |
| updated_at | timestamp | có | ngày cập nhật cuối |

### Bảng [tên bảng 2]
| Cột | Kiểu | Bắt buộc | Mô tả |
|-----|------|---------|------|
| id | uuid | có | khóa chính |
| [tên cột] | [kiểu] | [có/không] | [giải thích] |

### Quan hệ giữa các bảng
- [Bảng A] (1) -> (nhiều) [Bảng B] qua trường [tên trường]
- [Bảng C] (nhiều) <-> (nhiều) [Bảng D] qua bảng trung gian [tên]

## 7. Tech stack
- Frontend: Next.js, Tailwind CSS, shadcn/ui
- Backend: Supabase (PostgreSQL + Auth + Storage)
- Hosting: Vercel
- Version control: Git + GitHub

## 8. Out of scope (KHÔNG làm trong phiên bản này)
- [Thứ 1 không làm và lý do]
- [Thứ 2 không làm]
- [Thứ 3 không làm]

## 9. Edge cases cần xử lý
- [Edge case 1 và cách xử lý mong muốn]
- [Edge case 2 và cách xử lý]
- [Edge case 3 và cách xử lý]
- [Edge case 4 và cách xử lý]
- [Edge case 5 và cách xử lý]
