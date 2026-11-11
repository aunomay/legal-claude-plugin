---
name: tra-cuu-phap-luat
description: Kỹ năng nền cho MỌI câu hỏi về pháp luật Việt Nam — dân sự, đất đai, nhà ở, xây dựng, hôn nhân gia đình, lao động, bảo hiểm xã hội, thuế (TNCN, TNDN, hộ kinh doanh), doanh nghiệp, hợp đồng, dữ liệu cá nhân, quảng cáo, xử phạt hành chính, hình sự. Dùng khi người dùng hỏi "luật nói gì", "có bị phạt không", "phạt bao nhiêu", "có hợp pháp không", "có được … không", "điều kiện để …", "thủ tục …", "tính thuế / tính BHXH một lần", "so sánh hộ kinh doanh với công ty", hoặc nhắc tới một số hiệu văn bản (vd 91/2015/QH13). Tra bằng các công cụ Aunomay Legal (search_legal_docs, get_document, get_summary, check_compliance, get_laws), đọc toàn văn Điều trước khi dẫn, kiểm tra hiệu lực tại thời điểm sự việc, dẫn số hiệu + Điều/Khoản/điểm + link. Các skill soan-hop-dong, phan-tich-hop-dong, doi-chieu-tuan-thu, trinh-bay-va-dinh-dang, ban-quyen-sang-tao đều dựa trên quy trình này.
---

# Tra cứu pháp luật có kiểm chứng

English: base workflow — every legal statement must trace back to an article you actually read in full, in a document that was in force at the relevant time.

Nguyên tắc gốc: **trí nhớ của mô hình chỉ để biết nên tìm gì; căn cứ trả lời là văn bản đã đọc ở lượt này.**

## Công cụ (máy chủ MCP `aunomay-legal`)

Trong Claude Code, tên đầy đủ có tiền tố (vd `mcp__plugin_aunomay-legal_aunomay-legal__search_legal_docs`); dưới đây gọi tắt.

| Công cụ | Dùng khi | Tham số chính |
|---|---|---|
| `search_legal_docs` | Tìm văn bản và Điều liên quan theo từ khóa | `query`, `doc_type` ("Luật", "Bộ luật", "Nghị định", "Thông tư", "Nghị quyết"), `in_force_only` (mặc định `true`), `limit` 1–20 |
| `get_document` | Đọc nguyên văn Điều cần dẫn, hoặc cả văn bản theo trang | `doc` (id hoặc số hiệu, vd `"91/2015/QH13"`), `articles` (vd `"385,400-405"`), `offset`, `max_chars` |
| `get_summary` | Xem mục lục Phần/Chương/Mục/Điều để biết Điều nào cần đọc | `doc` |
| `check_compliance` | Câu hỏi "có được / có phải / có vi phạm không", tìm các Điều liên quan nhất trên toàn kho hoặc trong một văn bản | `question`, `doc` (tùy chọn), `limit` 1–15 |
| `get_laws` | Xem kho đang có văn bản nào theo lĩnh vực | `field`, `status` ("in_force" / "all"), `page` |
| `get_account_status` | Kiểm tra hạn mức còn lại | không có |

Gói miễn phí giới hạn lượt tra mỗi ngày. Gom câu hỏi hợp lý: dùng `get_summary` một lần rồi đọc nhiều Điều trong **một** lệnh `get_document` (`articles: "8,9,12-14"`) thay vì gọi từng Điều. Lỗi kết nối, đăng nhập, hết lượt → skill `setup`.

## Quy tắc cứng

1. **Không dẫn từ đoạn trích của kết quả tìm kiếm.** `snippet` chỉ để định vị. Trước khi dẫn một Điều, phải đọc toàn văn Điều đó bằng `get_document`.
2. Không nêu mức phạt, thuế suất, mức đóng, thời hạn, con số nào chưa đọc được ở lượt này. Không dùng con số nhớ sẵn, kể cả khi "chắc chắn".
3. Mỗi căn cứ ghi đủ: **tên văn bản – số hiệu – Điều, Khoản, điểm – tình trạng hiệu lực – link nguồn** (trường `source_url` trả về).
4. Không tìm được → nói `Chưa xác minh được: …` kèm lý do. Không lấp chỗ trống bằng phỏng đoán.
5. Kết thúc mỗi câu trả lời bằng dòng miễn trừ (xem mẫu).

## Quy trình

### Bước 1 — Khoanh sự việc
- Ai (cá nhân, hộ kinh doanh, doanh nghiệp, cơ quan), làm gì, ở đâu, **khi nào**. Luật áp dụng là luật có hiệu lực **tại thời điểm xảy ra sự việc** (ký hợp đồng, xây nhà, phát sinh thu nhập…), không mặc định là hôm nay.
- Thiếu chi tiết làm đổi kết luận (thời điểm, giá trị, loại đất, có giấy phép không…) → hỏi lại ngắn, hoặc trả lời theo từng giả định và nói rõ giả định.

### Bước 2 — Tìm văn bản
1. Gọi `search_legal_docs` với từ khóa pháp lý (không phải câu hỏi đời thường). Ví dụ: "xây dựng không có giấy phép phạt" thay cho "xây nhà không phép bị sao".
2. Câu hỏi dạng "có được/có phải" → gọi thêm `check_compliance` để thấy các Điều liên quan nằm rải ở nhiều văn bản.
3. Biết văn bản nhưng chưa biết Điều → `get_summary` rồi chọn Điều theo mục lục.
4. Nhớ thứ bậc: Hiến pháp > Bộ luật, Luật > Nghị quyết UBTVQH > Nghị định > Quyết định TTg > Thông tư > văn bản địa phương. Luật giao "Chính phủ quy định chi tiết" → phải tìm nghị định hướng dẫn; mức phạt hành chính nằm ở nghị định xử phạt của lĩnh vực.

### Bước 3 — Đọc và kiểm tra hiệu lực
1. `get_document` với đúng các Điều cần dẫn (kèm Điều định nghĩa, phạm vi, ngoại lệ, chuyển tiếp nếu liên quan).
2. Xem `status` và `eff_from`:
   - **Còn hiệu lực** → dùng được, vẫn kiểm tra văn bản sửa đổi.
   - **Hết hiệu lực một phần** → kiểm tra chính Điều cần dẫn có bị sửa, bãi bỏ không.
   - **Hết hiệu lực toàn bộ** → chỉ dùng cho sự việc xảy ra trước ngày hết hiệu lực; tìm văn bản thay thế cho hiện tại.
   - **Chưa có hiệu lực** → nói rõ ngày bắt đầu áp dụng; trước ngày đó vẫn theo văn bản cũ.
3. Tìm văn bản sửa đổi, thay thế: `search_legal_docs` với `"sửa đổi bổ sung <tên văn bản>"` và với `in_force_only: false` để thấy văn bản cũ. Có **văn bản hợp nhất** thì ưu tiên đọc bản hợp nhất mới nhất (số Điều có thể khác bài viết cũ).
4. Đọc điều khoản chuyển tiếp nếu sự việc bắt đầu trước và kéo dài sau ngày luật mới có hiệu lực.

### Bước 4 — Khi kho Aunomay Legal không có văn bản
Kho ban đầu khoảng 100 văn bản cốt lõi và đang mở rộng; văn bản mới ban hành có thể chưa có.
1. Thử `get_laws` theo lĩnh vực và `search_legal_docs` với số hiệu để chắc là không có.
2. Tra trên nguồn chính thức bằng WebSearch/WebFetch: `vbpl.vn` (Cơ sở dữ liệu quốc gia về pháp luật), `congbao.chinhphu.vn`, `vanban.chinhphu.vn`, `datafiles.chinhphu.vn` (PDF văn bản hợp nhất), `quochoi.vn`, cổng bộ ngành.
3. `vbpl.vn` dựng trang bằng JavaScript nên WebFetch thường không đọc được → mở bằng trình duyệt (Claude in Chrome hoặc trình duyệt tích hợp), chỉ đọc, không đăng nhập, không giải CAPTCHA.
4. Trong câu trả lời ghi rõ: *"Văn bản này chưa có trong Aunomay Legal; đã đọc tại <link>."*

### Bước 5 — Phân biệt ba trường hợp khi gọi công cụ
| Hiện tượng | Ý nghĩa | Cách xử lý |
|---|---|---|
| Trả về danh sách rỗng | **Không có kết quả** — kho không có hoặc từ khóa chưa đúng (lượt này không bị tính) | Đổi từ khóa, bỏ `doc_type`, thử `in_force_only: false`, rồi mới chuyển Bước 4 |
| Có văn bản nhưng con số là 0, hoặc Điều ghi "không phải nộp / không áp dụng" | **Giá trị bằng 0 thật** theo luật | Trả lời bằng 0 và dẫn Điều đó; không gộp với "không tìm thấy" |
| Thông báo lỗi (Unauthorized, quota, timeout, 5xx) | **Lỗi**, không nói gì về luật | Không kết luận nội dung pháp lý; xem skill `setup` |

### Bước 6 — Tính toán (thuế TNCN, BHXH một lần, thuế hộ kinh doanh so với công ty…)
1. Đọc bảng thuế suất, mức giảm trừ, công thức, mức tham chiếu **từ văn bản đang có hiệu lực** cho kỳ cần tính (vd biểu thuế lũy tiến, mức giảm trừ gia cảnh, tỷ lệ % trên doanh thu, cách tính mức bình quân tiền lương đóng BHXH, hệ số trượt giá). Không dùng số nhớ sẵn.
2. Ghi công thức trước, rồi thay số từng bước, mỗi bước một dòng, có đơn vị.
3. Nêu mọi giả định (thu nhập trước/sau bảo hiểm, số người phụ thuộc, số năm đóng trước/sau mốc, loại hình kinh doanh, ngưỡng doanh thu…).
4. Có tham số do văn bản khác ban hành (hệ số trượt giá hằng năm, mức lương tham chiếu) mà chưa đọc được → dừng ở công thức và ghi `Chưa xác minh được`.
5. So sánh phương án (hộ kinh doanh / công ty) → bảng cùng một mức doanh thu, cùng giả định chi phí; nhắc các khoản ngoài thuế (BHXH chủ, kế toán, hóa đơn) nếu có căn cứ.

Ví dụ khung tính:
```
Thu nhập tính thuế = Thu nhập chịu thuế − Giảm trừ gia cảnh − Bảo hiểm bắt buộc  (căn cứ: Điều …, Luật …)
= 30.000.000 − … − … = … đồng
Thuế phải nộp = Σ (phần thu nhập trong từng bậc × thuế suất bậc đó)  (biểu thuế: Điều …)
```

### Bước 7 — Trả lời theo mẫu

```
**Trả lời ngắn:** <1–3 câu, kết luận trực tiếp>

**Căn cứ pháp lý:**
- <Tên văn bản> số <số hiệu>, Điều <x> khoản <y> điểm <z> — <Còn hiệu lực / Hết hiệu lực một phần …, hiệu lực từ dd/mm/yyyy>. <Diễn giải hoặc trích ngắn một câu>. Nguồn: <url>
- …

**Áp dụng vào trường hợp của bạn:** <lập luận từng bước; nêu giả định; nếu có tính toán thì ghi công thức và từng bước>

**Chưa xác minh / cần làm rõ:** <văn bản chưa đọc được, chi tiết còn thiếu, chỗ các nguồn khác nhau>

_Aunomay Legal là công cụ tra cứu, không phải dịch vụ tư vấn pháp lý. Nội dung do AI tổng hợp có thể sai; hãy đối chiếu văn bản gốc qua đường link và hỏi luật sư trước khi ra quyết định quan trọng._
```

- Trả lời bằng ngôn ngữ người hỏi; giữ nguyên tên văn bản tiếng Việt.
- Mức phạt: ghi rõ áp dụng cho cá nhân hay tổ chức (nhiều nghị định quy định mức cho cá nhân, tổ chức gấp đôi — đọc Điều quy định về mức phạt để xác nhận), kèm biện pháp khắc phục hậu quả (vd buộc tháo dỡ) nếu Điều đó quy định.
- Hai nguồn mâu thuẫn → nêu cả hai và nói văn bản nào có thứ bậc cao hơn hoặc ban hành sau.

## Ví dụ

**"Xây nhà không phép bị phạt bao nhiêu, có bị tháo dỡ không?"**
1. `search_legal_docs {query: "xây dựng không có giấy phép xử phạt", doc_type: "Nghị định"}`.
2. `get_summary` nghị định xử phạt lĩnh vực xây dựng → tìm Điều về vi phạm trật tự xây dựng.
3. `get_document {doc: "<số hiệu>", articles: "<Điều đó>,<Điều về mức phạt cá nhân/tổ chức>"}` — đọc mức theo loại công trình, biện pháp khắc phục.
4. `search_legal_docs {query: "giấy phép xây dựng miễn", doc_type: "Luật"}` → đọc Điều về trường hợp được miễn phép (nhà ở nông thôn…), vì kết luận phụ thuộc vào việc có phải xin phép không.
5. Trả lời theo mẫu, tách "phạt tiền" và "buộc tháo dỡ / thủ tục hợp thức" theo từng giả định.

**"Ly hôn rồi, người nuôi con có được tự đưa con ra nước ngoài không?"**
→ `check_compliance {question: "người trực tiếp nuôi con sau ly hôn đưa con ra nước ngoài có cần đồng ý của người kia", limit: 10}` rồi `get_document` các Điều về quyền, nghĩa vụ của cha mẹ sau ly hôn trong Luật Hôn nhân và gia đình và quy định về xuất cảnh của người chưa thành niên.
