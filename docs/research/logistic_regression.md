# Tìm hiểu Hồi quy Logistic

## 1. Khái niệm và mục đích cốt lõi
- **Hồi quy Logistic là gì?**
  - Hồi quy Logistic là một thuật toán phân loại (classification algorithm) thuộc nhóm học máy có giám sát (supervised learning). Mặc dù tên gọi có chữ "hồi quy" (regression), nhưng nó được dùng để dự đoán loại của một đối tượng, không phải một giá trị liên tục.
  - **Mục tiêu chính**: Ước tính xác suất mà một trường hợp cụ thể thuộc về một trong các danh mục rời rạc (thường là 0 hoặc 1, "có" hoặc "không", "đúng" hoặc "sai").
- **Tại sao lại là "Logistic"?**
  - Tên gọi này xuất phát từ việc nó sử dụng hàm Sigmoid (còn gọi là hàm Logistic function) để ánh xạ đầu ra của một mô hình tuyến tính về một giá trị xác suất trong khoảng [0, 1].

## 2. Cơ chế hoạt động (Toán học đằng sau)
- **Bước 1: Mô hình tuyến tính (Linear Combination)**  
  - Giống như hồi quy tuyến tính, Logistic Regression bắt đầu bằng việc tính tổng có trọng số của các biến đầu vào:  
    ```
    z = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ
    ```
    Hoặc dưới dạng vector:  
    ```
    z = WᵀX + b
    ```
    Trong đó:
    - Xᵢ: các biến độc lập (features).
    - βᵢ (hoặc W, b): các hệ số (weights và bias) mà mô hình sẽ học trong quá trình huấn luyện.
- **Bước 2: Ánh xạ qua hàm Sigmoid**  
  - Giá trị z có thể là bất kỳ số thực nào (−∞ đến +∞). Để biến z thành một xác suất (giá trị trong khoảng [0, 1]), chúng ta sử dụng hàm Sigmoid:  
    ```
    ŷ = P(Y=1|X) = 1 / (1 + e⁻ᶻ) = 1 / (1 + e⁻(WᵀX + b))
    ```
    - ŷ chính là xác suất dự đoán rằng đầu ra là lớp 1 (hoặc "có", "đúng", v.v.).
- **Bước 3: Hàm mất mát (Loss Function - Cross-Entropy/Log Loss)**  
  - Để huấn luyện mô hình, chúng ta cần một cách để đo lường mức độ "sai" của các dự đoán. Logistic Regression sử dụng hàm Cross-Entropy Loss:  
    ```
    J(θ) = - (1/m) ∑ [y⁽ᵢ⁾log(ŷ⁽ᵢ⁾) + (1 - y⁽ᵢ⁾)log(1 - ŷ⁽ᵢ⁾)]
    ```
    Trong đó:
    - m: số lượng mẫu huấn luyện.
    - y⁽ᵢ⁾: nhãn thực tế của mẫu thứ i (0 hoặc 1).
    - ŷ⁽ᵢ⁾: xác suất dự đoán của mẫu thứ i bởi mô hình.
    - Mục tiêu là tìm các hệ số θ (gồm W và b) sao cho J(θ) được tối thiểu hóa.
- **Bước 4: Tối ưu hóa (Optimization - Gradient Descent)**  
  - Để tìm các hệ số tối ưu, chúng ta sử dụng các thuật toán tối ưu hóa như Gradient Descent (hoặc các biến thể của nó như Stochastic Gradient Descent, Adam, v.v.).
  - Gradient Descent điều chỉnh các hệ số θ lặp đi lặp lại theo hướng ngược lại với gradient của hàm mất mát, nhằm tìm điểm cực tiểu.

## 3. Quyết định phân loại (Classification Decision)
- Sau khi mô hình được huấn luyện và đưa ra xác suất ŷ, chúng ta cần một ngưỡng (threshold) để đưa ra quyết định phân loại cuối cùng.
- **Ngưỡng mặc định thường là 0.5**:
  - Nếu ŷ ≥ 0.5, dự đoán là lớp 1.
  - Nếu ŷ < 0.5, dự đoán là lớp 0.
- Ngưỡng này có thể được điều chỉnh tùy thuộc vào yêu cầu cụ thể của bài toán (ví dụ: nếu bạn muốn giảm thiểu lỗi False Negative, bạn có thể chọn một ngưỡng thấp hơn).

## 4. Các loại Logistic Regression
- **Hồi quy Logistic nhị phân (Binary Logistic Regression)**: Phổ biến nhất, cho các bài toán 2 lớp (ví dụ: Yes/No, True/False, Spam/Not Spam).
- **Hồi quy Logistic đa thức (Multinomial Logistic Regression)**: Khi có 3 hoặc nhiều hơn các lớp đầu ra không có thứ tự (ví dụ: Phân loại loại trái cây: Táo, Cam, Chuối).
- **Hồi quy Logistic thứ tự (Ordinal Logistic Regression)**: Khi có 3 hoặc nhiều hơn các lớp đầu ra có thứ tự (ví dụ: Đánh giá chất lượng sản phẩm: Kém, Trung bình, Tốt).

## 5. Giả định của Logistic Regression
- **Phụ thuộc biến mục tiêu là rời rạc**: Biến phụ thuộc phải là biến nhị phân hoặc biến danh nghĩa (nominal) trong trường hợp đa thức.
- **Độc lập các quan sát**: Các quan sát (dòng dữ liệu) phải độc lập với nhau.
- **Không có đa cộng tuyến nghiêm trọng**: Các biến độc lập không nên có mối tương quan quá cao với nhau. Đa cộng tuyến có thể làm cho các hệ số mô hình không ổn định.
- **Mối quan hệ tuyến tính giữa các biến độc lập và log-odds**: Đây là một giả định quan trọng. Mặc dù Logistic Regression không yêu cầu mối quan hệ tuyến tính giữa biến độc lập và xác suất của biến phụ thuộc, nhưng nó yêu cầu mối quan hệ tuyến tính giữa các biến độc lập và logarit của tỷ lệ cược (log-odds hay logit).  
  ```
  log[P(Y=1|X) / (1 - P(Y=1|X))] = WᵀX + b
  ```
- **Kích thước mẫu đủ lớn**: Để ước tính các hệ số một cách chính xác, cần có đủ số lượng quan sát.

## 6. Khi nào nên sử dụng Logistic Regression?
- Khi bạn cần dự đoán xác suất một sự kiện xảy ra.
- Khi biến mục tiêu của bạn là rời rạc (phân loại), đặc biệt là nhị phân.
- Khi bạn muốn một mô hình dễ hiểu và có khả năng diễn giải (interpretability) cao.
- Khi dữ liệu của bạn có mối quan hệ tuyến tính với log-odds.
- Làm mô hình cơ sở để so sánh với các mô hình phức tạp hơn.

## 7. Các bước thực hiện (Workflow chung)
1. **Thu thập và làm sạch dữ liệu**: Đảm bảo dữ liệu chất lượng.
2. **Khám phá dữ liệu (EDA)**: Hiểu rõ các đặc trưng và mối quan hệ.
3. **Tiền xử lý dữ liệu**:
   - Xử lý thiếu giá trị.
   - Mã hóa biến phân loại (One-Hot Encoding, Label Encoding).
   - Chuẩn hóa/co giãn dữ liệu (Standardization/Normalization) để giúp Gradient Descent hội tụ nhanh hơn.
4. **Phân chia dữ liệu**: Chia thành tập huấn luyện (training set) và tập kiểm tra (test set).
5. **Huấn luyện mô hình**: Sử dụng tập huấn luyện để tối thiểu hóa hàm mất mát và tìm các hệ số.
6. **Đánh giá mô hình**: Sử dụng tập kiểm tra để đánh giá hiệu suất. Các chỉ số thường dùng:
   - Accuracy (Độ chính xác).
   - Precision (Độ chính xác).
   - Recall (Độ nhạy).
   - F1-Score.
   - ROC Curve và AUC (Area Under the Curve) - đặc biệt hữu ích cho bài toán phân loại nhị phân.
   - Confusion Matrix.
7. **Điều chỉnh siêu tham số (Hyperparameter Tuning)**: Cải thiện hiệu suất mô hình (ví dụ: điều chỉnh tốc độ học, tham số Regularization).

## 8. Ví dụ trực quan
Hãy tưởng tượng bạn muốn dự đoán liệu một sinh viên có đậu kỳ thi hay không (Đậu/Trượt) dựa trên số giờ học.
- **Trục X**: Số giờ học (liên tục).
- **Trục Y**: Xác suất đậu (0 đến 1).
- Logistic Regression sẽ không vẽ một đường thẳng chia đôi điểm (như Linear Regression làm cho dự đoán giá trị liên tục), mà nó sẽ vẽ một đường cong S (hàm Sigmoid) biểu diễn xác suất đậu.
- Nếu xác suất > 0.5, dự đoán là Đậu.
- Nếu xác suất < 0.5, dự đoán là Trượt.