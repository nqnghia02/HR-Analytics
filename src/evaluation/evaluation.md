# NHẬN XÉT KẾT QUẢ TEST SET

## I. Bảng tổng hợp Metric (Test Set)

| Metric                 | Logistic | Random Forest | SVM   | XGBoost | LightGBM | CatBoost |
|------------------------|----------|----------------|-------|---------|----------|----------|
| Support                | 39       | 39             | 39    | 39      | 39       | 39       |
| Precision (Attrition)  | 0.340    | 0.419          | 0.429 | 0.273   | 0.242    | 0.301    |
| Recall (Attrition)     | 0.462    | 0.333          | 0.154 | 0.615   | 0.564    | 0.641    |
| F1-Score               | 0.391    | 0.371          | 0.226 | 0.378   | 0.338    | 0.410    |
| AUC-ROC                | 0.741    | 0.728          | 0.734 | 0.756   | 0.709    | 0.712    |

## II. Với từng mô hình

### 1. Logistic Regression

#### a. Đánh giá
- Mô hình có khả năng phân biệt tương đối (ROC AUC = 0.741), nhưng hiệu suất dự đoán lớp thiểu số (Attrition = 1) còn thấp  
- F1-score cho lớp 1: Chỉ 0.39, cho thấy sự cân bằng giữa Precision và Recall chưa tốt.  
- Precision thấp (0.34): Khi mô hình dự đoán "Attrition", chỉ 34% là đúng (nhiều false positives).  
- Recall trung bình (0.46): Mô hình chỉ phát hiện được 46% trường hợp Attrition thực tế.
  False Positive (FP) là trường hợp mô hình dự đoán sai một nhân viên sẽ nghỉ việc Attrition = "Có" nhưng thực tế họ không nghỉ Attrition = "Không", gây cảnh báo sai và lãng phí nguồn lực.
  False Negative (FN) là trường hợp mô hình dự đoán sai một nhân viên sẽ không nghỉ việc Attrition = "Không" nhưng thực tế họ đã nghỉ Attrition = "Có", gây bỏ sót đối tượng cần quan tâm.

#### b. Biểu đồ
- ROC Curve (AUC = 0.741): Đường cong nằm trên đường chéo ngẫu nhiên, chứng tỏ mô hình có giá trị dự đoán, nhưng chưa lý tưởng (AUC > 0.9 mới là tốt).  
- Precision-Recall Curve: Precision giảm mạnh khi Recall tăng, phản ánh sự đánh đổi rõ rệt: Muốn bắt nhiều Attrition (Recall cao) thì phải chấp nhận nhiều dự đoán sai (Precision thấp).  

#### c. Kết luận
- Để tránh bỏ sót nhân viên nghỉ việc (Recall cao), cần chấp nhận nhiều cảnh báo sai (Precision thấp).  
- Nếu ưu tiên tránh dự đoán sai (Precision cao), sẽ bỏ sót nhiều trường hợp thực tế.  
- Mô hình hiện tại phù hợp để sàng lọc ban đầu nhưng chưa đủ tin cậy để ra quyết định quan trọng.  
- Cần ưu tiên cải thiện Recall nếu mục tiêu là phát hiện sớm nhân viên có nguy cơ nghỉ việc.  

---

### 2. Random Forest

#### a. Đánh giá
- ROC AUC (0.728): Thấp hơn so với Logistic Regression (0.741), cho thấy khả năng phân biệt giữa hai lớp không tốt như kỳ vọng với Random Forest.  
- F1-score (0.371): Thấp hơn Logistic Regression (0.391), đặc biệt ở lớp thiểu số (Attrition = 1), cho thấy mô hình không cải thiện được sự cân bằng giữa Precision và Recall.  
- Precision (0.419) vs Recall (0.333): Mô hình có độ chính xác tương đối khi dự đoán Attrition (41.9% đúng), nhưng bỏ sót nhiều trường hợp thực tế (chỉ phát hiện 33.3%).  

#### b. Biểu đồ
- ROC Curve:  
  • AUC = 0.728 (< 0.8) cho thấy mô hình chỉ phân loại tốt hơn ngẫu nhiên một chút.  
  • Đường cong gần đường chéo ngẫu nhiên, phản ánh khả năng phân biệt yếu giữa hai lớp.  
- Precision-Recall Curve: Precision giảm nhanh khi Recall tăng thì phải chấp nhận nhiều dự đoán sai.  

#### c. Kết luận
- Mô hình Random Forest hiện tại không hiệu quả hơn Logistic Regression trong việc dự đoán Attrition, dù đáng lẽ phải mạnh hơn.  

---

### 3. Support Vector Machine (SVM)

#### a. Đánh giá
- ROC AUC (0.7337): Tương đương Logistic Regression (0.741) và Random Forest (0.728), nhưng không cải thiện được khả năng phân biệt giữa hai lớp.  
- F1-score (0.226): Thấp nhất trong 3 mô hình (Logistic: 0.391, RF: 0.371), cho thấy SVM kém hiệu quả trong việc cân bằng Precision và Recall cho lớp Attrition.  
- Precision (0.429) vs Recall (0.154):  
  • Precision tương đối cao: Khi SVM dự đoán Attrition, 42.9% là đúng.  
  • Recall cực thấp: Chỉ phát hiện được 15.4% trường hợp Attrition thực tế.  

#### b. Biểu đồ
- ROC Curve:  
  • AUC ~0.73 nằm dưới ngưỡng 0.8. Khả năng phân loại chỉ tốt hơn ngẫu nhiên một chút.  
  • Đường cong không gần góc trên bên trái. Hạn chế trong phân biệt lớp Attrition.  
- Precision-Recall Curve:  
  • Precision cao nhưng Recall rất thấp. Chỉ dự đoán Attrition khi rất chắc chắn, dẫn đến bỏ sót nhiều trường hợp.  

#### c. Kết luận
- SVM kém hiệu quả nhất trong việc phát hiện Attrition, không phù hợp cho bài toán trong trường hợp, đặc biệt về Recall.  

---

### 4. XGBoost

#### a. Đánh giá
- ROC AUC (0.7556): Cao nhất trong các mô hình đã thử (Logistic Regression: 0.741, Random Forest: 0.728, SVM: 0.734), cho thấy khả năng phân biệt tốt hơn giữa hai lớp.  
- F1-score (0.378): Cao hơn SVM (0.226) và Random Forest (0.371), nhưng vẫn thấp hơn Logistic Regression (0.391).  
- Recall (0.615) vs Precision (0.273):  
  • Recall cao nhất: XGBoost phát hiện được 61.5% trường hợp Attrition thực tế (tốt hơn hẳn các mô hình trước).  
  • Precision thấp: Chỉ 27.3% dự đoán Attrition là chính xác.  

#### b. Biểu đồ
- ROC Curve:  
  • AUC = 0.7556 (>0.7) cho thấy mô hình có khả năng phân loại tuy chưa xuất sắc nhưng vẫn chấp nhận được, ổn.  
  • Đường cong nằm trên các mô hình khác. XGBoost vượt trội hơn về mặt phân biệt lớp.  
- Precision-Recall Curve: Precision giảm mạnh khi Recall tăng. Recall cao nhiều dự đoán sai.  

#### c. Kết luận
- Ưu điểm:  
  • Recall cao nhất (61.5%), phù hợp cho bài toán ưu tiên không bỏ sót nhân viên có nguy cơ nghỉ việc.  
  • AUC cao nhất (0.756), chứng tỏ khả năng phân loại vượt trội.  
- Hạn chế:  
  • Precision thấp (27.3%) Nhiều cảnh báo sai, có thể gây nhầm lẫn không đáng có ảnh hưởng đến nguồn tài nguyên nhân lực.  

---

### 5. LightGBM

#### a. Đánh giá
- ROC AUC (0.709): Thấp hơn XGBoost (0.756) và Logistic Regression (0.741), cho thấy khả năng phân biệt kém hơn giữa hai lớp.  
- F1-score (0.338): Thấp hơn cả XGBoost (0.378) và Logistic Regression (0.391), đặc biệt ở lớp thiểu số (Attrition = 1).  
- Recall (0.564) vs Precision (0.242):  
  • Recall tương đối tốt: Phát hiện được 56.4% trường hợp Attrition thực tế (cao hơn Random Forest và SVM).  
  • Precision rất thấp: Chỉ 24.2% dự đoán Attrition là chính xác nghĩa là sẽ đưa ra nhiều dự đoán sai cho Attrition thực tế.  

#### b. Biểu đồ
- ROC Curve:  
  • AUC = 0.709 (<0.8). Khả năng phân loại chỉ tốt hơn ngẫu nhiên một chút.  
  • Đường cong gần đường chéo ngẫu nhiên. Hạn chế trong phân biệt lớp Attrition.  
- Precision-Recall Curve: Precision thấp dù Recall trung bình. Mô hình chấp nhận quá nhiều dự đoán sai để đạt Recall.  
- LightGBM dù có scale_pos_weight để điều chỉnh trọng số nhưng vẫn bị ảnh hưởng bởi imbalance.  

#### c. Kết luận
- Ưu điểm duy nhất: Recall tương đối tốt (56.4%), phù hợp nếu ưu tiên không bỏ sót nhân viên nghỉ việc.  
- Hạn chế: Precision quá thấp (24.2%) nhiều cảnh báo sai, gây lãng phí nguồn lực.  
- AUC thấp nhất trong các mô hình đã thử.  

---

### 6. CatBoost

#### a. Đánh giá
- F1-score (0.410): Cao nhất trong các mô hình đã thử (XGBoost: 0.378, LightGBM: 0.338, Logistic Regression: 0.391), cho thấy khả năng cân bằng tốt hơn giữa Precision và Recall.  
- Recall (0.641): Tốt nhất trong tất cả mô hình, phát hiện được 64.1% trường hợp Attrition thực tế.  
- Precision (0.301): Thấp hơn Logistic Regression (0.340), nhưng chấp nhận được khi Recall cao.  
- ROC AUC (0.7116): Tương đương LightGBM (0.709), nhưng thấp hơn XGBoost (0.756). Điều này cho thấy CatBoost tập trung vào cải thiện Recall hơn là phân biệt tổng thể (AUC).  

#### b. Biểu đồ
- ROC Curve (AUC = 0.7116): Đường cong nằm trên đường chéo ngẫu nhiên nhưng chưa sát góc trên bên trái. Khả năng phân loại chưa xuất sắc nhưng chấp nhận được, khá ổn.  
- Precision-Recall Curve: Precision giảm khi Recall tăng, chấp nhận giảm precision để cải thiện recall. Tuy CatBoost duy trì Recall cao hơn mà không làm Precision tệ hơn các mô hình khác.  

#### c. Kết luận
- Xử lý lớp thiểu số (yes) tốt nhất  
- Là lựa chọn hợp lý trong các mô hình đã thử (F1-score 0.41, Recall 64.1%), phù hợp khi ưu tiên phát hiện sớm nhân viên có nguy cơ nghỉ việc, nhưng vẫn phải nhận một số cảnh báo sai (Precision chỉ 30.1%).  
