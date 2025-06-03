
# ĐÁNH GIÁ KẾT QUẢ SAU KHI KIỂM TRA Ở CÁC BƯỚC:
## KIỂM TRA SỐ LƯỢNG GIÁ TRỊ NULL Ở MỖI TRƯỜNG
-	Sau khi kiểm tra thì ta nhận thấy không có trường dữ liệu nào bị bỏ trống
## KIỂM TRA GIÁ TRỊ TRÙNG LẶP
-	Không có giá trị nào trùng lặp.
## KIỂM TRA OUTLIERS
Lựa chọn các trường dữ liệu định lượng để thực hiện kiểm tra outlier 

Index(['Age', 'DailyRate', 'DistanceFromHome', 'Education', 'EmployeeCount',
       'EmployeeNumber', 'EnvironmentSatisfaction', 'HourlyRate',
       'JobInvolvement', 'JobLevel', 'JobSatisfaction', 'MonthlyIncome',
       'MonthlyRate', 'NumCompaniesWorked', 'PercentSalaryHike',
       'PerformanceRating', 'RelationshipSatisfaction', 'StandardHours',
       'StockOptionLevel', 'TotalWorkingYears', 'TrainingTimesLastYear',
       'WorkLifeBalance', 'YearsAtCompany', 'YearsInCurrentRole',
       'YearsSinceLastPromotion', 'YearsWithCurrManager'],
      dtype='object')
Các trường dữ liệu trên đây là các trường mà ta sẽ thực hiện việc xử lí outliers

-	Đánh giá: Sau khi xử lý bộ dữ liệu và giả định loại bỏ các giá trị outlier, ta thấy dữ liệu outlier chiếm hơn 50% bộ dữ liệu, ta thực hiện visualize để quan sát xem dữ liệu ở trường nào có outlier bằng cách sử dụng biểu đồ boxplot
-	Thực hiện hiện visualize để quan sát xem dữ liệu ở trường nào có outlier bằng cách sử dụng biểu đồ boxplot ta có nhận xét về từng biểu đồ cụ thể như sau 
•	Age:
	Phân bố khá đều, không có outlier rõ rệt.
	Dao động từ khoảng 18 đến 60 tuổi.
	Phân bố hơi nghiêng về nhóm tuổi 30 đến 40.
•	DailyRate:
	Có nhiều outliers ở cả hai phía (cao và thấp).
	Phân bố rộng, lương theo ngày dao động mạnh.
•	DistanceFromHome:
	Có một vài outliers phía trên (> 25km).
	Phần lớn nhân viên sống cách nơi làm < 20km.
•	Education:
	Giá trị từ 1 đến 5, không có outliers.
•	EmployeeCount:
	Chỉ có một giá trị (1) cho toàn bộ.
•	EmployeeNumber:
	Là ID nhân viên, không mang ý nghĩa số học
•	EnvirontmentSatisfaction:
	Giá trị 1 đến 4, không có outliers.
•	HourlyRate:
	Có vài outliers nhẹ phía trên và dưới.
	Lương theo giờ phân bố không đều, nhưng không có bất thường nghiêm trọng.
•	JobInvolvement:
	Giá trị 1 đến 4, không có outliers.
	Là thang đo mức độ tham gia
•	JobLevel:
	Phân bố hợp lý trong khoảng 1 đến 5.
	Không có outliers.
•	JobSatisfaction:
	Giá trị từ 1 đến 4, không có outlier.
	Thang đo mức độ hài lòng trong công việc
•	MonthlyIncome:
	Có rất nhiều outliers ở phía cao.
	Một số nhân viên có thu nhập > 20.000 trong khi phần lớn < 10.000.
•	MonthlyRate:
	Nhiều outliers ở phía cao.
	Có thể do một số nhân viên nhận lương cao hoặc phụ cấp lớn.
•	NumCompaniesWorked:
	Có outliers (giá trị lớn như 9).
	Đa phần nhân viên từng làm < 5 công ty.
•	PercentSalaryHike:
	Một vài điểm outlier (> 20%).
	Mức tăng lương thường từ 10 đến 15%.
•	PerformanceRating:
	Hầu như chỉ có 2 giá trị (3, 4), không có outlier.
•	RelationshipSatisfaction:
	Giá trị từ 1 đến 4, không có outlier.
•	StandardHours: Giá trị luôn là 80.
•	StockOptionLevel:
	Giá trị từ 0 đến 3, không có outlier.
•	TotalWorkingYears:
	Có vài outliers > 35 đến 40 năm.
	Phần lớn nhân viên có kinh nghiệm < 20 năm.
•	TrainingTimesLastYear:
	Giá trị 0 đến 6, có phân bố đều.
•	WorkLifeBalance:
	Giá trị 1 đến 4, không có outliers.
•	YearsAtCompany:
	Có outliers > 30 năm.
	Đa số làm dưới 10 năm
•	YearsInCurrentRole:
	Phân bố hợp lý, có vài outliers ở giá trị cao.
•	YearsSinceLastPromotion:
	Có outliers rõ (15 năm không được thăng chức).
•	YearsWithCurrManager:
	Có vài giá trị lớn hơn phần còn lại (> 15 năm).
•	Đánh giá chung: Việc có sự xuất hiện dữ liệu outliers trong bộ dữ liệu thuộc lĩnh vực này nguyên nhân là do đặc thù của các công ty, giả sử ở trường MonthlyIncome, có rất nhiều giá trị outliers vì những người này nắm giữ những vị trí quan trọng trong công ty, và mức lương của họ sẽ có sự chênh lệch đối với nhân viên trong công ty, nên mặt bằng chung các giá trị này thường trội hơn giá trị trung bình.
•	Đề xuất: Ta sẽ không loại bỏ các giá trị outliers, và ta sẽ thực hiện đánh giá ở bước Data Analysis để đưa ra kết luận
## THỐNG KÊ DỮ LIỆU 
Sau khi thực hiện việc thống kê dữ liệu ta có vài nhận xét cơ bản về bộ dữ liệu như sau
1.	Độ tuổi (Age): 
o	Trung bình: 36.92 tuổi, cho thấy lực lượng lao động có độ tuổi trung bình khá trẻ.
o	Phân bố: Độ tuổi dao động từ 18 đến 60, với 50% nhân viên nằm trong khoảng 30-43 tuổi (từ Q1 đến Q3).
o	Nhận xét: Tổ chức có sự đa dạng về độ tuổi, nhưng tập trung nhiều vào nhóm lao động trẻ và trung niên.
2.	Lương hàng ngày (DailyRate): 
o	Trung bình: 802.49 (đơn vị tiền tệ không xác định), nhưng mức lương dao động lớn, từ 102 đến 1499.
o	Phân bố: 50% nhân viên có mức lương hàng ngày từ 465 đến 1157.
o	Nhận xét: Có sự chênh lệch đáng kể về mức lương hàng ngày giữa các nhân viên, có thể phản ánh sự khác biệt về vai trò, kinh nghiệm hoặc cấp bậc.
3.	Khoảng cách từ nhà đến nơi làm việc (DistanceFromHome): 
o	Trung bình: 9.19 (đơn vị có thể là km hoặc dặm), với khoảng cách dao động từ 1 đến 29.
o	Phân bố: 50% nhân viên sống cách nơi làm việc từ 2 đến 14 đơn vị.
o	Nhận xét: Phần lớn nhân viên sống tương đối gần công ty, nhưng một số người sống khá xa, có thể ảnh hưởng đến thời gian di chuyển và sự cân bằng công việc-cuộc sống.
4.	Trình độ học vấn (Education): 
o	Trung bình: 2.91, với thang đo từ 1 đến 5 (có thể tương ứng với các mức như trung học, cao đẳng, đại học, v.v.).
o	Phân bố: 50% nhân viên có trình độ từ 2 đến 4, cho thấy đa số có trình độ cao đẳng hoặc đại học.
5.	Số năm làm việc tổng cộng (TotalWorkingYears): 
o	Trung bình: 11.28 năm, với sự phân bố rộng từ 0 đến 40 năm.
o	Phân bố: 50% nhân viên có kinh nghiệm từ 6 đến 15 năm.
6.	Mức độ hài lòng (EnvironmentSatisfaction, JobSatisfaction, RelationshipSatisfaction): 
o	Trung bình: Các chỉ số này dao động quanh 2.7-2.8 (thang 1-4), cho thấy mức độ hài lòng trung bình đến khá.
o	Phân bố: 50% nhân viên có mức hài lòng từ 2 đến 4, với một số ít không hài lòng (min = 1).
7.	Thu nhập hàng tháng (MonthlyIncome): 
o	Trung bình: 6502.93, nhưng dao động rất lớn, từ 1009 đến 19999.
o	Phân bố: 50% nhân viên có thu nhập từ 2911 đến 8379.
8.	Số năm làm việc tại công ty (YearsAtCompany): 
o	Trung bình: 7 năm, với 50% nhân viên làm việc từ 3 đến 9 năm.
o	Phân bố: Một số nhân viên đã ở lại rất lâu (tối đa 40 năm), nhưng cũng có người mới (tối thiểu 0 năm).
9.	Hiệu suất và tăng lương (PerformanceRating, PercentSalaryHike): 
o	Hiệu suất: Trung bình 3.15 (thang 3-4), cho thấy đa số nhân viên được đánh giá ở mức khá hoặc xuất sắc.
o	Tăng lương: Trung bình 15.21%, dao động từ 11% đến 25%.
10.	Cân bằng công việc - cuộc sống (WorkLifeBalance): 
o	Trung bình: 2.76 (thang 1-4), với 50% nhân viên đánh giá từ 2 đến 3.
## THỰC HIỆN MÃ HÓA CÁC TRƯỜNG DỮ LIỆU ĐỊNH TÍNH 

## PHÂN CHIA TẬP TRAIN-TEST
