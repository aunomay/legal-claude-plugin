---
name: setup
description: Cài đặt, kết nối và xử lý sự cố Aunomay Legal — thêm máy chủ MCP vào Claude.ai, Claude Desktop, ứng dụng di động hoặc Claude Code; đăng nhập bằng email và mã 6 số; lỗi "Unauthorized", 401, token hết hạn, "needs authentication"; hết lượt tra cứu, "quota exceeded", "đã dùng hết 20 lượt"; máy chủ không phản hồi, timeout, lỗi 5xx; công cụ Aunomay Legal không xuất hiện. Dùng khi người dùng hỏi "cài Aunomay Legal thế nào", "kết nối không được", "bị đăng xuất", "còn bao nhiêu lượt", "khi nào reset", "nâng cấp gói", "how to connect / sign in / quota", hoặc khi một công cụ aunomay-legal trả về lỗi.
---

# Cài đặt và xử lý sự cố Aunomay Legal

English: connect, sign in, check quota and recover from errors.

Thông tin chung:
- Địa chỉ máy chủ MCP: `https://legal.aunomay.com/mcp` (HTTP, OAuth tự đăng ký client).
- Đăng nhập: email + mã 6 số gửi qua email. Không cần mật khẩu. Claude **không bao giờ** hỏi, nhận hay nhập mã thay người dùng — người dùng tự nhập trong cửa sổ trình duyệt.
- Gói miễn phí: 20 lượt tra cứu/ngày, đặt lại lúc 00:00 giờ Việt Nam (UTC+7); lượt tra không có kết quả không bị tính. Gói trả phí: không giới hạn — liên hệ Aunomay (support@aunomay.com).
- Trang chủ, trạng thái: https://legal.aunomay.com

## 1. Kết nối lần đầu

### Claude.ai (web), Claude Desktop, ứng dụng di động
1. Mở **Settings → Connectors** (Cài đặt → Trình kết nối).
2. Chọn **Add custom connector**.
3. Đặt tên `Aunomay Legal`, URL: `https://legal.aunomay.com/mcp`, lưu.
4. Bấm **Connect** → trình duyệt mở trang đăng nhập Aunomay Legal → nhập email → nhập mã 6 số nhận qua email.
5. Trong cuộc trò chuyện, bật connector Aunomay Legal (biểu tượng công cụ) nếu nó chưa bật.
Connector thêm trên web dùng được cả trên Desktop và di động cùng tài khoản. Gói Team/Enterprise có thể cần quản trị viên cho phép custom connector.

### Claude Code
Cách 1 — cài plugin (có sẵn kỹ năng):
```
/plugin marketplace add aunomay/legal-claude-plugin
/plugin install aunomay-legal@aunomay-legal
```
Cách 2 — chỉ thêm máy chủ MCP:
```
claude mcp add --transport http aunomay-legal https://legal.aunomay.com/mcp
```
Sau đó gõ `/mcp`, chọn `aunomay-legal` → **Authenticate** → đăng nhập trong trình duyệt. Hoặc gọi một công cụ bất kỳ, lần đầu sẽ mở trình duyệt.

### Kiểm tra đã kết nối
Gọi `get_account_status {}` → thấy gói, số lượt đã dùng hôm nay, còn lại, giờ đặt lại. Trả lời người dùng ngắn gọn bằng các số đó.

## 2. Bảng xử lý sự cố

| Triệu chứng | Nguyên nhân thường gặp | Cách xử lý |
|---|---|---|
| Không thấy công cụ `search_legal_docs`… | Connector chưa bật / plugin chưa cài / chưa xác thực | Claude.ai: bật connector trong cuộc trò chuyện. Claude Code: `/mcp` xem trạng thái `aunomay-legal`; `/plugin` kiểm tra plugin đã bật; khởi động lại phiên |
| `Unauthorized`, 401, "needs authentication", token hết hạn | Phiên đăng nhập hết hạn hoặc bị thu hồi | Claude Code: `/mcp` → `aunomay-legal` → **Authenticate** lại (hoặc Clear authentication rồi Authenticate). Claude.ai: Settings → Connectors → Aunomay Legal → Disconnect → Connect lại |
| Không nhận được mã 6 số | Email vào thư rác, gõ sai email, mã hết hạn | Kiểm tra Spam/Promotions, gửi lại mã, kiểm tra chính tả email. Vẫn không có → support@aunomay.com |
| Trình duyệt không tự mở (Claude Code) | Môi trường không có trình duyệt / SSH | Copy đường link mà Claude Code in ra, mở trên máy có trình duyệt |
| Hết lượt / quota exceeded | Đã dùng 20 lượt của gói miễn phí hôm nay | Gọi `get_account_status` để báo số lượt và giờ đặt lại (00:00 giờ Việt Nam). Gợi ý: chờ đến giờ đặt lại, hoặc liên hệ Aunomay về gói trả phí. Trong lúc chờ có thể tra trên nguồn chính thức (mục 3) và nói rõ nguồn |
| Timeout, 502/503/504, không kết nối được | Máy chủ bảo trì hoặc sự cố mạng | Thử lại một lần sau ít phút; xem https://legal.aunomay.com; vẫn lỗi → chuyển sang nguồn chính thức (mục 3) và báo người dùng |
| Kết quả rỗng | Kho chưa có văn bản hoặc từ khóa chưa hợp | Không phải lỗi, lượt này không bị tính. Đổi từ khóa, thử `in_force_only: false`, `get_laws` theo lĩnh vực; xem skill `tra-cuu-phap-luat` Bước 4–5 |

Nguyên tắc: **lỗi kỹ thuật không phải là câu trả lời pháp lý.** Không kết luận "luật không quy định" vì công cụ lỗi hoặc hết lượt.

## 3. Khi không dùng được Aunomay Legal
Tra trực tiếp nguồn nhà nước (WebSearch/WebFetch; nếu bị chặn thì mở bằng trình duyệt, chỉ đọc):
- https://vbpl.vn — Cơ sở dữ liệu quốc gia về pháp luật
- https://congbao.chinhphu.vn — Công báo
- https://vanban.chinhphu.vn — Hệ thống văn bản Chính phủ
- https://quochoi.vn — Quốc hội
Ghi rõ trong câu trả lời: "Aunomay Legal tạm thời không dùng được; căn cứ dưới đây đọc trực tiếp tại …".

## 4. Quyền riêng tư và điều khoản
- Câu hỏi tra cứu được gửi tới máy chủ Aunomay Legal. Khuyên người dùng không đưa thông tin định danh không cần thiết (số CCCD, số tài khoản) vào câu hỏi.
- Chính sách quyền riêng tư: https://legal.aunomay.com/privacy
- Điều khoản sử dụng: https://legal.aunomay.com/terms
- Hỗ trợ: support@aunomay.com

## 5. Mẫu trả lời nhanh
**"Tôi còn bao nhiêu lượt?"** → `get_account_status {}` → "Gói <plan>: đã dùng <x>/20 lượt hôm nay, còn <y>. Lượt sẽ đặt lại lúc 00:00 giờ Việt Nam (<thời điểm reset>). Lượt tra không có kết quả không bị tính."

**Lỗi 401 giữa chừng (Claude Code)** → "Phiên đăng nhập Aunomay Legal đã hết hạn. Bạn gõ `/mcp`, chọn `aunomay-legal` rồi chọn Authenticate để đăng nhập lại bằng email và mã 6 số; xong báo tôi để tra tiếp."
