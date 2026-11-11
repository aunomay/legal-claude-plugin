---
name: doi-chieu-tuan-thu
description: Đối chiếu quy trình, chính sách, quy chế nội bộ hoặc hoạt động thực tế của doanh nghiệp với một văn bản pháp luật Việt Nam và lập checklist tuân thủ — bảo vệ dữ liệu cá nhân (đánh giá tác động, đồng ý, chuyển dữ liệu ra nước ngoài), lao động (nội quy, thỏa ước, làm thêm giờ), thuế và hóa đơn, quảng cáo, thương mại điện tử, an ninh mạng, phòng cháy, môi trường, kinh doanh có điều kiện. Dùng khi người dùng hỏi "công ty tôi đã tuân thủ … chưa", "cần làm gì để đúng luật …", "doanh nghiệp nhỏ có được miễn … không", "gap analysis", "compliance checklist", hoặc gửi một chính sách nội bộ để kiểm tra. Kết quả là checklist nhóm theo mức rủi ro cao/trung bình/thấp, mỗi mục có Điều/Khoản và bằng chứng cần lưu.
---

# Đối chiếu tuân thủ

English: gap analysis between an internal process or policy and a Vietnamese legal document, output as a risk-grouped checklist with article citations and evidence to keep.

Dựa trên skill `tra-cuu-phap-luat` (đọc nguyên văn, kiểm tra hiệu lực, dẫn nguồn).

## Bước 1 — Khoanh phạm vi
- Doanh nghiệp: loại hình, quy mô (siêu nhỏ, nhỏ, vừa — tiêu chí do văn bản quy định, cần tra), ngành nghề, số lao động, có yếu tố nước ngoài không.
- Đối tượng đối chiếu: tài liệu nội bộ (chính sách, quy trình, mẫu biểu, hợp đồng mẫu) hoặc mô tả hoạt động thực tế.
- Văn bản pháp luật đối chiếu: người dùng chỉ định, hoặc tự xác định ở Bước 2.
- Thời điểm: đánh giá theo luật hiện hành, đồng thời ghi văn bản **chưa có hiệu lực** sắp áp dụng để chuẩn bị.

## Bước 2 — Xác định văn bản và nghĩa vụ
1. `search_legal_docs {query: "<lĩnh vực> nghĩa vụ doanh nghiệp", limit: 10}`; với `doc_type: "Nghị định"` và `"Thông tư"` để lấy văn bản hướng dẫn.
2. `get_summary {doc: "<văn bản chính>"}` — chọn các Chương/Điều đặt nghĩa vụ cho đối tượng của người dùng.
3. `get_document {doc: "...", articles: "..."}` — đọc nguyên văn từng Điều nghĩa vụ, Điều về **đối tượng áp dụng**, **trường hợp miễn/giảm/lộ trình** và **điều khoản chuyển tiếp**.
4. `check_compliance {question: "<mô tả hoạt động cụ thể của người dùng>", doc: "<số hiệu>"}` để không bỏ sót Điều liên quan; chạy thêm một lần không có `doc` để thấy văn bản khác có liên quan.
5. Mức phạt khi vi phạm: tìm nghị định xử phạt của lĩnh vực, đọc Điều tương ứng (cá nhân/tổ chức).

Câu hỏi "doanh nghiệp nhỏ có được miễn … không": tìm cả (a) Điều quy định miễn/hoãn trong văn bản chuyên ngành, (b) tiêu chí xác định doanh nghiệp nhỏ và vừa trong văn bản tương ứng, (c) ngoại lệ của ngoại lệ (vd ngành nghề hoặc loại dữ liệu không được miễn), (d) thời hạn của ưu đãi.

## Bước 3 — Tách nghĩa vụ thành yêu cầu kiểm tra được
Mỗi nghĩa vụ trong luật → một hoặc vài mục checklist dạng "Doanh nghiệp đã/có …?". Ví dụ:
- Luật: "Bên kiểm soát dữ liệu phải lập hồ sơ đánh giá tác động…" → Mục: "Đã lập hồ sơ đánh giá tác động cho từng hoạt động xử lý? Đã gửi/lưu theo quy định?"

## Bước 4 — Đối chiếu với tài liệu nội bộ
Với mỗi mục: tìm trong tài liệu của người dùng đoạn đáp ứng (trích số mục), đánh giá **Đạt / Một phần / Chưa đạt / Không áp dụng / Chưa đủ thông tin**.

Mức rủi ro:
- **Cao** — nghĩa vụ bắt buộc chưa đáp ứng, có chế tài phạt tiền đáng kể, đình chỉ, hoặc ảnh hưởng quyền của người khác (dữ liệu, lao động, an toàn).
- **Trung bình** — đáp ứng một phần, hồ sơ thiếu, quy trình có nhưng không có bằng chứng thực hiện.
- **Thấp** — thủ tục, hình thức, khuyến nghị thực hành tốt (ghi rõ "khuyến nghị", không phải nghĩa vụ).

## Bước 5 — Kết quả

### 5.1. Tóm tắt
Phạm vi, văn bản đối chiếu (số hiệu, hiệu lực), số mục Đạt / Một phần / Chưa đạt; 3 việc cần làm trước.

### 5.2. Checklist theo mức rủi ro

**Rủi ro cao**
| # | Yêu cầu | Căn cứ (văn bản, Điều, Khoản) | Hiện trạng | Đánh giá | Việc cần làm | Bằng chứng cần lưu |
|---|---|---|---|---|---|---|
| C1 | … | Luật …, số …, Điều … khoản … — link | Chính sách mục 3.2 chưa nêu … | Chưa đạt | … | Biên bản, hồ sơ, log, văn bản đồng ý… |

**Rủi ro trung bình** — cùng cấu trúc, đánh số T1, T2…

**Rủi ro thấp** — cùng cấu trúc, đánh số L1, L2…

### 5.3. Mức chế tài tham khảo
Chỉ ghi các mức đã đọc trong nghị định xử phạt: hành vi → Điều → mức cho cá nhân/tổ chức → biện pháp khắc phục.

### 5.4. Văn bản sắp có hiệu lực
Liệt kê thay đổi đã biết (status "Chưa có hiệu lực") và ngày áp dụng.

### 5.5. Chưa xác minh và miễn trừ
Theo mẫu `tra-cuu-phap-luat`. Nhắc: checklist dựa trên tài liệu được cung cấp, không thay cho kiểm toán tuân thủ hay ý kiến pháp lý chính thức.

## Ví dụ
"Công ty 30 nhân viên bán hàng online, có danh sách khách hàng. Có phải đánh giá tác động xử lý dữ liệu cá nhân không?"
1. `search_legal_docs {query: "đánh giá tác động xử lý dữ liệu cá nhân"}` → văn bản luật và nghị định hướng dẫn về bảo vệ dữ liệu cá nhân.
2. `get_document` Điều về hồ sơ đánh giá tác động, Điều về miễn/hoãn cho doanh nghiệp nhỏ, khởi nghiệp, Điều chuyển tiếp.
3. `search_legal_docs {query: "tiêu chí xác định doanh nghiệp nhỏ và vừa số lao động doanh thu"}` → xác định công ty có thuộc diện nhỏ không.
4. Checklist: thông báo xử lý dữ liệu, sự đồng ý, hồ sơ đánh giá tác động (hoặc căn cứ miễn), người phụ trách, xử lý vi phạm, chuyển dữ liệu ra nước ngoài.

Xuất báo cáo Word: skill `trinh-bay-va-dinh-dang`.
