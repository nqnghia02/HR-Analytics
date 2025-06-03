# Grandient Boosting
## 1. Giới thiệu
Gradient Boosting là một phương pháp học ensemble được dùng cho các bài toán phân loại và hồi quy. Đây là một thuật toán học tăng cường bằng cách tổ hợp nhiều mô hình để tạo ra mô hình dự đoán mạnh nhất. Thuật toán hoạt động dựa trên việc training tuần tự models, trong đó mỗi model sẽ cố gắng sửa các lỗi do ‘người tiền nhiệm’ trước đó thực hiện
Trong gradient boosting, mỗi mô hình mới được đào tạo để tối tiểu hoá hàm loss, chẳng hạng như MSE hay cross-entropy của model trước đó sử dụng gradient descent. Trong mỗi bước lặp cảu thuật toán sẽ tính toán gradient của hàm loss theo dự đoá và huấn luyện một mô hình yếu mới để giảm thiểu gradient này. Dụ đoán cảu mô hình mới sẽ được thêm vào ensemble (tất cả mô hình dự đoán)và quá trình được lặp đi lặp lại cho đến khi thoả mãn tiêu chí dừng
## 2. Shrinkage và Độ phức tạp model
Trong gradient boosting, thuật ngữ ‘Shrinkage’ liên quan đến việc sử dụng learning rate (\eta ). Chỉ số learning rate sẽ điều chỉnh mức độ ảnh hưởng của mỗi Decision Tree mới được thêm vào model trong quá trình training.
-	Với leaning rate thấp: có nghĩa là sự đóng góp của mỗi cây là nhỏ, điều này sẽ làm giảm rủi ro overfitting nhưng yêu cầu nhiều cây để đạt được hiệu suất tốt, dẫn đến thời gian trainning lâu hơn
-	Với learning rate cao: có nghĩa là mỗi Decision Tree có sự tác động lớn nhưng điều đó lại dẫn đến hiện tượng overfitting
Vì vậy việc lựa chọn learning rate phải có sự phù hợp để models cho ra hiệu suất tốt nhất.
## 3. Cách thức hoạt động
### 3.1Quá trình học tập tuần tự
Ensemble bao gồm nhiều cây được huấn luyện để sửa lỗi của cây trước đó. Trong lần lặp đầu tiên, Tree 1 sẽ được trained trên dữ liệu gốc x và true labels y. Nó sẽ đưa ra dự đoán, và dự đoán này sẽ được dùng để tính toán lỗi.
### 3.2 Tính toán phần dư (phần chênh lệch giữa label y gốc và label y’ dự đoán dựa trên model đã trained)
Trong bước lặp thứ 2, Tree 2 sẽ được huấn luyện dựa trên data gốc  x, thay vì nhãn gốc y thì lúc này phần dư r = y - y’, và tương tự như bước huấn luyện ở Tree1. Quá trình này sẽ tiếp tục cho tất cả các cây trong Ensemble. Mỗi cây được huấn luyện tiếp theo dùng để dự đoán lỗi của cây trước đó.
 ![alt text](image.png)
(Nguồn: https://www.geeksforgeeks.org/ml-gradient-boosting/)
### 3.3 Shrinkage 
Sau mỗi lần cây được huấn luyện, thì dự đoán mới của nó sẽ thu hẹp lại bằng cách nhân chúng với giá trị learning rate (giá trị này dao động từ 0 đến 1). Điều này giúp tránh hiện tượng overfitting bằng cách đảm bảo cho mỗi cây có sự tác động nhỏ hơn đến mô hình cuối cùng.
Sau khi tất cả các cây được trained, thì dự đoán ban đầu được thực hiện bằng các tổng hợp các đóng góp của tất cả các cây. Dự đoán cuối cùng được tính toán bởi công thức sau: 
![alt text](image-1.png)
với r1, r2 ... rN là các lỗi dự đoán của mỗi cây.