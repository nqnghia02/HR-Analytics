## BÀI TÌM HIỂU VỀ RANDOM FOREST
## I. Giới thiệu về Random Forest
Random Forest (Rừng Ngẫu Nhiên) là một thuật toán học máy thuộc nhóm Ensemble Learning, kết hợp nhiều cây quyết định (Decision Trees) để tạo ra mô hình mạnh mẽ hơn so với một cây đơn lẻ, được sử dụng rộng rãi trong cả phân loại (classification) và hồi quy(regression). Thuật toán được đề xuất bởi Leo Breiman vào năm 2001 và được ứng dụng rộng rãi trong cả phân loại (classification) và hồi quy(regression). Random Forest có thể phân nhóm dữ liệu vào các lớp (categories) dựa trên các đặc trưng (features).
Ưu điểm
- Giảm overfitting nhờ kết hợp nhiều cây.
- Xử lý tốt dữ liệu nhiễu và missing values.
- Không cần chuẩn hóa dữ liệu.
- Có thể đo lường độ quan trọng của từng đặc trưng (feature importance).
Nhược điểm
- Tốc độ chậm hơn so với các mô hình đơn giản (do phải xây dựng nhiều cây).
- Khó giải thích hơn Decision Tree đơn lẻ.

## II. Nguyên lý hoạt động
Random Forest hoạt động dựa trên hai kỹ thuật chính:
1.	Bootstrap Aggregating (Bagging): Tạo nhiều tập con dữ liệu bằng cách lấy mẫu ngẫu nhiên có hoàn lại.
2.	Tính ngẫu nhiên trong lựa chọn đặc trưng: Mỗi cây chỉ sử dụng một tập con ngẫu nhiên các đặc trưng để phân chia.
Thuật toán
1.	Tạo Bootstrap Samples:
- Với mỗi cây, chọn ngẫu nhiên n mẫu từ tập dữ liệu gốc (có thể trùng lặp).
2.	Xây dựng cây quyết định:
-Tại mỗi node, chọn ngẫu nhiên k đặc trưng từ tổng số m đặc trưng (k << m, thường k = √m).
-Chọn đặc trưng tốt nhất (dựa trên Gini/Entropy cho phân loại hoặc MSE cho hồi quy) để phân chia.
3.	Lặp lại để xây dựng n cây.
4.	Tổng hợp kết quả:
-Phân loại: Majority voting (lấy nhãn được chọn nhiều nhất).
Hồi quy: Giá trị trung bình của các cây.
## III. Các tham số cần chú trọng
n_estimators : Số lượng cây trong rừng. Càng nhiều cây càng tốt nhưng chậm hơn. Giá trị mặc định là 100.
max_depth : Độ sâu tối đa của mỗi cây. Nếu “None”, cây phát triển đến khi không thể chia. Giá trị mặc định là None.
min_samples_split : Số mẫu tối thiểu để phân chia một node. Giá trị mặc định là 2.
min_sample_leaf : Số mẫu tối thiểu ở lá. Giá trị mặc định là 1.
max_features : Số đặc trưng tối đa được xem xét tại mỗi node (“sqrt”, “log2”, hoặc số cụ thể). Giá trị mặc định là “sqrt”.
Bootstrao : Có lấy mẫu ngẫu nhiên với replacement hay không. Giá trị mặc định là True.

## IV. Ví dụ minh họa bằng Python
1. Phân loại (Classification)
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

#Load dữ liệu
iris = load_iris()
X, y = iris.data, iris.target

#Chia tập train/test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

#Huấn luyện mô hình
model = RandomForestClassifier(
    n_estimators=100,
    max_depth=3,
    max_features='sqrt'
)
model.fit(X_train, y_train)

#Đánh giá
print("Accuracy:", model.score(X_test, y_test))
2. Hồi quy (Regression)
from sklearn.ensemble import RandomForestRegressor
from sklearn.datasets import fetch_california_housing
from sklearn.metrics import mean_squared_error

#Load dữ liệu
data = fetch_california_housing()
X, y = data.data, data.target

#Huấn luyện mô hình
model = RandomForestRegressor(n_estimators=100, random_state=42)
model.fit(X, y)

#Dự đoán
y_pred = model.predict(X)
print("MSE:", mean_squared_error(y, y_pred))
3. Đánh giá độ quan trọng của đặc trưng
import pandas as pd
import matplotlib.pyplot as plt

#Lấy độ quan trọng các đặc trưng
importance = pd.Series(model.feature_importances_, index=data.feature_names)
importance.sort_values().plot(kind='barh')
plt.title("Feature Importance")
plt.show()
________________________________________
## V. So sánh với các thuật toán khác
Thuật toán	                       Ưu điểm	                                     Nhược điểm
Decision Tree	                     Dễ hiểu, nhanh	                               Dễ overfitting
Random Forest	                     Giảm overfitting, độ chính xác cao	           Chậm, khó giải thích
XGBoost	                           Tốc độ nhanh, hiệu suất cao	                 Cần điều chỉnh nhiều tham số
________________________________________
## VI. Ứng dụng thực tế
-	Phân loại: Nhận diện chữ viết tay, spam email, chẩn đoán bệnh.
-	Hồi quy: Dự đoán giá nhà, giá cổ phiếu.
-	Feature Selection: Đánh giá mức độ quan trọng của các biến đầu vào.
________________________________________
## VII. Kết luận
Random Forest là một trong những thuật toán mạnh mẽ và linh hoạt nhất trong học máy nhờ:
-	Khả năng xử lý dữ liệu phức tạp.
-	Dễ sử dụng và ít cần tiền xử lý dữ liệu.
-	Ứng dụng rộng rãi từ phân loại, hồi quy đến khám phá dữ liệu.
Có thể áp dụng Random Forest cho hầu hết các bài toán với dữ liệu có cấu trúc (structured data). 
## Ví dụ Đơn Giản Về Random Forest
Để hiểu rõ cách Random Forest hoạt động, ta sẽ làm một ví dụ tính toán thủ công trên bộ dữ liệu cực nhỏ.
 "Bạn có nên đi picnic hôm nay không?"
Giả sử bạn cần quyết định có nên đi picnic dựa trên 3 yếu tố:
1.	Thời tiết (Nắng, Mưa, Âm u)
2.	Nhiệt độ (Nóng, Ấm, Mát)
3.	Gió (Có gió, Không gió)
Bạn hỏi ý kiến 3 người bạn (tương đương 3 cây trong rừng). Mỗi người chỉ quan tâm đến 2/3 yếu tố (tính ngẫu nhiên của Random Forest).
________________________________________
Bước 1: Thu thập "Dữ liệu"
Ngày	       Thời tiết	    Nhiệt độ	      Gió	          Đi picnic? (Target)
1	           Nắng	          Nóng	          Không	        Có
2	           Mưa	          Mát	            Có	          Không
3	           Âm u	          Ấm	            Không	        Có
4	           Nắng	          Ấm	            Có	          ? (Cần dự đoán)
________________________________________
Bước 2: "Xây dựng cây" (Hỏi từng người bạn)
Người bạn 1 (Chỉ xem Thời tiết + Nhiệt độ):
1.	Hỏi: "Hôm nay thời tiết Nắng và nhiệt độ Ấm, trước đây đi picnic chưa?"
2.	Nhớ lại:
-	Ngày 1: Nắng + Nóng → Đi picnic (Có).
-	Ngày 3: Âm u + Ấm → Đi picnic (Có).
→ Kết luận: "Có" (Vì đa số ngày tương tự đều đi).
Người bạn 2 (Chỉ xem Nhiệt độ + Gió):
1.	Hỏi: "Nhiệt độ Ấm + có gió, có nên đi không?"
2.	Nhớ lại:
-	Ngày 3: Ấm + Không gió → Đi picnic (Có).
-	Ngày 2: Mát + Có gió → Không đi (Không).
→ Phân vân, chọn theo nhiệt độ Ấm: "Có".
Người bạn 3 (Chỉ xem Thời tiết + Gió):
1.	Hỏi: "Thời tiết Nắng + có gió, đi picnic không?"
2.	Nhớ lại:
-	Ngày 1: Nắng + Không gió → Đi picnic (Có).
-	Không có ngày nào Nắng + Có gió.
→ Dựa vào Thời tiết Nắng: "Có".
________________________________________
Bước 3: Tổng hợp kết quả (Majority Vote)
-	Người 1: Có
-	Người 2: Có
-	Người 3: Có
→ Quyết định cuối cùng: ĐI PICNIC!
________________________________________
Giải thích thuật toán qua ví dụ
1.	Tính ngẫu nhiên: Mỗi "người bạn" (cây) chỉ xem xét một tập con yếu tố (features).
2.	Bootstrap: Mỗi người nhớ lại dữ liệu cũ (lấy mẫu ngẫu nhiên từ dữ liệu gốc).
3.	Tổng hợp: Bỏ phiếu đa số từ các cây.
________________________________________
Minh họa bằng Code
from sklearn.ensemble import RandomForestClassifier
import numpy as np

#Dữ liệu: Thời tiết (0: Nắng, 1: Mưa, 2: Âm u), Nhiệt độ (0: Nóng, 1: Ấm, 2: Mát), Gió (0: Không, 1: Có)
X = np.array([[0, 0, 0], [1, 2, 1], [2, 1, 0]])
y = np.array(["Có", "Không", "Có"])

#Huấn luyện Random Forest với 3 cây
model = RandomForestClassifier(n_estimators=3, max_features=2, random_state=42)
model.fit(X, y)

#Dự đoán ngày mới: Nắng (0), Ấm (1), Có gió (1)
new_day = np.array([[0, 1, 1]])
print("Có đi picnic không?", model.predict(new_day)[0])  # Output: 'Có'
Tại sao kết quả là "Có"?
-	Giống như ví dụ chạy tay, 3 cây đều nghiêng về "Có" do đa số phiếu!
________________________________________
Câu hỏi thêm
•	 Nếu thêm người bạn thứ 4 (cây thứ 4) cho kết quả "Không", kết quả cuối cùng là gì?
→ Sẽ hòa (3 Có vs 1 Không), nhưng Random Forest ưu tiên lớp có số phiếu cao hơn → Vẫn "Có".
•	 Tại sao không dùng tất cả yếu tố cho mỗi cây?
→ Nếu mọi người đều xem hết 3 yếu tố, họ sẽ đưa ra kết quả giống nhau → Mất tính đa dạng, dễ overfitting.
________________________________________
Tóm tắt
-	Random Forest giống như hỏi ý kiến nhiều người, mỗi người chỉ quan tâm một phần thông tin.
-	Kết quả cuối cùng là đa số phiếu từ các ý kiến riêng lẻ.


