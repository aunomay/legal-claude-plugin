---
name: trinh-bay-va-dinh-dang
description: Trình bày kết quả tra cứu pháp luật, rà soát hợp đồng, checklist tuân thủ hoặc bản nháp hợp đồng thành file Word (.docx) chuyên nghiệp bằng tiếng Việt — báo cáo pháp lý, bản ghi nhớ (memo), ý kiến tra cứu, phụ lục căn cứ. Dùng khi người dùng nói "xuất ra Word", "làm thành file docx", "định dạng báo cáo", "in ra để gửi sếp/khách hàng", "trình bày theo chuẩn văn bản hành chính", "export to Word". Quy định cấu trúc (tiêu đề, tóm tắt, câu hỏi, bảng căn cứ, phân tích, danh mục trích dẫn, miễn trừ), kiểu chữ Times New Roman 13, khổ A4, lề theo Nghị định 30/2020/NĐ-CP, và cách tạo bằng python-docx hoặc skill docx.
---

# Trình bày và định dạng báo cáo Word

English: turn verified lookup results into a clean Vietnamese .docx report.

Skill này chỉ định dạng; nội dung pháp lý phải đã được kiểm chứng theo `tra-cuu-phap-luat`. Không thêm căn cứ mới khi định dạng; nếu phát hiện thiếu căn cứ thì quay lại tra.

## 1. Cấu trúc báo cáo

1. **Tiêu đề** — vd "BÁO CÁO TRA CỨU PHÁP LÝ", dòng phụ: chủ đề; ngày lập; người yêu cầu (nếu người dùng muốn ghi).
2. **Tóm tắt kết luận** — 3–6 gạch đầu dòng, đọc riêng vẫn hiểu.
3. **Câu hỏi và sự việc** — nguyên văn câu hỏi; các dữ kiện và giả định đã dùng; thời điểm áp dụng luật.
4. **Bảng căn cứ pháp lý**

   | STT | Văn bản | Số hiệu | Điều, Khoản, điểm | Tình trạng hiệu lực | Nội dung chính |
   |---|---|---|---|---|---|

5. **Phân tích** — theo từng vấn đề (tiêu đề cấp 2), mỗi vấn đề: quy định → áp dụng → kết luận. Phép tính: công thức rồi từng bước.
6. **Rủi ro / việc cần làm** (nếu có) — bảng hoặc checklist từ `phan-tich-hop-dong`, `doi-chieu-tuan-thu`.
7. **Nội dung chưa xác minh**.
8. **Danh mục trích dẫn** — đánh số [1], [2]…: tên văn bản, số hiệu, ngày ban hành, ngày hiệu lực, tình trạng, đường link nguồn, ngày tra cứu. Ghi văn bản nào đọc qua Aunomay Legal, văn bản nào đọc trực tiếp trên cổng chính thức.
9. **Miễn trừ trách nhiệm** — "Báo cáo được lập bằng công cụ tra cứu Aunomay Legal, không phải ý kiến tư vấn pháp lý. Nội dung có thể chứa sai sót; cần đối chiếu văn bản gốc và tham khảo luật sư trước khi ra quyết định quan trọng."

Bản nháp hợp đồng: dùng cấu trúc của skill `soan-hop-dong` (quốc hiệu, tiêu ngữ, căn cứ, các Điều, chữ ký), bảng ghi chú căn cứ để ở phụ lục riêng hoặc file riêng — không để lẫn vào bản sẽ ký.

## 2. Quy cách trình bày

Đã đối chiếu (Phụ lục I, Nghị định 30/2020/NĐ-CP về công tác văn thư):
- Khổ giấy A4 (210 × 297 mm), trình bày theo chiều dọc.
- Phông Times New Roman, bộ mã Unicode theo TCVN 6909:2001, chữ màu đen.
- Lề: trên 20–25 mm, dưới 20–25 mm, trái 30–35 mm, phải 15–20 mm.

Lựa chọn mặc định của Aunomay Legal cho báo cáo tra cứu (không phải văn bản hành chính, nên đây là quy ước nội bộ):
- Thân bài cỡ 13, căn đều hai bên; giãn dòng 1.15–1.3; cách đoạn 6 pt.
- Tiêu đề báo cáo cỡ 14 in hoa đậm, căn giữa; tiêu đề cấp 1 cỡ 13 đậm; cấp 2 cỡ 13 đậm nghiêng.
- Bảng cỡ 11–12, có viền mảnh, hàng tiêu đề đậm và lặp lại khi sang trang.
- Đánh số trang ở giữa lề trên hoặc chân trang.
- Lề mặc định dùng: trên 20 mm, dưới 20 mm, trái 30 mm, phải 15 mm (nằm trong khoảng ở trên).

Cần đúng thể thức **văn bản hành chính** (công văn, quyết định của cơ quan, tổ chức) thì tra lại Nghị định 30/2020/NĐ-CP và văn bản sửa đổi (nếu có) bằng `search_legal_docs {query: "thể thức kỹ thuật trình bày văn bản hành chính"}` hoặc trên cổng chính thức, rồi theo đúng cỡ chữ, vị trí từng thành phần trong Phụ lục I.

Chính tả, kiểu chữ:
- Số hiệu viết đúng nguyên dạng: `91/2015/QH13`, `…/2026/NĐ-CP`, `…/2026/TT-BTC`.
- "Điều 385 khoản 1 điểm a" hoặc "điểm a khoản 1 Điều 385" — chọn một kiểu và dùng thống nhất.
- Ngày `dd/mm/yyyy`; số tiền có dấu chấm phân cách nghìn: `1.000.000 đồng`.
- Không dùng chữ in hoa toàn bộ cho đoạn văn; chỉ tiêu đề.

## 3. Cách tạo file

Thứ tự ưu tiên:
1. **Skill `docx`** (nếu có trong phiên, vd `anthropic-skills:docx`) — gọi skill đó và đưa cho nó cấu trúc + quy cách ở trên.
2. **python-docx** — kiểm tra `python -c "import docx"`; thiếu thì xin phép người dùng trước khi cài (`pip install python-docx`).
3. Không có cả hai → xuất Markdown có cùng cấu trúc và nói rõ chưa tạo được .docx.

Khung python-docx:
```python
from docx import Document
from docx.shared import Pt, Mm
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.oxml.ns import qn

doc = Document()
sec = doc.sections[0]
sec.page_width, sec.page_height = Mm(210), Mm(297)
sec.top_margin, sec.bottom_margin = Mm(20), Mm(20)
sec.left_margin, sec.right_margin = Mm(30), Mm(15)

st = doc.styles["Normal"]
st.font.name = "Times New Roman"
st.font.size = Pt(13)
st.element.rPr.rFonts.set(qn("w:eastAsia"), "Times New Roman")
st.paragraph_format.space_after = Pt(6)
st.paragraph_format.line_spacing = 1.2

for name in ("Heading 1", "Heading 2", "Title"):
    h = doc.styles[name]
    h.font.name = "Times New Roman"
    h.element.rPr.rFonts.set(qn("w:eastAsia"), "Times New Roman")
    h.font.color.rgb = None

t = doc.add_paragraph("BÁO CÁO TRA CỨU PHÁP LÝ")
t.alignment = WD_ALIGN_PARAGRAPH.CENTER
t.runs[0].bold = True
t.runs[0].font.size = Pt(14)

doc.add_heading("1. Tóm tắt kết luận", level=1)
doc.add_paragraph("…", style="List Bullet")

doc.add_heading("2. Căn cứ pháp lý", level=1)
rows = [("1", "Bộ luật Dân sự", "91/2015/QH13", "Điều …", "Còn hiệu lực", "…")]
tbl = doc.add_table(rows=1, cols=6)
tbl.style = "Table Grid"
for cell, text in zip(tbl.rows[0].cells,
        ["STT", "Văn bản", "Số hiệu", "Điều, Khoản", "Hiệu lực", "Nội dung"]):
    cell.text = text
    cell.paragraphs[0].runs[0].bold = True
for r in rows:
    for cell, text in zip(tbl.add_row().cells, r):
        cell.text = text

doc.save("bao-cao-tra-cuu.docx")
```
Ghi chú: đặt `rFonts eastAsia` để tiếng Việt không bị đổi phông; tên file không dấu, không khoảng trắng; lưu vào thư mục người dùng chỉ định (mặc định thư mục làm việc hiện tại).

## 4. Kiểm tra trước khi giao
- Mở lại file (đọc bằng python-docx) và kiểm tra: đủ 9 phần, mọi căn cứ trong phân tích đều có trong bảng và danh mục trích dẫn, mọi link đầy đủ.
- Không còn chỗ trống `[...]` ngoài chỗ người dùng phải tự điền (liệt kê cho người dùng).
- Báo đường dẫn tuyệt đối của file đã tạo.
