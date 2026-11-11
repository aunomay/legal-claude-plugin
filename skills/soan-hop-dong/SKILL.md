---
name: soan-hop-dong
description: Soạn hợp đồng theo pháp luật Việt Nam — hợp đồng dịch vụ, mua bán hàng hóa, thuê nhà, thuê tài sản, vay, đặt cọc, hợp tác kinh doanh, hợp đồng lao động, thuê khoán, cộng tác viên, chuyển nhượng hoặc cho phép sử dụng quyền tác giả, quảng cáo/KOL, bảo mật (NDA), phụ lục hợp đồng, biên bản thanh lý. Dùng khi người dùng nói "soạn giúp hợp đồng", "làm mẫu hợp đồng", "viết điều khoản phạt", "hợp đồng này cần những gì", "draft a contract under Vietnamese law". Tra trước nội dung bắt buộc, hình thức (văn bản, công chứng, chứng thực, đăng ký), mức trần phạt vi phạm theo luật chuyên ngành, rồi mới soạn, mỗi điều khoản có ghi chú căn cứ.
---

# Soạn hợp đồng có căn cứ

English: draft Vietnamese contracts only after looking up the mandatory contents, form requirements and legal caps; every clause carries a note with its legal basis.

Dựa trên skill `tra-cuu-phap-luat` (quy tắc cứng, kiểm tra hiệu lực, mẫu dẫn nguồn). Không ghi bất kỳ "mức tối đa", "bắt buộc công chứng", "phải có nội dung…" nào chưa đọc được trong văn bản ở lượt này.

## Bước 1 — Thu thập thông tin (hỏi gọn một lần)
- Loại giao dịch và đối tượng (hàng hóa, dịch vụ, tài sản, quyền sử dụng đất, nhà ở, quyền tác giả, sức lao động).
- Các bên: cá nhân / hộ kinh doanh / doanh nghiệp / tổ chức nước ngoài; người ký và thẩm quyền ký.
- Giá trị, phương thức và thời hạn thanh toán; có VAT không; ai khấu trừ thuế TNCN.
- Thời hạn, địa điểm thực hiện, tiêu chí nghiệm thu.
- Bên người dùng là bên nào (để cân bằng hoặc bảo vệ lợi ích bên đó — nói rõ nghiêng về ai).
- Ngôn ngữ (Việt, song ngữ), luật áp dụng, cách giải quyết tranh chấp (tòa án, trọng tài).
Thiếu thông tin không quan trọng → điền chỗ trống `[...]` thay vì hỏi.

## Bước 2 — Xác định khung pháp lý
| Quan hệ | Văn bản thường điều chỉnh (tra để xác nhận số hiệu, hiệu lực) |
|---|---|
| Hợp đồng dân sự nói chung | Bộ luật Dân sự (phần hợp đồng, các hợp đồng thông dụng) |
| Giữa thương nhân, mục đích sinh lợi | Luật Thương mại (phạt vi phạm, bồi thường, mua bán hàng hóa, dịch vụ) |
| Lao động | Bộ luật Lao động — nếu thực chất là việc làm có trả lương và chịu quản lý thì là hợp đồng lao động dù đặt tên khác |
| Nhà ở, đất đai, kinh doanh bất động sản | Luật Nhà ở, Luật Đất đai, Luật Kinh doanh bất động sản |
| Quyền tác giả, quyền liên quan | Luật Sở hữu trí tuệ và nghị định hướng dẫn |
| Quảng cáo | Luật Quảng cáo và nghị định hướng dẫn |
| Có dữ liệu cá nhân | Luật Bảo vệ dữ liệu cá nhân và nghị định hướng dẫn |

Gọi:
1. `search_legal_docs {query: "<loại hợp đồng> nội dung hợp đồng", limit: 10}`.
2. `check_compliance {question: "hợp đồng <loại> phải có những nội dung gì, có phải công chứng không, mức phạt vi phạm tối đa", limit: 15}`.
3. `get_summary` cho văn bản chính để chọn Điều.

## Bước 3 — Tra bốn nhóm yêu cầu bắt buộc (đọc nguyên văn bằng `get_document`)
1. **Nội dung bắt buộc / nội dung chủ yếu.** Vd hợp đồng chuyển nhượng quyền tác giả, hợp đồng lao động, hợp đồng mua bán nhà có danh sách nội dung luật yêu cầu. Lập danh sách, đánh dấu từng mục sẽ nằm ở điều nào của bản nháp.
2. **Hình thức.** Bằng văn bản? Công chứng hoặc chứng thực? Đăng ký tại cơ quan nào? Thời điểm có hiệu lực (ký, công chứng, đăng ký)? Hậu quả nếu sai hình thức.
3. **Giới hạn do luật đặt ra.**
   - Phạt vi phạm: Bộ luật Dân sự để các bên tự thỏa thuận *trừ khi luật liên quan có quy định khác*; một số luật chuyên ngành đặt mức trần (vd Luật Thương mại, luật về xây dựng). Đọc đúng luật áp dụng cho hợp đồng này rồi mới ghi mức.
   - Lãi suất vay, lãi chậm trả, tiền đặt cọc, thời gian thử việc, tiền lương tối thiểu, thời hạn bảo hành… — tra Điều tương ứng.
   - Điều khoản bị cấm hoặc vô hiệu (vd hạn chế quyền lao động trái luật, miễn trách nhiệm trái điều cấm).
4. **Nội dung đặc thù.** Chuyển giao quyền sở hữu trí tuệ (phạm vi quyền, lãnh thổ, thời hạn, quyền nhân thân không chuyển được), dữ liệu cá nhân (mục đích, đồng ý, xử lý khi chấm dứt), quảng cáo (ghi nhãn, sản phẩm hạn chế).

Ghi kết quả thành bảng nháp nội bộ: `Yêu cầu | Văn bản, Điều, Khoản | Hiệu lực | Sẽ thể hiện ở Điều … của hợp đồng`.

## Bước 4 — Soạn bản nháp
Cấu trúc gợi ý (điều chỉnh theo loại hợp đồng):
1. Quốc hiệu, tiêu ngữ; tên hợp đồng; số hợp đồng.
2. Căn cứ ký kết (liệt kê văn bản đã tra, có số hiệu).
3. Thông tin các bên (tên, mã số doanh nghiệp/số định danh, địa chỉ, người đại diện, chức vụ, giấy ủy quyền nếu có).
4. Điều 1 — Đối tượng, phạm vi.
5. Điều 2 — Giá, thanh toán, thuế, hóa đơn.
6. Điều 3 — Thời hạn, địa điểm, phương thức thực hiện, nghiệm thu.
7. Điều 4–5 — Quyền và nghĩa vụ từng bên.
8. Điều 6 — Sở hữu trí tuệ / bảo mật / dữ liệu cá nhân (nếu có).
9. Điều 7 — Phạt vi phạm và bồi thường thiệt hại (trong giới hạn đã tra).
10. Điều 8 — Bất khả kháng.
11. Điều 9 — Sửa đổi, tạm ngừng, chấm dứt, đơn phương chấm dứt.
12. Điều 10 — Giải quyết tranh chấp, luật áp dụng.
13. Điều 11 — Hiệu lực, số bản, ngôn ngữ; chữ ký.

Quy tắc viết:
- Câu ngắn, mỗi khoản một nghĩa vụ; dùng số đo được (ngày, số tiền, %), tránh "kịp thời", "hợp lý" khi có thể định lượng.
- Thuật ngữ thống nhất từ đầu đến cuối; định nghĩa ở Điều đầu nếu nhiều thuật ngữ.
- Số tiền ghi bằng số và bằng chữ; ngày theo `dd/mm/yyyy`.
- Không chép nguyên điều luật vào hợp đồng; dẫn "theo quy định tại Điều … của …" khi cần.

## Bước 5 — Ghi chú căn cứ từng điều
Sau bản nháp (hoặc chú thích ngay dưới mỗi điều, in nghiêng), thêm bảng:

| Điều trong hợp đồng | Căn cứ pháp lý | Hiệu lực | Ghi chú |
|---|---|---|---|
| Điều 7 — Phạt vi phạm […]% | Luật …, số …, Điều … | Còn hiệu lực | Mức trần đọc được trong Điều này; link |
| Điều 11 — Hình thức | Luật …, Điều … | Còn hiệu lực | Phải công chứng / không bắt buộc |

Thêm mục **Việc cần làm sau khi ký**: công chứng, đăng ký, khai thuế, lưu hồ sơ — chỉ nêu việc có căn cứ đã đọc.

Thêm mục **Chưa xác minh** và dòng miễn trừ như skill `tra-cuu-phap-luat`.

## Ví dụ ngắn
Người dùng: "Soạn hợp đồng dịch vụ quay video quảng cáo giữa công ty tôi và một freelancer, công ty được toàn quyền dùng video."
1. `check_compliance {question: "hợp đồng dịch vụ với cá nhân, chuyển nhượng quyền tác giả tác phẩm điện ảnh, nội dung bắt buộc của hợp đồng chuyển nhượng quyền tác giả"}`.
2. `get_document` các Điều về hợp đồng dịch vụ (Bộ luật Dân sự) và hợp đồng chuyển nhượng quyền tác giả (Luật Sở hữu trí tuệ).
3. Kiểm tra dấu hiệu quan hệ lao động trá hình (làm thường xuyên, chịu quản lý giờ giấc) → cảnh báo nếu có.
4. Soạn: chuyển nhượng quyền tài sản (liệt kê quyền), quyền nhân thân giữ cho tác giả, thù lao gồm cả tiền chuyển nhượng, khấu trừ thuế TNCN theo văn bản đã tra.
5. Bảng căn cứ + miễn trừ.

Xuất ra Word: dùng skill `trinh-bay-va-dinh-dang`. Không ký, gửi hay nộp thay người dùng.
