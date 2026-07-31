# Đề xuất công cụ

*Cập nhật: 2026-07-30*

> ⚠️ **Đọc phần này với tinh thần cảnh giác.** Đây là **đề xuất**, không phải hướng
> dẫn. Thị trường công cụ AI coding thay đổi theo tuần: giá đổi, free tier co lại,
> tính năng mới xuất hiện, sản phẩm bị mua lại hoặc đóng cửa. Vì vậy trang này
> **không nêu giá, không nêu hạn mức free tier, không nêu tên menu**. Trước khi
> chọn, hãy vào trang chủ của công cụ và tự kiểm chứng.
>
> Cuốn sách này cố tình dạy **nguyên lý** thay vì thao tác trên một công cụ cụ thể,
> để phần bạn học không hết hạn cùng với phần mềm.

## Cách chọn quan trọng hơn chọn cái gì

Trước khi so sánh sản phẩm, trả lời bốn câu này. Câu trả lời của bạn sẽ loại bỏ
phần lớn lựa chọn nhanh hơn bất kỳ bảng so sánh nào.

**1. Bạn muốn kết quả hay muốn hiểu?**
Nếu mục tiêu là có một app dùng được cuối tuần này, chọn nhóm dựng-app-từ-prompt.
Nếu mục tiêu là hiểu code để lâu dài tự chủ, chọn nhóm AI IDE — chậm hơn nhưng bạn
thấy được từng file.

**2. Dữ liệu của bạn có nhạy cảm không?**
Nếu đang làm với dữ liệu nội bộ công ty, câu hỏi đầu tiên không phải "công cụ nào
mạnh nhất" mà là "công cụ này gửi code của tôi đi đâu, có dùng để train model không,
công ty tôi đã duyệt chưa". Hỏi bộ phận IT/Security trước khi hỏi cộng đồng.

**3. Bạn có sẵn sàng đọc code không?**
Trả lời thật. Nếu không, đừng chọn công cụ đòi bạn phải mở terminal — bạn sẽ bỏ
giữa đường. Chọn thứ có giao diện, rồi nâng cấp sau.

**4. Bạn cần làm một lần hay làm lặp lại?**
Một lần thì công cụ nào cũng được. Làm lặp lại thì hãy ưu tiên công cụ cho phép
lưu **rules file** (xem Chương 6) — vì đó là thứ giúp bạn không phải nhắc lại cùng
một yêu cầu mỗi lần.

## Bốn nhóm công cụ

Đừng nhớ tên sản phẩm — hãy nhớ **nhóm**. Sản phẩm sẽ đổi, nhóm thì bền hơn.

**Nhóm 1 — Dựng app từ prompt, chạy trên trình duyệt.**
Bạn mô tả bằng lời, công cụ sinh ra app chạy được kèm hosting. Nhanh nhất để có
kết quả nhìn thấy được, phù hợp prototype và validate ý tưởng. Đổi lại: bạn ít kiểm
soát chi tiết, và khi app lớn lên thì hay bị nghẽn.
*Ví dụ hiện có: Lovable, Bolt.new, v0, Replit, Firebase Studio.*

**Nhóm 2 — AI IDE, chạy trên máy bạn.**
Là code editor có AI tích hợp sâu. Bạn thấy toàn bộ file, sửa được từng dòng, chạy
được project thật. Cần cài đặt và cần chịu được việc nhìn thấy code.
*Ví dụ hiện có: Cursor, Windsurf, VS Code kèm extension AI.*

**Nhóm 3 — Agentic CLI, chạy trong terminal.**
AI tự đọc project, tự sửa nhiều file, tự chạy lệnh kiểm tra. Mạnh nhất cho việc
lặp lại và cho project đã có sẵn, nhưng đòi bạn quen dòng lệnh. Đây cũng là nhóm
mà kỹ năng ở Chương 18 (agentic workflows) phát huy nhiều nhất.
*Ví dụ hiện có: Claude Code, Codex CLI, Gemini CLI.*

**Nhóm 4 — Chat AI thuần.**
Không sinh app, chỉ trả lời. Nhưng đây là nơi tốt nhất để **hỏi hiểu**: "đoạn code
này làm gì", "lỗi này nghĩa là gì", "cách nào an toàn hơn". Đừng bỏ qua nhóm này
chỉ vì nó không tự build được app.
*Ví dụ hiện có: Claude, ChatGPT, Gemini.*

## Lộ trình đề xuất cho người mới

Không cần chọn đúng ngay từ đầu. Thứ tự này giảm rủi ro bỏ cuộc:

1. **Tuần đầu:** một công cụ nhóm 1 + một chat AI nhóm 4. Mục tiêu là *nhìn thấy
   thứ mình mô tả biến thành app thật* — cảm giác này quan trọng hơn việc chọn
   đúng công cụ.
2. **Sau khi đã dựng được 2–3 thứ:** thêm một công cụ nhóm 2, đọc thử code mà nhóm 1
   đã sinh ra. Đây là lúc kiến thức Phần 3 của sách bắt đầu có ích.
3. **Khi thấy mình lặp lại cùng một loại việc:** chuyển sang nhóm 3 và viết rules file.

## Một lưu ý về chi phí

Trang này không nêu giá, nhưng nêu một nguyên tắc: **mọi công cụ AI coding đều có
cách để bạn tiêu nhiều tiền hơn dự định**, thường qua việc gọi model mạnh cho việc
nhỏ, hoặc qua dịch vụ backend tính theo lượng dùng. Trước khi dùng thật cho việc
công ty, hãy tìm phần đặt hạn mức chi tiêu (spending limit) và bật nó lên. Chương 12
nói kỹ hơn về việc này.

---

*Trang này nằm ngoài phần nội dung chính của sách nên được cập nhật độc lập. Nếu
bạn thấy thông tin đã lỗi thời, hãy mở một Issue trên repo.*
