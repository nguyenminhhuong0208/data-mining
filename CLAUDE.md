# CLAUDE.md

Tài liệu hướng dẫn trợ lý AI (Claude Code) khi phát triển tài liệu và bài giảng cho khóa học **Khai phá dữ liệu (Data Mining)** của Viện Trí tuệ Nhân tạo (IAI), Trường Đại học Công nghệ (UET – VNU).

---

## 1. Định hướng & Đối tượng mục tiêu

- **Định hướng khóa học:** Khóa học Khai phá dữ liệu chuyên sâu, tổng hợp và chuẩn hóa, không phụ thuộc vào một học kỳ cụ thể nào. Khóa học được thiết kế như một tài liệu học tập mở (Open Educational Resource - OER), bền vững theo thời gian.
- **Đối tượng người học:** Mở rộng cho mọi đối tượng quan tâm đến Data Mining (sinh viên đại học, học viên cao học, kỹ sư dữ liệu, lập trình viên và người tự học). Do đó:
  - Cần đảm bảo tính chặt chẽ về thuật toán và nền tảng toán học.
  - Đồng thời phải có trực giác sinh động, ví dụ tính tay được (lead-in numbers), liên hệ thực tế dữ liệu lớn và giải thích dễ hiểu, mạch lạc.

---

## 2. Kiến trúc & Công nghệ

Dự án tuân thủ triệt để mô hình **Web tĩnh 100% (No Framework, No Build Step)**:
- **Slide bài giảng:** HTML5 + [Reveal.js](https://revealjs.com/) (chạy trực tiếp trên trình duyệt, nạp file tĩnh).
- **Ghi chú bài giảng (Lecture Notes):** File Markdown tĩnh (`.md`), được render phía client qua bộ đọc `material-viewer.html` kết hợp **KaTeX** (toán học), **Marked** (parser), và **DOMPurify** (sanitizer).
- **Không build step:** Không dùng Webpack, Vite, npm build hay compiler.
- **Không CDN:** Toàn bộ thư viện JavaScript, CSS, phông chữ được tải về đặt trong `vendor/`, `revealjs/`, `plugin/`. Không tải tài nguyên từ bên ngoài (`default-src 'self'`).

---

## 3. Cấu trúc thư mục

Toàn bộ tài nguyên của khóa học được tổ chức phẳng và trực tiếp trong kho:

```text
data-mining/
├── index.html                      # Trang chủ khóa học (danh mục toàn bộ bài giảng & tài liệu)
├── lecture-template.html           # Bản mẫu HTML chuẩn cho slide bài giảng
├── lecture-style.css               # CSS dùng chung cho toàn bộ slide
├── material-viewer.html            # Trình đọc web tĩnh cho ghi chú bài giảng
├── material-viewer.css             # CSS cho trình đọc ghi chú
├── material-viewer.js              # JS xử lý Markdown + KaTeX + directives
├── material-index.css              # CSS bổ trợ chỉ mục tài liệu
│
├── lecture-XX-<slug>.html          # Slide Reveal.js cho Bài XX (XX = 01, 02, ...)
│
├── materials/                      # Ghi chú bài giảng, câu hỏi quiz và bài tập
│   ├── _templates/                 # Bản mẫu Markdown cho ghi chú
│   ├── quizzes/                    # Phiếu quiz câu hỏi ngắn (quiz-XX.html)
│   ├── assignments/                # File đề bài tập tuần cho sinh viên (assignment-XX.pdf)
│   ├── docs/                       # Giáo trình và tài liệu đọc thêm (PDF)
│   └── lec-XX/                     # Thư mục tài liệu của Bài XX
│       ├── lecture-note.md         # Nội dung ghi chú chi tiết
│       ├── quiz.html               # Quiz bài tập ngắn riêng của bài
│       └── assignment.pdf          # File đề bài tập của bài
│
├── img/                            # Hình vẽ và sơ đồ trực quan
│   └── lec-XX/                     # Hình ảnh riêng cho Bài XX
│       └── *.svg                   # Ưu tiên tuyệt đối định dạng SVG
│
├── planning/                       # Hồ sơ lập kế hoạch và biên tập (nội bộ)
│   └── lec-XX/
│       ├── outline.md              # Đề cương chi tiết, mục tiêu, bảng thuật ngữ
│       ├── storyboard.md           # Kịch bản từng slide, luồng dẫn dắt, đếm mật độ
│       └── review-log.md           # Nhật ký rà soát, đánh giá, kiểm định chất lượng
│
├── sources/                        # Tài liệu nguồn, giáo trình, đề cương, ánh xạ
│   ├── source.md                   # Bản đồ nguồn: danh mục bài giảng, CĐR, tiên quyết
│   └── reference-slides/           # Slide tham khảo từ các nguồn uy tín (MMDS, CS246,...)
│
├── revealjs/                       # Mã nguồn tĩnh Reveal.js cục bộ
├── plugin/                         # Các plugin Reveal.js (highlight, math, notes)
└── vendor/                         # Thư viện bên thứ ba cục bộ (offline)
    ├── katex/                      # KaTeX CSS, JS và fonts
    ├── marked/                     # Marked JS parser
    └── dompurify/                  # DOMPurify sanitizer
```

---

## 4. Quy ước đặt tên file & Mã định danh

| Loại tài nguyên | Quy ước đường dẫn & tên file | Ví dụ |
|---|---|---|
| **Slide bài giảng** | `lecture-XX-<slug>.html` (`XX` gồm 2 chữ số: 01, 02,...) | `lecture-01-tong-quan-khai-pha-du-lieu.html` |
| **Ghi chú bài giảng** | `materials/lec-XX/lecture-note.md` | `materials/lec-01/lecture-note.md` |
| **Quiz ngắn** | `materials/quizzes/quiz-XX.html` hoặc `materials/lec-XX/quiz.html` | `materials/quizzes/quiz-01.html` |
| **Bài tập tuần** | `materials/assignments/assignment-XX.pdf` hoặc `materials/lec-XX/assignment.pdf` | `materials/assignments/assignment-01.pdf` |
| **Hình vẽ SVG** | `img/lec-XX/<ten-hinh>.svg` | `img/lec-01/k-means-clustering-steps.svg` |
| **Kế hoạch & rà soát** | `planning/lec-XX/{outline,storyboard,review-log}.md` | `planning/lec-01/outline.md` |
| **Slide ID (trong HTML)** | `id="lecXX-sMM-NN"` và `data-slide-id="lecXX-sMM-NN"` | `lec01-s02-01` (bài 01, mạch 02, slide 01) |
| **Strand Title ID** | `id="mach-M"` và `data-slide-id="lecXX-sMM-00"` | `lec01-s02-00` (slide tiêu đề mạch 2) |
| **Topic ID (ghi chú)** | `<!-- note-topic-id: lec-XX-topic-k -->` đặt trước heading | `<!-- note-topic-id: lec-01-topic-2 -->` |

---

## 5. Quy tắc nội dung & Ngôn ngữ (Tiếng Việt)

- **Chuẩn văn phong:** Tiếng Việt học thuật, trang trọng, chính xác, khách quan, giàu tính trực quan sư phạm. Không dùng ngôn ngữ nói mô phỏng ("chúng ta hãy nhìn", "người viết xin lưu ý"), câu hỏi tu từ, khẩu hiệu hoặc văn phong tiếp thị.
- **Thuật ngữ chuyên môn:**
  - Viết thuần Việt là chính.
  - Khi xuất hiện thuật ngữ lần đầu trong tài liệu: ghi `Thuật ngữ tiếng Việt (Tiếng Anh tương ứng)`. Ví dụ: *khai phá tập mục phổ biến (frequent itemset mining)*, *phân cụm (clustering)*.
  - Viết tắt: ghi đầy đủ tiếng Việt lần đầu rồi để chữ viết tắt trong ngoặc đơn.
  - Sử dụng thống nhất **"Lời giải"** (không dùng "Đáp án").
  - Mọi thuật ngữ của bài phải được lập bảng đối soát trong `outline.md`.
- **Slide:**
  - Tuyệt đối không dùng "chúng ta" trên mặt slide và speaker notes.
  - Mỗi slide có một luận điểm rõ ràng, tiêu đề mang tính khẳng định/nêu khái niệm (không đặt tiêu đề dạng câu hỏi).
  - Khống chế mật độ chữ: hướng tới $\le 40$ âm tiết/slide nội dung, trần cứng $60$ âm tiết (bảng tóm tắt/mục tiêu $\le 80$).
- **Ghi chú bài giảng (Lecture Note):**
  - Đóng vai trò như một chương giáo trình hoàn chỉnh, tự đọc và hiểu độc lập không cần phụ thuộc slide.
  - Dùng "chúng ta" khi nêu nhu cầu, kế hoạch; dùng "ta" trong biến đổi toán học; giữ giọng khách quan trong định lý/thuật toán.

---

## 6. Quy chuẩn kỹ thuật

### Slide Reveal.js
- **Cấu hình chuẩn:**
  ```javascript
  Reveal.initialize({
    width: 1280,
    height: 720,
    margin: 0.04,
    controlsLayout: "edges",
    slideNumber: true,
    hash: true,
    hashOneBasedIndex: true,
    katex: { local: "vendor/katex" },
    plugins: [RevealHighlight, RevealNotes, RevealMath.KaTeX]
  });
  ```
- **Cấu trúc Slide:** Phân thành 5–7 mạch (strand lớn - thẻ `<section>` ngoài), mỗi mạch gồm các slide con (`<section>` trong). Ngoại trừ mạch mở đầu, mỗi mạch bắt đầu bằng một slide tiêu đề mạch (`section.strand-title`).
- **CSS:** Toàn bộ slide chỉ liên kết tới `lecture-style.css`. Không viết inline CSS ghi đè cỡ chữ hoặc chèn khối `<style>` riêng trong từng HTML.

### Ghi chú bài giảng & Material Viewer
- **URL mở ghi chú:** `material-viewer.html?doc=materials/lec-XX/lecture-note.md&deck=lecture-XX-<slug>.html`.
- **Công thức toán:** Chỉ dùng `$...$` (inline) và `$$...$$` (block display).
- **Cú pháp Directives 14 khối:**
  `::: <block_name> [Tiêu đề tuỳ chọn]` ... `:::`
  Hỗ trợ: `definition`, `theorem`, `proposition`, `lemma`, `corollary`, `remark`, `algorithm`, `example`, `application`, `derivation`, `proof`, `exercise`, `hint`, `solution`.

### Trực quan hóa (Figures) & Dữ liệu
- Vẽ mới sơ đồ dưới định dạng **SVG** trong `img/lec-XX/`, có thuộc tính `role="img"` và `aria-label`/`alt` đầy đủ.
- Công thức, bảng biểu, mã giả phải soạn bằng HTML/KaTeX, tuyệt đối không chụp ảnh dán vào.

---

## 7. Lệnh làm việc & Kiểm tra cục bộ

Chạy máy chủ tĩnh phục vụ kiểm thử (tại thư mục gốc của kho):
```bash
# Sử dụng Python HTTP server
python -m http.server 8000

# Hoặc dùng reloadserver tự reload khi sửa file
python -m reloadserver 8765
```

- Xem slide bài giảng: `http://localhost:8000/lecture-XX-<slug>.html`
- Xem ghi chú bài giảng: `http://localhost:8000/material-viewer.html?doc=materials/lec-XX/lecture-note.md&deck=lecture-XX-<slug>.html`

Kiểm tra định dạng và trạng thái git:
```bash
git status --short
git diff --check
```

---

## 8. Quy trình hoàn thành một bài học ("Done" Definition)

Một bài giảng được xem là hoàn thành khi đáp ứng đủ các tiêu chí:
1. Có đủ bộ 5 thành phần: Slide (`lecture-XX-*.html`), Ghi chú (`materials/lec-XX/lecture-note.md`), Hình vẽ SVG (`img/lec-XX/`), Kế hoạch biên tập (`planning/lec-XX/`), và liên kết trong `index.html`.
2. Không có lỗi bảng điều khiển (console errors), không có lỗi KaTeX (`.katex-error`).
3. Mọi tài nguyên tải hoàn toàn cục bộ từ `vendor/` (không có lỗi mạng/CSP).
4. Mật độ chữ trên slide không vượt ngưỡng; không có chữ tràn viền (overflow) ở cả tỷ lệ 16:9 (1600×900) và màn hình hẹp di động (390×844).
5. Các bài tập vận dụng trích dẫn trực tiếp từ giáo trình/nguồn chuẩn (MMDS, Han-Kamber...), có đề bài và lời giải đầy đủ trong speaker notes.
