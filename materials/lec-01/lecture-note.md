# Bài 01: Tổng quan Khai phá dữ liệu & Mô hình thuật toán

Tài liệu tự học chi tiết cho Bài 01 học phần **Khai phá dữ liệu (Data Mining)**. Slide bài giảng tương ứng: [lecture-01-tong-quan-khai-pha-du-lieu.html](lecture-01-tong-quan-khai-pha-du-lieu.html).

<!-- note-topic-id: lec-01-topic-intro -->
## 1. Giới thiệu và bài toán dữ liệu lớn

Trong thời đại số hóa, khối lượng dữ liệu phát sinh từ mạng xã hội, thiết bị cảm biến (IoT), giao dịch thương mại điện tử và tài liệu web đang tăng trưởng theo cấp số nhân. Tuy nhiên, dữ liệu thô tự nó không mang lại giá trị trực tiếp nếu chúng ta không thể chuyển hóa thành tri thức và thông tin hữu ích hỗ trợ ra quyết định.

::: definition Định nghĩa 01.1 (Khai phá dữ liệu)
**Khai phá dữ liệu (Data Mining)** là quá trình tự động hoặc bán tự động khám phá các mẫu (patterns), quy luật và mối liên hệ tiềm ẩn, có ý nghĩa, mới mẻ và có khả năng ứng dụng thực tế từ các tập dữ liệu có quy mô rất lớn.
:::

Quy trình phát hiện tri thức trong cơ sở dữ liệu (KDD) bao gồm các giai đoạn chuẩn hóa:
1. Thu thập và làm sạch dữ liệu (Data Cleaning).
2. Tích hợp dữ liệu từ các nguồn không đồng nhất (Data Integration).
3. Lựa chọn và chuyển đổi dữ liệu (Data Selection & Transformation).
4. Áp dụng thuật toán khai phá dữ liệu (Data Mining Algorithms).
5. Đánh giá mẫu và trực quan hóa tri thức (Pattern Evaluation & Knowledge Presentation).

<!-- note-topic-id: lec-01-topic-bonferroni -->
## 2. Nguyên lý Bonferroni và Hiện tượng Mẫu giả

Khi khai phá trên tập dữ liệu quy mô khổng lồ, một nguy cơ cố hữu là tìm thấy các mẫu xuất hiện hoàn toàn ngẫu nhiên nhưng lại mang vẻ bề ngoài của một quy luật đáng chú ý.

::: theorem Định lý 01.1 (Bất đẳng thức Boole - Giới hạn Bonferroni)
Cho một họ các biến cố $E_1, E_2, \dots, E_m$. Xác suất để ít nhất một biến cố xảy ra bị chặn trên bởi tổng xác suất của từng biến cố:
$$\mathbb{P}\left(\bigcup_{i=1}^m E_i\right) \le \sum_{i=1}^m \mathbb{P}(E_i)$$
Nếu mỗi biến cố có xác suất rất nhỏ $\mathbb{P}(E_i) \le \alpha$, thì xác suất xảy ra ít nhất một biến cố sai lệch thỏa mãn:
$$\mathbb{P}(\text{Ít nhất một sự kiện ngẫu nhiên}) \le m \cdot \alpha$$
:::

::: example Ví dụ 01.1 (Theo dõi hành vi đáng ngờ)
Giả sử một cơ quan an ninh theo dõi $10^9$ người dân. Giả thiết mỗi người độc lập ngẫu nhiên ghé một khách sạn nhất định vào một ngày bất kỳ với xác suất $p = 10^{-6}$.
Số cặp người dân là $\binom{10^9}{2} \approx 5 \times 10^{17}$.
Xác suất hai người bất kỳ tình cờ cùng xuất hiện tại một khách sạn vào cùng một ngày là $p^2 = 10^{-12}$.
Kỳ vọng số cặp vô tội cùng ở khách sạn vào ngày đó là:
$$\mathbb{E}[\text{Số cặp trùng hợp}] \approx 5 \times 10^{17} \times 10^{-12} = 500{,}000 \text{ cặp}$$
Do đó, việc chỉ dựa vào sự trùng lặp đơn thuần mà kết luận hai người có liên hệ sẽ dẫn đến nửa triệu trường hợp báo động giả (False Positives).
:::

<!-- note-topic-id: lec-01-topic-tasks -->
## 3. Các bài toán trọng tâm trong khóa học

Trong các bài tiếp theo, chúng ta sẽ lần lượt nghiên cứu các giải thuật nền tảng:

::: algorithm Thuật toán 01.1 (Khung tổng quát phân tích mẫu phổ biến)
- **Đầu vào:** Cơ sở dữ liệu giao dịch $D = \{T_1, T_2, \dots, T_n\}$, ngưỡng hỗ trợ tối thiểu $s \in (0, 1]$.
- **Đầu ra:** Toàn bộ các tập mục $X$ sao cho tần suất xuất hiện $\text{supp}(X) \ge s \cdot n$.
- **Nguyên lý suy giảm Apriori:** Mọi tập con của một tập mục phổ biến đều phải là tập mục phổ biến.
:::

<!-- note-topic-id: lec-01-topic-exercises -->
## 4. Bài tập tự kiểm tra

::: exercise Bài tập 01.1
Cho tập dữ liệu gồm $N = 10^7$ văn bản. Giả sử ta muốn tìm tất cả các cặp văn bản có độ tương đồng Jaccard lớn hơn $0.8$.
1. Tính số phép so sánh trực tiếp nếu so sánh vét cạn mọi cặp.
2. Với giả định mỗi phép so sánh tốn 1 micro giây ($10^{-6}$ giây), hệ thống cần bao lâu để hoàn thành phép vét cạn?
:::

::: hint Gợi ý
Số cặp là tổ hợp chập 2 của $N$: $\binom{N}{2} = \frac{N(N-1)}{2}$. Áp dụng công thức nhân thời gian để ra số ngày hoặc số năm cần tính.
:::

::: solution Lời giải
1. Số cặp cần so sánh:
   $$\binom{10^7}{2} = \frac{10^7 \times (10^7 - 1)}{2} \approx 5 \times 10^{13} \text{ phép so sánh}$$
2. Tổng thời gian thực thi:
   $$T = 5 \times 10^{13} \times 10^{-6} \text{ s} = 5 \times 10^7 \text{ s} \approx 578.7 \text{ ngày} \approx 1.58 \text{ năm}$$
Kết quả này cho thấy giải thuật duyệt vét cạn hoàn toàn bất khả thi trong thực tế và đòi hỏi kỹ thuật lọc ứng viên gần đúng như MinHash và LSH (sẽ học trong Bài 04 & 05).
:::
