# Templates

Ba file mẫu dùng được luôn, trích từ nội dung sách. Cấp phép **MIT** — copy vào dự án
của bạn thoải mái, kể cả dự án thương mại.

| File | Dùng khi nào | Chương liên quan |
|---|---|---|
| [prd-template.md](prd-template.md) | Trước khi bắt đầu bất kỳ project nào — mô tả cho AI hiểu bạn muốn gì | Chương 5 |
| [rules-file-template.md](rules-file-template.md) | Sau khi chọn tech stack — để không phải nhắc lại cùng một yêu cầu mỗi lần | Chương 6 |
| [gitignore-template.txt](gitignore-template.txt) | Ngay khi tạo repo — tuyến phòng thủ đầu tiên chống lộ secrets | Chương 12, 13 |

## Cách dùng

**PRD** — copy `prd-template.md`, điền vào các chỗ `[trong ngoặc vuông]`, rồi đưa cả
file cho AI trước khi yêu cầu build. Phần `## 8. Out of scope` quan trọng ngang phần
liệt kê tính năng: nó ngăn AI tự ý thêm thứ bạn không muốn.

**Rules file** — nơi lưu tùy theo công cụ bạn dùng. Nguyên tắc chung: file này là
"văn hóa làm việc" mà AI tự tuân theo, bạn không phải nhắc lại. Giữ nó **cụ thể** —
"mỗi function không quá 20 dòng" hiệu quả, còn "viết code sạch" thì vô ích vì AI
không biết "sạch" là thế nào.

**`.gitignore`** — đổi tên thành `.gitignore` (có dấu chấm đầu) và đặt ở thư mục gốc
dự án. Làm việc này **trước** commit đầu tiên. Một khi secret đã push lên GitHub, kể
cả repo private, coi như đã lộ — không có cách undo nào an toàn.

> ⚠️ Template rules file có nêu tên vài công cụ và phiên bản framework. Đó là ví dụ
> tại thời điểm viết, không phải khuyến nghị cố định — hãy sửa cho khớp stack thật
> của bạn.
