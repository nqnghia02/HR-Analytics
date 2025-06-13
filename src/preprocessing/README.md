## (+) BÁO CÁO MÔ TẢ TẬP DỮ LIỆU TRƯỚC KHI XỬ LÝ
I. Tổng quan về tập dữ liệu
1.	Số lượng dòng: Dựa trên số lượng giá trị của cột EmployeeNumber (1470 giá trị), có thể suy ra rằng tập dữ liệu có khả năng chứa khoảng 1470 dòng (giả định mỗi nhân viên có một số định danh duy nhất).
2.	Số lượng cột: Có 35 cột được liệt kê trong tập dữ liệu.
3.	Loại dữ liệu: 
-	Int64: Age, DailyRate, DistanceFromHome, Education, EmployeeCount, EmployeeNumber, EnvironmentSatisfaction, HourlyRate, JobInvolvement, JobLevel, JobSatisfaction, MonthlyIncome, MonthlyRate, NumCompaniesWorked, PercentSalaryHike, PerformanceRating, RelationshipSatisfaction, StandardHours, StockOptionLevel, TotalWorkingYears, TrainingTimesLastYear, WorkLifeBalance, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager.
-	Object:  Attrition, BusinessTravel, DistanceFromHome, EducationField, Gender, JobRole, MaritalStatus, Over18, OverTime.

II. Mô tả các cột và phân tích ngoại lệ
Dưới đây là mô tả chi tiết từng cột, phạm vi giá trị, và các tính năng ngoại lệ tiềm năng:
1.	Age (Tuổi): 
-	Phạm vi giá trị: Từ 18 đến 60.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Phạm vi tuổi hợp lý cho lực lượng lao động. Không có giá trị ngoại lệ rõ ràng (ví dụ: không có giá trị âm hoặc quá lớn như 100). Phân bố tuổi có thể cần được kiểm tra thêm để phát hiện xem có bất kỳ nhóm tuổi nào chiếm ưu thế hay không.
2.	BusinessTravel (Tần suất công tác): 
-	Giá trị: Non-Travel, Travel_Frequently, Travel_Rarely (3 giá trị).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Đây là cột danh mục với ba mức độ, phù hợp để phân tích tần suất công tác.
3.	DailyRate (Lương ngày): 
-	Phạm vi giá trị: Từ 102 đến 1496.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Phạm vi giá trị rộng, có thể cần kiểm tra phân bố để xác định xem có giá trị nào bất thường (quá thấp hoặc quá cao so với mức lương ngày trung bình). 
4.	Department (Phòng ban): 
-	Giá trị: Human Resources, Research & Development, Sales (3 giá trị).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Cột này phân loại rõ ràng các phòng ban trong tổ chức.
5.	DistanceFromHome (Khoảng cách từ nhà đến nơi làm việc): 
-	Phạm vi giá trị: Từ 1 đến 29.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Khoảng cách hợp lý, có thể là số dặm hoặc kilômét. Không có giá trị ngoại lệ rõ ràng, nhưng cần kiểm tra phân bố để xem liệu có nhiều nhân viên sống quá xa (ví dụ: 29) so với phần lớn.
6.	Education (Trình độ học vấn): 
-	Phạm vi giá trị: Từ 1 đến 5 (5 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64), có thể đại diện cho các mức học vấn.
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể được xử lý như một biến danh mục có thứ tự.
7.	EducationField (Lĩnh vực học vấn): 
-	Giá trị: Human Resources, Life Sciences, Marketing, Medical, Other, Technical Degree (6 giá trị).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Cột này phù hợp để phân tích sự phân bố nhân viên theo lĩnh vực học vấn.
8.	EmployeeCount (Số lượng nhân viên): 
-	Giá trị: Chỉ có 1.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Cột này không mang thông tin phân tích vì chỉ có một giá trị duy nhất. Có thể xem xét loại bỏ cột này trong quá trình xử lý dữ liệu.
9.	EmployeeNumber (Số định danh nhân viên): 
-	Phạm vi giá trị: Từ 1 đến 2068.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Đây là định danh cho mỗi nhân viên, không có giá trị ngoại lệ. Tuy nhiên, cần kiểm tra xem có giá trị trùng lặp hoặc thiếu sót nào không.
10.	EnvironmentSatisfaction (Mức độ hài lòng với môi trường làm việc): 
-	Phạm vi giá trị: Từ 1 đến 4 (4 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể được xử lý như một biến danh mục có thứ tự.
11.	Gender (Giới tính): 
-	Giá trị: Female, Male (2 giá trị).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Cột này phù hợp để phân tích sự khác biệt giới tính.
12.	HourlyRate (Lương giờ): 
-	Phạm vi giá trị: Từ 30 đến 100.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Phạm vi hợp lý cho lương giờ. Cần kiểm tra phân bố để xác định xem có giá trị nào bất thường (quá thấp hoặc quá cao) so với mức trung bình.
13.	JobInvolvement (Mức độ tham gia công việc): 
-	Phạm vi giá trị: Từ 1 đến 4 (4 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể được xử lý như một biến danh mục có thứ tự.
14.	JobLevel (Cấp bậc công việc): 
-	Phạm vi giá trị: Từ 1 đến 5 (5 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể đại diện cho các cấp bậc trong tổ chức, phù hợp để phân tích sự phân bố nhân viên theo cấp bậc.
15.	JobRole (Vai trò công việc): 
-	Giá trị: 9 vai trò (Healthcare Representative, Human Resources, Laboratory Technician, Manager, Manufacturing Director, Research Director, Research Scientist, Sales Executive, Sales Representative).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Cột này cung cấp thông tin chi tiết về vai trò công việc trong tổ chức.
16.	JobSatisfaction (Mức độ hài lòng với công việc): 
-	Phạm vi giá trị: Từ 1 đến 4 (4 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể được xử lý như một biến danh mục có thứ tự.
17.	MaritalStatus (Tình trạng hôn nhân): 
-	Giá trị: Divorced, Married, Single (3 giá trị).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Cột này phù hợp để phân tích nhân khẩu học.
18.	MonthlyIncome (Thu nhập tháng): 
-	Phạm vi giá trị: Từ 1009 đến 19999.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Phạm vi giá trị rộng, với thu nhập thấp nhất là 1009 và cao nhất là 19999. Các giá trị cực đại (gần 19999) hoặc cực tiểu (gần 1009) có thể là ngoại lệ, cần kiểm tra phân bố để xác định xem có bất thường không (ví dụ: thu nhập quá thấp so với vai trò công việc hoặc cấp bậc).
19.	MonthlyRate (Tỷ lệ lương tháng): 
-	Phạm vi giá trị: Từ 2094 đến 26999.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Phạm vi giá trị rất rộng. Các giá trị cực đại (gần 26999) hoặc cực tiểu (gần 2094) có thể là ngoại lệ, cần kiểm tra để đảm bảo tính hợp lý so với MonthlyIncome.
20.	NumCompaniesWorked (Số công ty đã làm việc): 
-	Phạm vi giá trị: Từ 0 đến 9 (10 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ rõ ràng. Giá trị 0 (chưa làm việc ở công ty nào trước đó) và 9 (làm việc ở 9 công ty) là hợp lý, nhưng cần kiểm tra phân bố để xem liệu giá trị 9 có chênh lệch nhiều so với giá trị khác không.
21.	Over18 (Trên 18 tuổi): 
-	Giá trị: Chỉ có Y.
-	Kiểu dữ liệu: Object.
-	Nhận xét: Cột này không mang thông tin phân tích vì tất cả giá trị đều là Y. Có thể xem xét loại bỏ trong quá trình xử lý.
22.	OverTime (Làm thêm giờ): 
-	Giá trị: No, Yes (2 giá trị).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Cột này phù hợp để phân tích tác động của làm thêm giờ.
23.	PercentSalaryHike (Tỷ lệ tăng lương): 
-	Phạm vi giá trị: Từ 11% đến 25% (15 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Phạm vi hợp lý cho tỷ lệ tăng lương. Không có giá trị ngoại lệ rõ ràng, nhưng cần kiểm tra phân bố để xác định mức tăng lương phổ biến.
24.	PerformanceRating (Xếp hạng hiệu suất): 
-	Phạm vi giá trị: 3 và 4 (2 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Chỉ có hai mức đánh giá, có thể cần kiểm tra sự phân bố để xem có mất cân bằng không.
25.	RelationshipSatisfaction (Mức độ hài lòng với mối quan hệ): 
-	Phạm vi giá trị: Từ 1 đến 4 (4 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể được xử lý như một biến danh mục có thứ tự.
26.	StandardHours (Số giờ làm việc tiêu chuẩn): 
-	Giá trị: Chỉ có 80.
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Cột này không mang thông tin phân tích vì chỉ có một giá trị. Có thể xem xét loại bỏ.
27.	StockOptionLevel (Mức quyền chọn cổ phiếu): 
-	Phạm vi giá trị: Từ 0 đến 3 (4 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể được xử lý như một biến danh mục có thứ tự.
28.	TotalWorkingYears (Tổng số năm làm việc): 
-	Phạm vi giá trị: Từ 0 đến 40 (40 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Phạm vi hợp lý, nhưng giá trị 0 (chưa có kinh nghiệm làm việc) và 40 (rất nhiều kinh nghiệm) có thể cần kiểm tra để xác định xem có bất thường không.
29.	TrainingTimesLastYear (Số lần đào tạo trong năm trước): 
-	Phạm vi giá trị: Từ 0 đến 6 (7 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ rõ ràng. Giá trị 0 (không đào tạo) và 6 (đào tạo nhiều lần) là hợp lý, nhưng cần kiểm tra phân bố.
30.	WorkLifeBalance (Cân bằng công việc - cuộc sống): 
-	Phạm vi giá trị: Từ 1 đến 4 (4 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Không có giá trị ngoại lệ. Cột này có thể được xử lý như một biến danh mục có thứ tự.
31.	YearsAtCompany (Số năm làm việc tại công ty): 
-	Phạm vi giá trị: Từ 0 đến 40 (36 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Giá trị 40 là khá cao và có thể là ngoại lệ nếu số lượng nhân viên có thời gian làm việc dài như vậy là hiếm. Cần kiểm tra phân bố.
32.	YearsInCurrentRole (Số năm ở vai trò hiện tại): 
-	Phạm vi giá trị: Từ 0 đến 18 (19 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Giá trị 18 có thể là ngoại lệ nếu ít nhân viên giữ vai trò hiện tại lâu như vậy. Cần kiểm tra phân bố.
33.	YearsSinceLastPromotion (Số năm kể từ lần thăng chức cuối): 
-	Phạm vi giá trị: Từ 0 đến 15 (16 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Giá trị 15 có thể là ngoại lệ nếu ít nhân viên có khoảng thời gian dài như vậy mà không được thăng chức. Cần kiểm tra phân bố.
34.	YearsWithCurrManager (Số năm làm việc với quản lý hiện tại): 
-	Phạm vi giá trị: Từ 0 đến 17 (18 giá trị).
-	Kiểu dữ liệu: Số nguyên (np.int64).
-	Nhận xét: Giá trị 17 có thể là ngoại lệ nếu ít nhân viên làm việc lâu với cùng một quản lý. Cần kiểm tra phân bố.
35.	Attrition (Tỷ lệ nghỉ việc): 
-	Giá trị: No, Yes (2 giá trị).
-	Kiểu dữ liệu: Object.
-	Nhận xét: Không có giá trị ngoại lệ. Đây là cột mục tiêu quan trọng để phân tích tỷ lệ nghỉ việc của nhân viên.

PHÂN CHIA CÁC TRƯỜNG DỮ LIỆU THÀNH CÁC NHÓM 
1.	Thông tin nhân viên
-	Age: 18 - 60
-	Gender: 'Male' , 'Female'
-	MaritalStatus: 'Single' , 'Married' , 'Divorced'
-	Education: 1 , 2 , 3 , 4 , 5
-	DistanceFromHome: 1 - 29
-	TotalWorkingYears: 0 - 40
-	NumCompaniesWorked 0 - 9
2.	Thông tin công việc của nhân viên:
-	EducationField: 'Human Resources', 'Life Sciences', 'Marketing', 'Medical', 'Other', 'Technical Degree'
-	Department: 'Human Resources', 'Research & Development', 'Sales'
-	JobLevel: 1, 2, 3, 4, 5
-	JobRole: 'Healthcare Representative', 'Human Resources', 'Laboratory Technician', 'Manager', 'Manufacturing Director', 'Research Director', 'Research Scientist', 'Sales Executive', 'Sales Representative'
-	JobInvolvement: 1, 2, 3, 4
-	OverTime: Yes, No
-	JobSatisfaction: 1, 2, 3, 4
3.	Thông tin công ty về nhân viên:
-	YearsAtCompany: 0 - 40
-	YearsInCurrentRole: 0 - 18
-	YearsWithCurrManager: 0 - 17
-	YearsSinceLastPromotion: 0 -15
-	TrainingTimesLastYear: 0 – 6
-	WorkLifeBalance: 1, 2, 3, 
4.	Thông tin về công ty:
-	PercentSalaryHike: 11 - 25
-	StockOptionLevel: 0, 1, 2, 3
-	BusinessTravel: 'Non-Travel', 'Travel_Frequently', 'Travel_Rarely'
-	PerformanceRating: 3, 4
-	EnvironmentSatisfaction: 1, 2, 3, 4
-	RelationshipSatisfaction: 1, 2, 3, 4
5.	Thông tin về lương thưởng:
-	MonthlyIncome: 1k - 20k
-	HourlyRate: 30 - 100
-	DailyRate: 100 - 1500
-	MonthlyRate: 2000 – 27000

III. Các tính năng ngoại lệ tiềm năng
Dựa trên phân tích trên, các cột có khả năng chứa giá trị ngoại lệ hoặc cần kiểm tra thêm bao gồm:
1.	DailyRate: 
-	Giá trị thấp (102) và cao (1496) có thể là ngoại lệ nếu không phù hợp với phân bố chung của lương ngày. Cần sử dụng biểu đồ hộp (boxplot) hoặc phân tích thống kê để xác định.
2.	MonthlyIncome: 
-	Giá trị thấp (1009) và cao (19999) có thể là ngoại lệ, đặc biệt nếu không tương ứng với vai trò công việc (JobRole) hoặc cấp bậc (JobLevel). Cần kiểm tra mối quan hệ với các cột khác.
3.	MonthlyRate: 
-	Giá trị thấp (2094) và cao (26999) có thể là ngoại lệ. Cần kiểm tra tính nhất quán với MonthlyIncome và DailyRate.
4.	YearsAtCompany: 
-	Giá trị 40 là khá cao và có thể là ngoại lệ nếu số lượng nhân viên có thâm niên như vậy là ít. Cần kiểm tra phân bố.
5.	YearsInCurrentRole: 
-	Giá trị 18 có thể là ngoại lệ nếu ít nhân viên giữ vai trò hiện tại lâu như vậy.
6.	YearsSinceLastPromotion: 
-	Giá trị 15 có thể là ngoại lệ nếu ít nhân viên có khoảng thời gian dài mà không được thăng chức.
7.	YearsWithCurrManager: 
-	Giá trị 17 có thể là ngoại lệ nếu ít nhân viên làm việc lâu với cùng một quản lý.
8.	EmployeeCount, Over18, StandardHours: 
-	Những cột này chỉ có một giá trị duy nhất (1, Y, 80), không mang thông tin phân tích và có thể được loại bỏ để giảm chiều dữ liệu.
IV. Đề xuất xử lý dữ liệu
1.	Kiểm tra giá trị ngoại lệ: 
-	Sử dụng biểu đồ hộp (boxplot) hoặc phương pháp thống kê (như IQR) để xác định và xử lý các giá trị ngoại lệ trong các cột DailyRate, MonthlyIncome, MonthlyRate, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, và YearsWithCurrManager.
-	Kiểm tra tính nhất quán giữa các cột liên quan (ví dụ: MonthlyIncome với JobRole và JobLevel).
2.	Loại bỏ cột không mang thông tin: 
-	Xem xét loại bỏ các cột EmployeeCount, Over18, và StandardHours vì chỉ có một giá trị.
3.	Xử lý dữ liệu danh mục: 
-	Mã hóa các cột danh mục (BusinessTravel, Department, EducationField, JobRole, MaritalStatus, Gender, OverTime, Attrition) thành dạng số (one-hot encoding hoặc label encoding) để sử dụng trong các mô hình học máy.
4.	Phân tích phân bố: 
-	Vẽ biểu đồ phân bố (histogram, boxplot) cho các cột số để hiểu rõ hơn về sự phân tán và xác định các giá trị bất thường.
-	Phân tích sự phân bố của các cột danh mục để kiểm tra xem có sự mất cân bằng nào không (ví dụ: tỷ lệ Attrition giữa Yes và No).
5.	Kiểm tra giá trị thiếu: 
-	Dữ liệu được cung cấp không đề cập đến giá trị thiếu, nhưng cần kiểm tra toàn bộ tập dữ liệu để đảm bảo không có giá trị NaN hoặc null.
________________________________________
V. Kết luận
Tập dữ liệu có khoảng 1470 dòng và 35 cột, bao gồm các biến số, danh mục và nhị phân, cung cấp thông tin toàn diện về nhân viên trong tổ chức. Các cột như DailyRate, MonthlyIncome, MonthlyRate, và các cột liên quan đến thời gian làm việc (YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager) có khả năng chứa giá trị ngoại lệ cần được kiểm tra thêm. Các cột EmployeeCount, Over18, và StandardHours không mang thông tin phân tích và có thể được loại bỏ. Tập dữ liệu này phù hợp để phân tích các yếu tố ảnh hưởng đến tỷ lệ nghỉ việc (Attrition), nhưng cần được xử lý cẩn thận để đảm bảo chất lượng dữ liệu trước khi áp dụng các mô hình học máy.
 (+) ĐÁNH GIÁ KẾT QUẢ SAU KHI KIỂM TRA Ở CÁC BƯỚC:
## PHÂN CHIA TẬP TRAIN-TEST
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
1.	Age:
-	Phân bố khá đều, không có outlier rõ rệt.
-	Dao động từ khoảng 18 đến 60 tuổi.
-	Phân bố hơi nghiêng về nhóm tuổi 30 đến 40.
2.	DailyRate:
-	Có nhiều outliers ở cả hai phía (cao và thấp).
-	Phân bố rộng, lương theo ngày dao động mạnh.
3.	DistanceFromHome:
-	Có một vài outliers phía trên (> 25km).
-	Phần lớn nhân viên sống cách nơi làm < 20km.
4.	Education:
-	Giá trị từ 1 đến 5, không có outliers.
5.	EmployeeCount:
-	Chỉ có một giá trị (1) cho toàn bộ.
6.	EmployeeNumber:
-	Là ID nhân viên, không mang ý nghĩa số học
7.	EnvirontmentSatisfaction:
-	Giá trị 1 đến 4, không có outliers.
8.	HourlyRate:
-	Có vài outliers nhẹ phía trên và dưới.
-	Lương theo giờ phân bố không đều, nhưng không có bất thường nghiêm trọng.
9.	JobInvolvement:
-	Giá trị 1 đến 4, không có outliers.
-	Là thang đo mức độ tham gia
10.	JobLevel:
-	Phân bố hợp lý trong khoảng 1 đến 5.
-	Không có outliers.
11.	JobSatisfaction:
-	Giá trị từ 1 đến 4, không có outlier.
-	Thang đo mức độ hài lòng trong công việc
12.	MonthlyIncome:
-	Có rất nhiều outliers ở phía cao.
-	Một số nhân viên có thu nhập > 20.000 trong khi phần lớn < 10.000.
13.	MonthlyRate:
-	Nhiều outliers ở phía cao.
-	Có thể do một số nhân viên nhận lương cao hoặc phụ cấp lớn.
14.	NumCompaniesWorked:
-	Có outliers (giá trị lớn như 9).
-	Đa phần nhân viên từng làm < 5 công ty.
15.	PercentSalaryHike:
-	Một vài điểm outlier (> 20%).
-	Mức tăng lương thường từ 10 đến 15%.
16.	PerformanceRating:
-	Hầu như chỉ có 2 giá trị (3, 4), không có outlier.
17.	RelationshipSatisfaction:
-	Giá trị từ 1 đến 4, không có outlier.
18.	StandardHours: 
-	Giá trị luôn là 80.
19.	StockOptionLevel:
-	Giá trị từ 0 đến 3, không có outlier.
20.	TotalWorkingYears:
-	Có vài outliers > 35 đến 40 năm.
-	Phần lớn nhân viên có kinh nghiệm < 20 năm.
21.	TrainingTimesLastYear:
-	Giá trị 0 đến 6, có phân bố đều.
22.	WorkLifeBalance:
-	Giá trị 1 đến 4, không có outliers.
23.	YearsAtCompany:
-	Có outliers > 30 năm.
-	Đa số làm dưới 10 năm
24.	YearsInCurrentRole:
-	Phân bố hợp lý, có vài outliers ở giá trị cao.
25.	YearsSinceLastPromotion:
-	Có outliers rõ (15 năm không được thăng chức).
26.	YearsWithCurrManager:
-	Có vài giá trị lớn hơn phần còn lại (> 15 năm).
Đánh giá chung: Việc có sự xuất hiện dữ liệu outliers trong bộ dữ liệu thuộc lĩnh vực này nguyên nhân là do đặc thù của các công ty, giả sử ở trường MonthlyIncome, có rất nhiều giá trị outliers vì những người này nắm giữ những vị trí quan trọng trong công ty, và mức lương của họ sẽ có sự chênh lệch đối với nhân viên trong công ty, nên mặt bằng chung các giá trị này thường trội hơn giá trị trung bình.
Đề xuất: Ta sẽ không loại bỏ các giá trị outliers, và ta sẽ thực hiện đánh giá ở bước Data Analysis để đưa ra kết luận
## THỐNG KÊ DỮ LIỆU 
Sau khi thực hiện việc thống kê dữ liệu ta rút ra vài điều cơ bản về bộ dữ liệu như sau 
1.	Age (Tuổi): 
-	Phân bố: Tuổi trung bình là 36.77 (gần 37), với độ lệch chuẩn 9.20, cho thấy sự phân tán hợp lý. Tuổi dao động từ 18 đến 60, phù hợp với lực lượng lao động.
2.	DailyRate (Lương ngày): 
-	Phân bố: Trung bình 799.41, độ lệch chuẩn 405.73, dao động từ 102 đến 1496. Giá trị trung vị (796.5) gần với trung bình, cho thấy phân bố có thể khá đối xứng.
3.	DistanceFromHome (Khoảng cách từ nhà đến nơi làm việc): 
-	Phân bố: Trung bình 9.26 (dặm hoặc km), độ lệch chuẩn 8.15, dao động từ 1 đến 29. Trung vị là 7, thấp hơn trung bình, cho thấy phân bố có thể lệch phải (skewed right).
4.	Education (Trình độ học vấn): 
-	Phân bố: Trung bình 2.90 (gần mức 3), dao động từ 1 đến 5, với trung vị là 3. Độ lệch chuẩn 1.04 cho thấy sự phân tán vừa phải.
5.	EmployeeCount (Số lượng nhân viên): 
-	Phân bố: Chỉ có giá trị 1, với độ lệch chuẩn 0.
6.	EmployeeNumber (Số định danh nhân viên): 
-	Phân bố: Dao động từ 1 đến 2068, với trung bình 1028.28 và trung vị 1018. Độ lệch chuẩn 607.60 cho thấy sự phân bố rộng.
7.	EnvironmentSatisfaction (Mức độ hài lòng với môi trường làm việc): 
-	Phân bố: Trung bình 2.70 (gần mức 3), dao động từ 1 đến 4, với trung vị là 3.
8.	HourlyRate (Lương giờ): 
-	Phân bố: Trung bình 66.67, độ lệch chuẩn 20.46, dao động từ 30 đến 100. Trung vị (67) gần với trung bình, cho thấy phân bố khá đối xứng.
9.	JobInvolvement (Mức độ tham gia công việc): 
-	Phân bố: Trung bình 2.72 (gần mức 3), dao động từ 1 đến 4, với trung vị là 3.
10.	JobLevel (Cấp bậc công việc): 
-	Phân bố: Trung bình 2.03, dao động từ 1 đến 5, với trung vị là 2. Độ lệch chuẩn 1.10 cho thấy sự phân tán vừa phải.
11.	MonthlyIncome (Thu nhập tháng): 
-	Phân bố: Trung bình 6483.64, độ lệch chuẩn 4714.19, dao động từ 1009 đến 19999. Trung vị (4908) thấp hơn trung bình, cho thấy phân bố lệch phải.
12.	MonthlyRate (Tỷ lệ lương tháng): 
-	Phân bố: Trung bình 14311.30, độ lệch chuẩn 7118.93, dao động từ 2094 đến 26999. Trung vị (14235.5) gần với trung bình, cho thấy phân bố khá đối xứng.
13.	NumCompaniesWorked (Số công ty đã làm việc): 
-	Phân bố: Trung bình 2.67, dao động từ 0 đến 9, với trung vị là 2. Độ lệch chuẩn 2.50 cho thấy sự phân tán đáng kể.
14.	PercentSalaryHike (Tỷ lệ tăng lương): 
-	Phân bố: Trung bình 15.18%, dao động từ 11% đến 25%, với trung vị là 14%. Độ lệch chuẩn 3.67 cho thấy sự phân tán vừa phải.
15.	RelationshipSatisfaction (Mức độ hài lòng với mối quan hệ): 
-	Phân bố: Trung bình 2.69 (gần mức 3), dao động từ 1 đến 4, với trung vị là 3.
16.	StandardHours (Số giờ làm việc tiêu chuẩn): 
-	Phân bố: Chỉ có giá trị 80, với độ lệch chuẩn 0.
17.	StockOptionLevel (Mức quyền chọn cổ phiếu): 
-	Phân bố: Trung bình 0.81, dao động từ 0 đến 3, với trung vị là 1. Độ lệch chuẩn 0.86 cho thấy sự phân tán vừa phải.
18.	TotalWorkingYears (Tổng số năm làm việc): 
-	Phân bố: Trung bình 11.12 năm, độ lệch chuẩn 7.81, dao động từ 0 đến 40. Trung vị (10) gần với trung bình, nhưng giá trị tối đa 40 có thể hiếm.
19.	TrainingTimesLastYear (Số lần đào tạo trong năm trước): 
-	Phân bố: Trung bình 2.80, dao động từ 0 đến 6, với trung vị là 3. Độ lệch chuẩn 1.30 cho thấy sự phân tán vừa phải.
20.	WorkLifeBalance (Cân bằng công việc - cuộc sống): 
-	Phân bố: Trung bình 2.75 (gần mức 3), dao động từ 1 đến 4, với trung vị là 3.
21.	YearsAtCompany (Số năm làm việc tại công ty): 
-	Phân bố: Trung bình 6.93 năm, độ lệch chuẩn 6.09, dao động từ 0 đến 40. Trung vị (5) thấp hơn trung bình, cho thấy phân bố lệch phải.
22.	YearsInCurrentRole (Số năm ở vai trò hiện tại): 
-	Phân bố: Trung bình 4.21 năm, độ lệch chuẩn 3.61, dao động từ 0 đến 18. Trung vị (3) thấp hơn trung bình, cho thấy phân bố lệch phải.
23.	YearsSinceLastPromotion (Số năm kể từ lần thăng chức cuối): 
-	Phân bố: Trung bình 2.11 năm, độ lệch chuẩn 3.12, dao động từ 0 đến 15. Trung vị (1) thấp hơn trung bình, cho thấy phân bố lệch phải.
24.	YearsWithCurrManager (Số năm làm việc với quản lý hiện tại): 
-	Phân bố: Trung bình 4.03 năm, độ lệch chuẩn 3.53, dao động từ 0 đến 17. Trung vị (3) thấp hơn trung bình, cho thấy phân bố lệch phải.
## THỰC HIỆN MÃ HÓA CÁC TRƯỜNG DỮ LIỆU ĐỊNH TÍNH 
## SAU KHI MÃ HÓA THỰC HIỆN SCALING
Vì trong bộ dữ liệu này có một số trường có giá trị rất lớn (VD: MonthlyIncome). Điều này làm cho việc sử dụng SVM hoặc Logistic Regression có thể bị mất ổn định. Nên ta cần scaling để mô hình hội tụ nhanh hơn.

