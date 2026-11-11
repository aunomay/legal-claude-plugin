---
name: phan-tich-hop-dong
description: Rà soát, phân tích một hợp đồng hoặc điều khoản có sẵn theo pháp luật Việt Nam — tìm điều khoản bất lợi, mập mờ, trái luật hoặc có thể vô hiệu, vượt mức trần phạt vi phạm, thiếu nội dung bắt buộc, sai hình thức (công chứng, đăng ký), rủi ro thuế và lao động trá hình. Dùng khi người dùng gửi file, ảnh hoặc dán nội dung hợp đồng (thuê nhà, mua bán, dịch vụ, lao động, đặt cọc, hợp tác, KOL/quảng cáo, MCN, NDA, điều khoản sử dụng) và hỏi "có gì bất lợi không", "ký được không", "điều này có hợp pháp không", "review this contract". Kết quả là bảng Điều khoản | Rủi ro | Căn cứ | Đề xuất sửa.
---

# Phân tích hợp đồng

English: review an existing contract clause by clause; every "unlawful / void / over the cap" finding cites an article read in full.

Dựa trên skill `tra-cuu-phap-luat`. Phân biệt rõ:
- **Trái luật / có thể vô hiệu** → bắt buộc có Điều/Khoản đã đọc.
- **Bất lợi nhưng hợp pháp** → ghi "ý kiến thương mại", không gắn căn cứ giả.

## Bước 1 — Đọc hợp đồng và dựng hồ sơ
1. Đọc toàn bộ (cả phụ lục, điều khoản dẫn chiếu). Ảnh/scan khó đọc → nói phần nào không đọc được.
2. Ghi: loại hợp đồng, các bên, tư cách và thẩm quyền ký, ngày ký, ngày hiệu lực, giá trị, luật áp dụng, cơ quan giải quyết tranh chấp.
3. Hỏi người dùng là bên nào và mục tiêu (ký ngay, đàm phán lại, đã ký và đang tranh chấp).
4. Luật áp dụng là luật có hiệu lực **tại ngày giao kết** (và điều khoản chuyển tiếp nếu có).

## Bước 2 — Tra khung pháp lý
1. `check_compliance {question: "<loại hợp đồng> nội dung bắt buộc, hình thức, phạt vi phạm, đơn phương chấm dứt", limit: 15}`.
2. `search_legal_docs` cho từng vấn đề lớn phát hiện khi đọc (vd `"lãi suất chậm thanh toán"`, `"tiền đặt cọc"`, `"thời gian thử việc"`).
3. `get_document {doc: "...", articles: "..."}` — đọc nguyên văn mọi Điều sẽ dẫn. Gom nhiều Điều trong một lệnh để tiết kiệm lượt.
4. Hợp đồng ký trước một luật mới → tìm cả văn bản cũ với `in_force_only: false`.

## Bước 3 — Rà theo nhóm điều khoản
Với mỗi nhóm: hợp đồng nói gì → luật nói gì → đánh giá → đề xuất.

1. **Chủ thể và thẩm quyền ký** — người ký có quyền đại diện? Giấy ủy quyền? Tài sản chung vợ chồng cần cả hai ký?
2. **Đối tượng, phạm vi, nghiệm thu** — mô tả có đo được không; ai quyết định "đạt"; thời hạn phản hồi.
3. **Giá, thanh toán, thuế** — trước/sau thuế, hóa đơn, ai khấu trừ TNCN, thời hạn, lãi chậm trả (so với giới hạn luật).
4. **Phạt vi phạm, bồi thường, giới hạn trách nhiệm** — có thỏa thuận phạt không; mức có vượt trần của luật chuyên ngành áp dụng không; giới hạn trách nhiệm một chiều.
5. **Đặt cọc, bảo đảm** — xử lý cọc khi mỗi bên vi phạm có khớp luật không.
6. **Sở hữu trí tuệ** — chuyển nhượng hay chỉ cho phép sử dụng; phạm vi, lãnh thổ, thời hạn; quyền nhân thân; thiếu nội dung bắt buộc của hợp đồng chuyển quyền.
7. **Độc quyền, không cạnh tranh, bảo mật** — phạm vi, thời hạn; với người lao động thì đối chiếu Bộ luật Lao động.
8. **Chấm dứt** — điều kiện đơn phương chấm dứt, báo trước, hậu quả; điều khoản cho một bên chấm dứt tùy ý.
9. **Dữ liệu cá nhân** — thu thập, chia sẻ dữ liệu có căn cứ và sự đồng ý không.
10. **Hình thức** — có cần công chứng/chứng thực/đăng ký mà chưa làm không; hậu quả.
11. **Tranh chấp, luật áp dụng** — trọng tài có thỏa thuận hợp lệ không; tòa án nước ngoài; ngôn ngữ ưu tiên.
12. **Dấu hiệu quan hệ lao động trá hình** — "cộng tác viên", "khoán việc" nhưng có trả lương định kỳ, chịu quản lý, điều hành.

## Bước 4 — Kết quả
### 4.1. Tóm tắt (3–5 dòng)
Đánh giá chung, 3–5 điểm phải đàm phán trước khi ký, điểm nào có thể làm hợp đồng (hoặc một phần) vô hiệu.

### 4.2. Bảng rủi ro
| # | Điều khoản trong hợp đồng | Rủi ro | Mức | Căn cứ pháp lý | Đề xuất câu chữ |
|---|---|---|---|---|---|
| 1 | Điều 8.2 — phạt 30% giá trị | Có thể vượt mức trần nếu là hợp đồng thương mại | Cao | Luật …, số …, Điều … (Còn hiệu lực) — link | "Bên vi phạm chịu phạt … % giá trị phần nghĩa vụ bị vi phạm" |
| 2 | Điều 5 — thanh toán "sau khi nghiệm thu" | Không có thời hạn nghiệm thu | Trung bình | Ý kiến thương mại | "Trong 05 ngày làm việc kể từ …" |

Mức: **Cao** (trái luật, có thể vô hiệu, rủi ro tài chính lớn) / **Trung bình** (mập mờ, dễ tranh chấp) / **Thấp** (nên cải thiện).

### 4.3. Nội dung còn thiếu
Liệt kê nội dung bắt buộc chưa có, kèm Điều yêu cầu.

### 4.4. Chưa xác minh và miễn trừ
Theo mẫu của `tra-cuu-phap-luat`. Với hợp đồng giá trị lớn, độc quyền dài hạn, bất động sản: khuyên nhờ luật sư xem bản cuối.

## Ví dụ
Người dùng dán hợp đồng thuê nhà có điều "bên thuê trả nhà trước hạn mất toàn bộ tiền cọc và phạt thêm 3 tháng tiền nhà".
1. `check_compliance {question: "đặt cọc trong hợp đồng thuê nhà, đơn phương chấm dứt hợp đồng thuê nhà ở, phạt vi phạm"}`.
2. `get_document` Điều về đặt cọc, phạt vi phạm, chấm dứt hợp đồng thuê (Bộ luật Dân sự; Luật Nhà ở nếu là nhà ở).
3. Đánh giá: hợp pháp nếu các bên tự thỏa thuận và không có luật chuyên ngành giới hạn? → nêu căn cứ; nếu chỉ là bất lợi → "ý kiến thương mại", đề xuất giảm.

Không ký, gửi, chấp nhận điều khoản thay người dùng. Xuất báo cáo Word: skill `trinh-bay-va-dinh-dang`.
