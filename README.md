# Aunomay Legal

**Tra cứu pháp luật Việt Nam cho Claude, có căn cứ rõ ràng.**
*Vietnamese legal research for Claude, with verified citations.*

Aunomay Legal kết nối Claude với kho văn bản pháp luật Việt Nam được lưu toàn văn, chia theo Phần, Chương, Mục, Điều, kèm tình trạng hiệu lực và đường link về nguồn chính thức. Plugin này bổ sung bộ kỹ năng hướng dẫn Claude đọc đúng Điều, kiểm tra hiệu lực trước khi dẫn, rồi mới trả lời, soạn hay rà soát hợp đồng.

*Aunomay Legal gives Claude full-text Vietnamese legal documents with validity status and source links, plus skills that make Claude read and verify before citing.*

## Dùng trên Claude.ai, Claude Desktop, ứng dụng di động

1. Vào **Settings → Connectors** → **Add custom connector**.
2. Nhập URL: `https://legal.aunomay.com/mcp`
3. Bấm **Connect**, đăng nhập bằng email và mã 6 số được gửi tới email.
4. Bật connector Aunomay Legal trong cuộc trò chuyện và đặt câu hỏi.

*On Claude.ai / Desktop / mobile: Settings → Connectors → Add custom connector → paste the URL → sign in with the emailed code.*

## Cài trong Claude Code

```
/plugin marketplace add aunomay/legal-claude-plugin
/plugin install aunomay-legal@aunomay-legal
```

Lần đầu Claude gọi công cụ, trình duyệt sẽ mở để đăng nhập (hoặc gõ `/mcp` → `aunomay-legal` → Authenticate).

Chỉ cần máy chủ MCP, không cần kỹ năng:
```
claude mcp add --transport http aunomay-legal https://legal.aunomay.com/mcp
```

## Công cụ / Tools

| Công cụ | Chức năng |
|---|---|
| `search_legal_docs` | Tìm văn bản theo từ khóa, lọc theo loại (Luật, Bộ luật, Nghị định, Thông tư, Nghị quyết) và hiệu lực; trả về văn bản kèm các Điều khớp nhất |
| `get_document` | Đọc nguyên văn các Điều cần thiết (vd `"385,400-405"`) hoặc cả văn bản theo trang; tra theo id hoặc số hiệu như `91/2015/QH13` |
| `get_summary` | Thông tin văn bản và mục lục Phần/Chương/Mục/Điều |
| `check_compliance` | Với một câu hỏi tuân thủ, trả về các đoạn Điều liên quan nhất trên toàn kho hoặc trong một văn bản, có trích dẫn đầy đủ |
| `get_laws` | Danh mục văn bản đang có trong kho, lọc theo lĩnh vực và hiệu lực |
| `get_account_status` | Gói đang dùng, số lượt đã dùng hôm nay, còn lại, giờ đặt lại |

## Kỹ năng / Skills

| Kỹ năng | Dùng khi |
|---|---|
| `tra-cuu-phap-luat` | Mọi câu hỏi pháp luật: quy trình kiểm chứng, mẫu trả lời có căn cứ, cách tính thuế/BHXH từng bước |
| `soan-hop-dong` | Soạn hợp đồng: tra nội dung bắt buộc, hình thức, mức giới hạn trước, mỗi điều khoản có ghi chú căn cứ |
| `phan-tich-hop-dong` | Rà soát hợp đồng có sẵn: bảng điều khoản, rủi ro, căn cứ, đề xuất sửa |
| `doi-chieu-tuan-thu` | So quy trình, chính sách nội bộ với luật; checklist theo mức rủi ro kèm bằng chứng cần lưu |
| `trinh-bay-va-dinh-dang` | Xuất kết quả thành báo cáo Word (.docx) đúng quy cách tiếng Việt |
| `ban-quyen-sang-tao` | Bản quyền cho người làm nội dung, nội dung AI, chính sách YouTube |
| `setup` | Kết nối, đăng nhập, hạn mức, xử lý lỗi |

## Câu hỏi mẫu / Example questions

- Tính thuế thu nhập cá nhân năm 2026 cho lương 35 triệu, 1 người phụ thuộc.
- Tính bảo hiểm xã hội một lần sau 8 năm đóng.
- Hộ kinh doanh hay công ty — so sánh thuế phải nộp theo doanh thu 3 tỷ đồng/năm.
- Xây nhà không phép, sai phép bị phạt bao nhiêu, có bị tháo dỡ không?
- Ly hôn rồi, người trực tiếp nuôi con có được tự ý đưa con ra nước ngoài không?
- Thuế thu nhập doanh nghiệp cho doanh nghiệp nhỏ và vừa hiện nay là bao nhiêu?
- Ở nhà ông bà 60 năm, giờ muốn đứng tên sổ một mình thì cần điều kiện gì?
- Doanh nghiệp nhỏ có được miễn đánh giá tác động xử lý dữ liệu cá nhân không?

## Hạn mức / Quota

- **Gói miễn phí:** 20 lượt tra cứu mỗi ngày, đặt lại lúc 00:00 giờ Việt Nam (UTC+7).
- Lượt tra không có kết quả **không** bị tính.
- **Gói trả phí:** không giới hạn — liên hệ Aunomay qua support@aunomay.com.
- Xem số lượt còn lại: hỏi Claude "tôi còn bao nhiêu lượt Aunomay Legal?" (công cụ `get_account_status`).

*Free: 20 lookups/day, reset at midnight Vietnam time; empty results are free; paid plan is unlimited.*

## Nguồn dữ liệu / Data source

Văn bản được lấy từ các cổng thông tin chính thức của Nhà nước, chủ yếu là Cơ sở dữ liệu quốc gia về pháp luật (vbpl.vn). Mỗi văn bản lưu số hiệu, ngày ban hành, ngày hiệu lực, tình trạng (Còn hiệu lực / Hết hiệu lực một phần / Hết hiệu lực toàn bộ / Chưa có hiệu lực) và đường link về trang nguồn. Kho ban đầu gồm khoảng 100 văn bản cốt lõi (bộ luật, luật, nghị định quan trọng) và đang được bổ sung. Khi kho chưa có văn bản cần thiết, kỹ năng hướng dẫn Claude đọc trực tiếp trên cổng chính thức và ghi rõ điều đó.

*Texts come from official Vietnamese state portals; each answer links back to the source.*

## Miễn trừ trách nhiệm / Disclaimer

Aunomay Legal giúp bạn tìm và đọc văn bản pháp luật nhanh hơn; đây không phải dịch vụ tư vấn pháp lý và không tạo ra quan hệ luật sư – khách hàng. Câu trả lời do AI tổng hợp nên có thể thiếu sót hoặc sai, kể cả khi có trích dẫn. Hãy mở đường link để đối chiếu văn bản gốc, và trao đổi với luật sư hoặc cơ quan có thẩm quyền trước khi đưa ra quyết định có hậu quả lớn.

*Aunomay Legal is a research tool, not legal advice. AI output can be wrong; check the linked source and consult a lawyer before important decisions.*

## Liên kết / Links

- Trang chủ: https://legal.aunomay.com
- Quyền riêng tư: https://legal.aunomay.com/privacy
- Điều khoản sử dụng: https://legal.aunomay.com/terms
- Hỗ trợ: support@aunomay.com

## Bản quyền / Licence

Copyright (c) 2026 Aunomay. All rights reserved. Xem [LICENSE](LICENSE).
