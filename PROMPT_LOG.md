# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** [Sinh viên xác nhận và điền chính xác trước khi nộp]
- **MSSV:** [Sinh viên xác nhận và điền chính xác trước khi nộp]
- **Tên đề tài Website:** KAZE — Đến Nhật Bản, chạm vào những điều dịu dàng
- **Công cụ AI đã sử dụng:** ChatGPT (GPT-6), công cụ tạo ảnh AI
- **Công cụ kiểm tra:** Chromium và Playwright (môi trường giả lập viewport)
- **Ngày thực hiện:** 21/10/2026

> **Lưu ý tính trung thực:** Các đoạn trong dấu ngoặc kép dưới đây ghi lại yêu cầu người dùng đã thực sự gửi; phần “prompt kỹ thuật” là chỉ dẫn triển khai được tổng hợp lại cho dễ theo dõi, không phải lời nguyên văn của sinh viên. Không ghi Antigravity hoặc Chrome DevTools MCP là “đã dùng” khi chưa trực tiếp kết nối với chúng. Các bước đẩy GitHub, đo PSI và sử dụng điện thoại thật chưa được xác nhận.

## 1. Yêu cầu ban đầu (System/Initial Prompt)

**Yêu cầu thật:** “Tao đang thi vibe code ... hãy đọc pdf rồi làm ... muốn ... đạt 10 điểm tuyệt đối và antigravity sao thêm mcp devtools để nó tự fix.”

**Phân tích yêu cầu từ PDF:** Website tự chọn chủ đề; `header`, `nav`, `main`, `section`/`article`, `footer`; CSS Variables trong `:root` và Flexbox/Grid; Animate.css, AOS, các trạng thái `:hover`/`:focus`; nhật ký prompt; GitHub repository công khai, đúng dạng `Ten_Ho_MSSV`, commit rõ ràng và GitHub Pages.

**Định hướng:** Landing page KAZE giới thiệu hành trình khám phá Nhật Bản; không dùng framework frontend, chỉ HTML5/CSS3, không có tập tin JavaScript tự viết (ngoại trừ phụ thuộc thư viện AOS bắt buộc theo đề).

## 2. Quá trình tinh chỉnh và giải quyết sự cố (Iterations)

### Lần 1 — Semantic HTML5 & CSS Variables

**Prompt kỹ thuật (biên tập từ mục tiêu):** Tạo cấu trúc `header > nav`, `main > section` và `footer`; headings đúng cấp, 3 bài giới thiệu điểm đến dùng `article`; tạo hệ biến cho màu sắc, typography, spacing, transition; dùng Grid cho bố cục chính và Flexbox cho nhóm điều hướng.

**Kết quả:** Giao diện đầu tiên có Hero, Điểm đến, Trải nghiệm, Lịch trình, Footer; có các thành phần ngữ nghĩa, CSS Variables, responsive.

**Nhận xét của sinh viên (phản hồi thật):** “Sao nhiều file ... pdf nó yêu cầu gì thì làm đó đừng sinh file dư thừa ... mobile có mấy mục nó quá dài ... tự kéo sang ...”.

**Tinh chỉnh:** Loại file QA/mẫu ảnh/README không bắt buộc khỏi thư mục nộp; tổ chức `index.html`, `style.css`, `PROMPT_LOG.md`, `assets/`; thiết kế thanh ảnh theo horizontal scroll + scroll-snap.

### Lần 2 — Animate.css, AOS và giao diện đẹp hơn

**Prompt kỹ thuật:** Tích hợp Animate.css 4.1.1 và AOS 2.3.4; Animate.css dùng cho hero headline/eyebrow/CTA; AOS dùng với sections; bổ sung CSS hover/focus; dùng chuyển động ngắn trên opacity/transform và giảm chuyển động theo tùy chọn hệ thống.

**Kết quả:** Trang có `animate__animated` và `animate__fadeInUp`/`fadeInDown`; các khối sử dụng `data-aos="fade-up"`; code kiểm tra AOS có tải hay không và tránh nội dung biến mất nếu thư viện không có.

**Vấn đề:** CDN thư viện không thể xác nhận qua mạng trong môi trường kiểm thử ngoại tuyến. Các ảnh bên ngoài cũng không bảo đảm tải, dù có fallback.

**Cách sửa:** Loại bỏ toàn bộ URL ảnh từ xa, tạo và nén ảnh WebP nội bộ. Giữ đường dẫn thư viện theo đúng yêu cầu và cần xác thực Network HTTP 200 trên máy có Internet khi đưa GitHub Pages.

### Lần 3 — Tái thiết kế lần thứ nhất chưa đạt thẩm mỹ

**Phản hồi thật:** “Giao diện quá xấu như asset nó xấu và giao diện đơn giản quá ... cải thiện thay đổi đổi mới giao diện ... speedpage phải trên 90.”

**Prompt kỹ thuật:** Đổi ảnh từ minh họa SVG phẳng sang ảnh phong cảnh giàu chiều sâu; nâng typography và hiệu ứng; giữ mã nguồn nhẹ, hướng tới PageSpeed Insights ≥90 (đây là mục tiêu nâng cao, không phải điểm số đã đo).

**Kết quả:** Bản KAZE ULTIMATE dùng hình ảnh Phú Sĩ và Kyoto, thêm các khu vực được thiết kế có chiều sâu. Tuy nhiên giao diện còn nhiều khối vuông và một số ảnh phụ còn lấy URL bên ngoài.

### Lần 4 — Redesign toàn diện, khắc phục ảnh trắng

**Phản hồi mới nhất, nguyên văn:** “Vẫn xấu quá bị khối và vuồn nhọn nhiều sáng tạo hơn ảnh vẫn bị lỗi k hiện sửa hoàn toàn giao diện”.

**Prompt kỹ thuật:** Không chỉ sửa CSS cũ. Dựng giao diện mới với khối ảnh mềm dạng organic/arch, khoảng trắng thông thoáng, typography editorial, các phần nội dung không đóng trong card vuông. Toàn bộ ảnh nội dung là file WebP nội bộ. Mobile dùng vuốt ngang cho dãy điểm đến, tab và timeline. Không dùng URL ảnh không ổn định.

**Kết quả:** Viết lại HTML/CSS/JS. Hero là ảnh Kyoto dạng đường cong tự do; điểm đến dùng ảnh mái vòm lệch nhịp; câu chuyện có ảnh Phú Sĩ lớn; Trải nghiệm thay nội dung bằng tab; Lịch trình 3/5/7 ngày chuyển động theo timeline ngang. Thực hiện tối ưu 4 ảnh WebP trong `assets/`.

**Debug thực tế:** Kiểm thử viewport bằng Chromium/Playwright phát hiện riêng kích thước 320px có `scrollWidth` lớn hơn màn hình do header chứa quá nhiều nút. Sửa bằng media query ở breakpoint dưới 360px để chỉ giữ logo + menu hamburger. Sau đó chạy lại test.

### Lần 5 — Sửa lỗi nghiêm trọng dấu tiếng Việt và typography trên Windows (21/10/2026)

**Phản hồi thật của người dùng:** “Lỗi font chữ nghiêm trọng”, kèm năm ảnh chụp Chrome trên Windows cho thấy dấu tiếng Việt và chữ tiêu đề bị lệch/tách bất thường (ví dụ các tiêu đề “Đi thật xa. Để thấy lòng mình gần hơn.” và “Bạn muốn Nhật Bản trông như thế nào?”).

**Phân tích mã nguồn:** CSS trước đó dùng font display `Georgia` và nén ký tự mạnh (`letter-spacing: -.085em`), dòng cao chỉ `.98`; các dấu tiếng Việt có thể bị quá sát hoặc hiển thị không đồng nhất do fallback font trên thiết bị khác nhau. HTML và JS được kiểm tra ở chuẩn Unicode NFC, không phát hiện ký tự dấu tổ hợp lẫn vào văn bản.

**Prompt sửa lỗi (diễn đạt lại chỉ thị thực tế):** Kiểm tra lỗi typography từ ảnh người dùng; bỏ phụ thuộc Georgia; dùng font fallback quen thuộc có hỗ trợ tiếng Việt trên Windows, Linux/Android; hạ mức letter-spacing âm, tăng line-height và điều chỉnh kích cỡ H1/H2; không thêm file thừa vào repo. Kiểm tra ảnh chụp với kích thước desktop/mobile và lỗi tràn ngang.

**Thay đổi:** `--font-display` trở thành `Cambria, 'Noto Serif', 'Times New Roman', serif`; giảm mạnh letter-spacing âm ở các tiêu đề; tăng line-height lên khoảng 1.18–1.2; điều chỉnh `clamp()` cho các headline và thêm quy tắc chống tách từ sai (`word-break: normal`, `hyphens: none`). Không bổ sung font binary hay thư viện mới.

**Kiểm tra:** Chạy Chromium/Playwright với nội dung HTML, CSS và ảnh nội bộ được nạp trong bộ nhớ tại 20 độ rộng viewport từ 320px đến 2560px do môi trường hạn chế điều hướng địa chỉ `file://` và `localhost`. Không ghi nhận tràn ngang của trang, tràn phần tử heading hoặc lỗi JavaScript trong lượt kiểm tra. Đã đối chiếu ảnh render hero và mục Trải nghiệm ở 320/390/768/1440px. Đây **không phải** kiểm thử thực tế trên Windows hay kết quả PageSpeed Insights từ URL công khai; người dùng cần giải nén toàn bộ ZIP và kiểm tra trên Chrome Windows trước khi nộp.

### Lần 7 — Loại bỏ mã JavaScript tự viết, chuyển điều khiển sang HTML/CSS

**Yêu cầu thật:** “Hãy làm làm đi đề k yêu cầu dùng js đâu hãy bỏ đi”.

**Xử lý:** Xóa `script.js`; menu điều hướng dùng CSS `:target`; Trải nghiệm và Lịch trình 3/5/7 ngày dùng các lựa chọn radio gốc HTML kết hợp CSS `:checked`/`:has()`; danh sách ảnh và lịch trình cuộn ngang bằng `overflow-x:auto` và `scroll-snap`. Bỏ chức năng lưu `localStorage` vì phụ thuộc JavaScript, thay bằng liên kết khám phá thực sự hoạt động; không để nút bấm vô hiệu.

**Lưu ý yêu cầu PDF:** AOS là thư viện bắt buộc có lõi JavaScript; vì thế vẫn nạp AOS từ CDN và dùng một lệnh `AOS.init(...)` ngay trong thuộc tính `onload` của thẻ script thư viện. Không có logic JavaScript do dự án tự viết và không còn file `.js` trong gói nộp. Animate.css vẫn được áp dụng trên hero, CSS hover/focus và Semantic HTML5 giữ nguyên.

## 3. Đánh giá cá nhân về quá trình Vibe Coding

**AI giúp tiết kiệm thời gian nhất ở đâu?** Tạo khung ngữ nghĩa HTML5, xây dựng hệ CSS Variables, triển khai responsive theo nhiều kích thước, thiết kế tab/timeline không cần JavaScript riêng và tự động hóa các vòng kiểm tra lỗi.

**Bài học khi viết prompt:** “Thiết kế đẹp” là yêu cầu quá chung chung. Cần chỉ rõ những điều không được phép (ảnh từ xa hỏng, khối vuông lặp lại, mobile kéo quá dài), tiêu chí có thể kiểm tra (ảnh tải thành công, không tràn ngang, tương tác thật), giới hạn công nghệ và chất lượng trải nghiệm. Điều khiển AI là quá trình nhiều lượt thử–nhận xét–sửa, không phải chỉ một prompt duy nhất.

**Cần tự kiểm tra trước khi nộp:** Tên và MSSV, tên GitHub repo đúng cú pháp, commit thật, GitHub Pages hoạt động, AOS/Animate.css tải thành công qua mạng và PageSpeed Insights trên URL public. Không ghi các việc này là “đã đạt” khi chưa hoàn thành.
