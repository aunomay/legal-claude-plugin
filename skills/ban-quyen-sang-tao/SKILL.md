---
name: ban-quyen-sang-tao
description: Kiểm tra bản quyền và chính sách cho người làm nội dung (YouTube, TikTok, Facebook, podcast, livestream, thiết kế, nhiếp ảnh) — dùng nhạc, hình, video, phim của người khác; trích dẫn, review, reaction; nội dung tạo bằng AI có được bảo hộ không, có phải khai báo không; kinh sách, tranh tượng, văn hóa dân gian; bị Content ID claim, gậy bản quyền, tắt kiếm tiền vì "nội dung dùng lại", tranh chấp, phản đối DMCA; mức phạt hành chính về quyền tác giả. Dùng khi người dùng hỏi "video này có an toàn bản quyền không", "nhạc này dùng được không", "ảnh AI có bản quyền không", "bị claim thì làm gì", "kháng nghị thế nào", "copyright check for my video". Luật Việt Nam tra bằng công cụ Aunomay Legal; chính sách YouTube đọc từ trang chính thức của YouTube.
---

# Bản quyền cho người sáng tạo

English: copyright, AI content and platform-policy checks for creators. Vietnamese law via Aunomay Legal tools; YouTube policy only from YouTube's own pages.

Dựa trên skill `tra-cuu-phap-luat`. Ghi chú định hướng (số Điều, trang chính sách, ngày kiểm chứng) ở `references/ghi-chu-ban-quyen.md` cạnh file này — chỉ để biết mở Điều nào, trang nào; trước khi trả lời vẫn đọc lại nguồn.

## Ba lớp phải trả lời tách bạch

| Lớp | Câu hỏi | Tra ở đâu |
|---|---|---|
| Luật Việt Nam | Có xâm phạm quyền tác giả, quyền liên quan không? Có thuộc ngoại lệ không? Bị phạt thế nào? | `search_legal_docs` / `get_document` với Luật Sở hữu trí tuệ, nghị định hướng dẫn về quyền tác giả, nghị định xử phạt |
| Chính sách nền tảng | YouTube có claim, gỡ, gậy, tắt kiếm tiền không? | Trang `support.google.com/youtube` (WebFetch) |
| Luật nơi xử lý tranh chấp | Tranh chấp trên YouTube thường theo thủ tục DMCA và học thuyết fair use của Mỹ | 17 U.S.C. §107, §512 (law.cornell.edu), copyright.gov |

Hợp pháp ở lớp này không có nghĩa là an toàn ở lớp khác (vd được phép dùng nhưng vẫn bị coi là "nội dung dùng lại" và không kiếm tiền được).

## Bước 1 — Tra luật Việt Nam bằng Aunomay Legal
1. `get_summary {doc: "Luật Sở hữu trí tuệ"}` (hoặc số hiệu trả về từ `search_legal_docs {query: "Luật Sở hữu trí tuệ quyền tác giả", doc_type: "Luật"}`) — xác định bản đang có hiệu lực / hợp nhất mới nhất.
2. Tùy câu hỏi, đọc bằng `get_document {articles: "..."}`:
   - loại hình tác phẩm được bảo hộ và đối tượng không được bảo hộ;
   - quyền nhân thân, quyền tài sản; thời hạn bảo hộ;
   - ngoại lệ không phải xin phép, không phải trả tiền (trích dẫn hợp lý, giảng dạy, đưa tin…) và giới hạn quyền (không phải xin phép nhưng phải trả tiền);
   - quyền liên quan của người biểu diễn, nhà sản xuất bản ghi;
   - quy định về tác phẩm có sử dụng hệ thống trí tuệ nhân tạo (luật và nghị định hướng dẫn).
3. `check_compliance {question: "<mô tả cách dùng cụ thể>", limit: 10}` để không bỏ sót Điều ở văn bản khác (quyền hình ảnh cá nhân, dữ liệu cá nhân, quảng cáo).
4. Mức phạt: `search_legal_docs {query: "xử phạt vi phạm hành chính quyền tác giả quyền liên quan", doc_type: "Nghị định"}` → đọc Điều hành vi tương ứng. Nghị định không có trong kho → nguồn chính thức (skill `tra-cuu-phap-luat`, Bước 4).

## Bước 2 — Đọc chính sách nền tảng
WebFetch đúng trang chính thức (danh sách trong `references/ghi-chu-ban-quyen.md`). Trang chính sách đổi thường xuyên và hiếm khi ghi ngày cập nhật → luôn đọc lại, ghi "đọc ngày …".

## Bước 3 — Checklist một video / một sản phẩm
Mỗi thành phần một dòng kết luận có căn cứ:
1. **Hình ảnh, cảnh quay** — tự quay / có giấy phép (tên giấy phép, phạm vi thương mại) / của người khác / đã hết thời hạn bảo hộ (tính theo đúng Điều về thời hạn, nêu mốc năm).
2. **Âm nhạc** — tự sáng tác / thư viện có giấy phép (điều khoản ghi công, phạm vi kiếm tiền) / nhạc AI (điều khoản dịch vụ của công cụ: gói miễn phí có cho thương mại không) / bản ghi của người khác (quyền tác giả bài hát **và** quyền liên quan của bản ghi, người biểu diễn).
3. **Nội dung AI** — điều kiện để được bảo hộ theo quy định hiện hành về tác phẩm có dùng AI; lưu bằng chứng đóng góp sáng tạo (prompt, bản nháp, lịch sử chỉnh sửa); nghĩa vụ khai báo nội dung tổng hợp/chỉnh sửa trên YouTube; chính sách "nội dung không nguyên bản" khi kiếm tiền.
4. **Tôn giáo, dân gian** — kinh điển cổ, văn học dân gian có quy định riêng hoặc đã hết thời hạn, nhưng **bản dịch, bản ghi âm, ảnh chụp, bài giảng hiện đại** có chủ sở hữu riêng.
5. **Trích dẫn, bình luận, review** — điều kiện của ngoại lệ trích dẫn trong luật Việt Nam (hợp lý, không làm sai ý, ghi tên tác giả và nguồn, không ảnh hưởng khai thác bình thường) và bốn yếu tố fair use. Không bao giờ khẳng định "chắc chắn là fair use" — đó là việc của tòa.
6. **Người xuất hiện** — quyền đối với hình ảnh cá nhân (Bộ luật Dân sự), dữ liệu cá nhân; trẻ em có quy định chặt hơn.
7. **Quảng cáo, tài trợ, link tiếp thị** — nghĩa vụ ghi rõ quảng cáo theo luật quảng cáo hiện hành và chính sách nội dung trả phí của YouTube.

Kết quả: bảng `Thành phần | Rủi ro (thấp/vừa/cao) | Căn cứ (văn bản, Điều, link hoặc trang chính sách) | Cách xử lý`.

## Bước 4 — Khi đã bị claim, gỡ, gậy hoặc tắt kiếm tiền
1. Xác định đúng loại: Content ID claim (không phải gậy) / gỡ theo yêu cầu pháp lý (gậy bản quyền) / vi phạm nguyên tắc cộng đồng / chính sách kiếm tiền YPP. Mở đúng trang hướng dẫn hiện hành.
2. Liệt kê các lựa chọn trang đó nêu (cắt đoạn, thay nhạc, chia sẻ doanh thu, tranh chấp, kháng nghị, chờ hết hạn, đề nghị rút lại) kèm điều kiện và thời hạn **đọc được trên trang**.
3. Chỉ đề xuất tranh chấp hay phản đối khi có căn cứ thật (giấy phép, tác phẩm tự làm, ngoại lệ thỏa mãn điều kiện). Nhắc: phản đối DMCA là tuyên bố có giá trị pháp lý; khai sai có thể phải chịu trách nhiệm.
4. Soạn nháp nội dung tranh chấp nếu được yêu cầu — ngắn, nêu sự kiện và giấy tờ. Không tự gửi thay người dùng.

## Không làm
- Không hướng dẫn né Content ID (lật hình, đổi tốc độ, chèn nhiễu) — không làm việc sử dụng thành hợp pháp và có thể vi phạm chính sách.
- Không bịa tên giấy phép, điều khoản dịch vụ, quy định nền tảng. Không đọc được → `Chưa xác minh được`.

## Ví dụ
"Tôi làm video review phim, dùng 5 đoạn trích mỗi đoạn 20 giây, có bị gì không?"
1. `get_document` Điều về ngoại lệ trích dẫn và Điều về quyền tài sản đối với tác phẩm điện ảnh (Luật Sở hữu trí tuệ) + Điều hướng dẫn trích dẫn trong nghị định.
2. WebFetch trang fair use và trang claim/gậy của YouTube.
3. Trả lời theo ba lớp; kết luận về rủi ro, không hứa "an toàn"; gợi ý giảm rủi ro hợp pháp (bình luận thực chất, trích ngắn, ghi nguồn).
