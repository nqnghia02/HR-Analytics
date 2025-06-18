# Báo cáo phân tích và xử lý tập dữ liệu

Báo cáo này mô tả tập dữ liệu nhân sự (1470 dòng, 35 cột) trước và sau xử lý, tập trung vào các yếu tố ảnh hưởng đến tỷ lệ nghỉ việc (Attrition). Báo cáo gồm tổng quan dữ liệu, mô tả cột, phân tích ngoại lệ, thống kê, và kết quả sau xử lý.

## 1. Tổng quan về tập dữ liệu

- **Số lượng dòng**: 1470 (dựa trên cột EmployeeNumber, giả định mỗi nhân viên có ID duy nhất).
- **Số lượng cột**: 35.
- **Loại dữ liệu**:
  - **Số nguyên (int64)**: Age, DailyRate, DistanceFromHome, Education, EmployeeCount, EmployeeNumber, EnvironmentSatisfaction, HourlyRate, JobInvolvement, JobLevel, JobSatisfaction, MonthlyIncome, MonthlyRate, NumCompaniesWorked, PercentSalaryHike, PerformanceRating, RelationshipSatisfaction, StandardHours, StockOptionLevel, TotalWorkingYears, TrainingTimesLastYear, WorkLifeBalance, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager.
  - **Chuỗi (object)**: Attrition, BusinessTravel, Department, EducationField, Gender, JobRole, MaritalStatus, Over18, OverTime.

## 2. Mô tả các cột và phân tích ngoại lệ

### 2.1 Mô tả chi tiết
1. **Age (Tuổi)**:
   - Phạm vi: 18–60.
   - Kiểu dữ liệu: int64.
   - Nhận xét: Phạm vi hợp lý, không có ngoại lệ rõ ràng. Cần phân tích phân bố để xác định nhóm tuổi chiếm ưu thế.
2. **BusinessTravel (Tần suất công tác)**:
   - Giá trị: Non-Travel, Travel_Frequently, Travel_Rarely.
   - Kiểu dữ liệu: object.
   - Nhận xét: Biến danh mục, không có ngoại lệ.
3. **DailyRate (Lương ngày)**:
   - Phạm vi: 102–1496.
   - Kiểu dữ liệu: int64.
   - Nhận xét: Phạm vi rộng, giá trị cực đại/cực tiểu có thể là ngoại lệ. Cần kiểm tra bằng boxplot.
4. **Department (Phòng ban)**:
   - Giá trị: Human Resources, Research & Development, Sales.
   - Kiểu dữ liệu: object.
   - Nhận xét: Biến danh mục, không có ngoại lệ.
5. **DistanceFromHome (Khoảng cách từ nhà)**:
   - Phạm vi: 1–29 (km hoặc dặm).
   - Kiểu dữ liệu: int64.
   - Nhận xét: Hợp lý, nhưng giá trị >25 có thể là ngoại lệ. Cần kiểm tra phân bố.
6. **Education (Trình độ học vấn)**:
   - Phạm vi: 1–5.
   - Kiểu dữ liệu: int64.
   - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
7. **EducationField (Lĩnh vực học vấn)**:
   - Giá trị: Human Resources, Life Sciences, Marketing, Medical, Other, Technical Degree.
   - Kiểu dữ liệu: object.
   - Nhận xét: Biến danh mục, không có ngoại lệ.
8. **EmployeeCount (Số lượng nhân viên)**:
   - Giá trị: 1.
   - Kiểu dữ liệu: int64.
   - Nhận xét: Không mang thông tin, nên loại bỏ.
9. **EmployeeNumber (ID nhân viên)**:
   - Phạm vi: 1–2068.
   - Kiểu dữ liệu: int64.
   - Nhận xét: Định danh duy nhất, cần kiểm tra trùng lặp.
10. **EnvironmentSatisfaction (Hài lòng môi trường)**:
    - Phạm vi: 1–4.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
11. **Gender (Giới tính)**:
    - Giá trị: Female, Male.
    - Kiểu dữ liệu: object.
    - Nhận xét: Biến nhị phân, không có ngoại lệ.
12. **HourlyRate (Lương giờ)**:
    - Phạm vi: 30–100.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Hợp lý, nhưng cần kiểm tra phân bố để xác định giá trị bất thường.
13. **JobInvolvement (Tham gia công việc)**:
    - Phạm vi: 1–4.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
14. **JobLevel (Cấp bậc công việc)**:
    - Phạm vi: 1–5.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
15. **JobRole (Vai trò công việc)**:
    - Giá trị: 9 vai trò (Healthcare Representative, Human Resources, Laboratory Technician, Manager, Manufacturing Director, Research Director, Research Scientist, Sales Executive, Sales Representative).
    - Kiểu dữ liệu: object.
    - Nhận xét: Biến danh mục, không có ngoại lệ.
16. **JobSatisfaction (Hài lòng công việc)**:
    - Phạm vi: 1–4.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
17. **MaritalStatus (Tình trạng hôn nhân)**:
    - Giá trị: Divorced, Married, Single.
    - Kiểu dữ liệu: object.
    - Nhận xét: Biến danh mục, không có ngoại lệ.
18. **MonthlyIncome (Thu nhập tháng)**:
    - Phạm vi: 1009–19999.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị cực đại/cực tiểu có thể là ngoại lệ, cần kiểm tra tính nhất quán với JobRole và JobLevel.
19. **MonthlyRate (Tỷ lệ lương tháng)**:
    - Phạm vi: 2094–26999.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị cực đại/cực tiểu có thể là ngoại lệ, cần kiểm tra với MonthlyIncome.
20. **NumCompaniesWorked (Số công ty đã làm)**:
    - Phạm vi: 0–9.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị 9 có thể hiếm, cần kiểm tra phân bố.
21. **Over18 (Trên 18 tuổi)**:
    - Giá trị: Y.
    - Kiểu dữ liệu: object.
    - Nhận xét: Không mang thông tin, nên loại bỏ.
22. **OverTime (Làm thêm giờ)**:
    - Giá trị: No, Yes.
    - Kiểu dữ liệu: object.
    - Nhận xét: Biến nhị phân, không có ngoại lệ.
23. **PercentSalaryHike (Tỷ lệ tăng lương)**:
    - Phạm vi: 11–25%.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Hợp lý, cần kiểm tra phân bố để xác định mức phổ biến.
24. **PerformanceRating (Hiệu suất)**:
    - Giá trị: 3, 4.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến nhị phân, không có ngoại lệ.
25. **RelationshipSatisfaction (Hài lòng mối quan hệ)**:
    - Phạm vi: 1–4.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
26. **StandardHours (Số giờ làm chuẩn)**:
    - Giá trị: 80.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Không mang thông tin, nên loại bỏ.
27. **StockOptionLevel (Quyền chọn cổ phiếu)**:
    - Phạm vi: 0–3.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
28. **TotalWorkingYears (Tổng năm làm việc)**:
    - Phạm vi: 0–40.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị 40 có thể hiếm, cần kiểm tra phân bố.
29. **TrainingTimesLastYear (Số lần đào tạo)**:
    - Phạm vi: 0–6.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Hợp lý, không có ngoại lệ rõ ràng.
30. **WorkLifeBalance (Cân bằng công việc)**:
    - Phạm vi: 1–4.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Biến danh mục có thứ tự, không có ngoại lệ.
31. **YearsAtCompany (Năm làm tại công ty)**:
    - Phạm vi: 0–40.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị 40 có thể là ngoại lệ, cần kiểm tra phân bố.
32. **YearsInCurrentRole (Năm ở vai trò hiện tại)**:
    - Phạm vi: 0–18.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị 18 có thể hiếm, cần kiểm tra.
33. **YearsSinceLastPromotion (Năm từ lần thăng chức)**:
    - Phạm vi: 0–15.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị 15 có thể hiếm, cần kiểm tra.
34. **YearsWithCurrManager (Năm với quản lý)**:
    - Phạm vi: 0–17.
    - Kiểu dữ liệu: int64.
    - Nhận xét: Giá trị 17 có thể hiếm, cần kiểm tra.
35. **Attrition (Nghỉ việc)**:
    - Giá trị: No, Yes.
    - Kiểu dữ liệu: object.
    - Nhận xét: Biến mục tiêu, cần phân tích tỷ lệ Yes/No để đánh giá mất cân bằng lớp.

### 2.2 Phân chia nhóm dữ liệu
1. **Thông tin nhân viên**:
   - Age, Gender, MaritalStatus, Education, DistanceFromHome, TotalWorkingYears, NumCompaniesWorked.
2. **Thông tin công việc**:
   - EducationField, Department, JobLevel, JobRole, JobInvolvement, OverTime, JobSatisfaction.
3. **Thông tin công ty về nhân viên**:
   - YearsAtCompany, YearsInCurrentRole, YearsWithCurrManager, YearsSinceLastPromotion, TrainingTimesLastYear, WorkLifeBalance.
4. **Thông tin về công ty**:
   - PercentSalaryHike, StockOptionLevel, BusinessTravel, PerformanceRating, EnvironmentSatisfaction, RelationshipSatisfaction.
5. **Thông tin lương thưởng**:
   - MonthlyIncome, HourlyRate, DailyRate, MonthlyRate.

### 2.3 Ngoại lệ tiềm năng
- **DailyRate, MonthlyIncome, MonthlyRate**: Giá trị cực đại/cực tiểu (102, 1009, 2094; 1496, 19999, 26999) có thể là ngoại lệ, cần kiểm tra bằng boxplot và so sánh với JobRole/JobLevel.
- **YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager**: Giá trị cao (40, 18, 15, 17) có thể hiếm, cần kiểm tra phân bố.
- **EmployeeCount, Over18, StandardHours**: Chỉ có một giá trị, không mang thông tin.

## 3. Đề xuất xử lý dữ liệu
1. **Kiểm tra ngoại lệ**:
   - Sử dụng boxplot và phương pháp IQR để xác định ngoại lệ trong DailyRate, MonthlyIncome, MonthlyRate, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager.
   - Kiểm tra tính nhất quán giữa MonthlyIncome, JobRole, và JobLevel.
2. **Loại bỏ cột không mang thông tin**:
   - Xóa EmployeeCount, Over18, StandardHours.
3. **Mã hóa biến danh mục**:
   - Áp dụng one-hot encoding cho BusinessTravel, Department, EducationField, JobRole, MaritalStatus, Gender, OverTime.
   - Sử dụng label encoding cho Attrition (Yes: 1, No: 0).
4. **Phân tích phân bố**:
   - Vẽ histogram và boxplot cho cột số để xác định phân bố và ngoại lệ.
   - Kiểm tra tỷ lệ Attrition (Yes/No) để đánh giá mất cân bằng lớp.
5. **Kiểm tra giá trị thiếu**:
   - Đảm bảo không có giá trị NaN hoặc null trong dữ liệu.

## 4. Kết quả sau xử lý

### 4.1 Phân chia tập train-test
- Tập dữ liệu được chia thành tập huấn luyện và kiểm tra (thường tỷ lệ 80:20 hoặc 70:30) để đánh giá mô hình học máy.

### 4.2 Kiểm tra giá trị null
- Kết quả: Không có giá trị null trong bất kỳ cột nào.

### 4.3 Kiểm tra giá trị trùng lặp
- Kết quả: Không có giá trị trùng lặp trong cột EmployeeNumber, đảm bảo mỗi nhân viên có ID duy nhất.

### 4.4 Kiểm tra ngoại lệ
- **Phương pháp**: Sử dụng boxplot để kiểm tra các cột số: Age, DailyRate, DistanceFromHome, Education, EnvironmentSatisfaction, HourlyRate, JobInvolvement, JobLevel, JobSatisfaction, MonthlyIncome, MonthlyRate, NumCompaniesWorked, PercentSalaryHike, PerformanceRating, RelationshipSatisfaction, StockOptionLevel, TotalWorkingYears, TrainingTimesLastYear, WorkLifeBalance, YearsAtCompany, YearsInCurrentRole, YearsSinceLastPromotion, YearsWithCurrManager.
- **Kết quả**:
  1. **Age**: Phân bố đều (18–60), không có ngoại lệ, tập trung ở 30–40 tuổi.
  2. **DailyRate**: Nhiều ngoại lệ ở cả hai phía (cao/thấp), phân bố rộng.
  3. **DistanceFromHome**: Một vài ngoại lệ >25 km, đa số <20 km.
  4. **Education, EnvironmentSatisfaction, JobInvolvement, JobLevel, JobSatisfaction, PerformanceRating, RelationshipSatisfaction, StockOptionLevel, TrainingTimesLastYear, WorkLifeBalance**: Không có ngoại lệ.
  5. **HourlyRate**: Một vài ngoại lệ nhẹ, phân bố không đều.
  6. **MonthlyIncome**: Nhiều ngoại lệ ở giá trị cao (>20.000), đa số <10.000.
  7. **MonthlyRate**: Nhiều ngoại lệ ở giá trị cao, có thể do phụ cấp.
  8. **NumCompaniesWorked**: Ngoại lệ ở giá trị 9, đa số <5.
  9. **PercentSalaryHike**: Ngoại lệ >20%, phổ biến 10–15%.
  10. **TotalWorkingYears**: Ngoại lệ >35 năm, đa số <20 năm.
  11. **YearsAtCompany**: Ngoại lệ >30 năm, đa số <10 năm.
  12. **YearsInCurrentRole**: Ngoại lệ >15 năm.
  13. **YearsSinceLastPromotion**: Ngoại lệ >15 năm.
  14. **YearsWithCurrManager**: Ngoại lệ >15 năm.
- **Đánh giá**: Ngoại lệ chiếm tỷ lệ đáng kể (không phải 50%, cần kiểm tra cụ thể), nhưng giữ lại do đặc thù công ty (ví dụ: MonthlyIncome cao ở vai trò quản lý).

### 4.5 Mã hóa biến danh mục
- Áp dụng one-hot encoding cho BusinessTravel, Department, EducationField, JobRole, MaritalStatus, Gender, OverTime.
- Sử dụng label encoding cho Attrition (Yes: 1, No: 0).

### 4.6 Scaling dữ liệu
- **Lý do**: Các cột như MonthlyIncome, MonthlyRate, DailyRate có giá trị lớn, gây mất ổn định cho SVM và Logistic Regression.
- **Phương pháp**: Áp dụng StandardScaler để chuẩn hóa dữ liệu, đảm bảo mô hình hội tụ nhanh hơn.

## 5. Thống kê dữ liệu
- **Age**: Trung bình 36.77, độ lệch chuẩn 9.20, trung vị 36, phân bố hơi lệch về 30–40 tuổi.
- **DailyRate**: Trung bình 799.41, độ lệch chuẩn 405.73, trung vị 796.5, phân bố khá đối xứng.
- **DistanceFromHome**: Trung bình 9.26, độ lệch chuẩn 8.15, trung vị 7, lệch phải.
- **Education**: Trung bình 2.90, trung vị 3, độ lệch chuẩn 1.04.
- **EnvironmentSatisfaction**: Trung bình 2.70, trung vị 3.
- **HourlyRate**: Trung bình 66.67, độ lệch chuẩn 20.46, trung vị 67, khá đối xứng.
- **JobInvolvement**: Trung bình 2.72, trung vị 3.
- **JobLevel**: Trung bình 2.03, trung vị 2, độ lệch chuẩn 1.10.
- **MonthlyIncome**: Trung bình 6483.64, độ lệch chuẩn 4714.19, trung vị 4908, lệch phải.
- **MonthlyRate**: Trung bình 14311.30, độ lệch chuẩn 7118.93, trung vị 14235.5, khá đối xứng.
- **NumCompaniesWorked**: Trung bình 2.67, trung vị 2, độ lệch chuẩn 2.50.
- **PercentSalaryHike**: Trung bình 15.18%, trung vị 14%, độ lệch chuẩn 3.67.
- **RelationshipSatisfaction**: Trung bình 2.69, trung vị 3.
- **StockOptionLevel**: Trung bình 0.81, trung vị 1, độ lệch chuẩn 0.86.
- **TotalWorkingYears**: Trung bình 11.12, trung vị 10, độ lệch chuẩn 7.81.
- **TrainingTimesLastYear**: Trung bình 2.80, trung vị 3, độ lệch chuẩn 1.30.
- **WorkLifeBalance**: Trung bình 2.75, trung vị 3.
- **YearsAtCompany**: Trung bình 6.93, trung vị 5, độ lệch chuẩn 6.09, lệch phải.
- **YearsInCurrentRole**: Trung bình 4.21, trung vị 3, độ lệch chuẩn 3.61, lệch phải.
- **YearsSinceLastPromotion**: Trung bình 2.11, trung vị 1, độ lệch chuẩn 3.12, lệch phải.
- **YearsWithCurrManager**: Trung bình 4.03, trung vị 3, độ lệch chuẩn 3.53, lệch phải.

## 6. Kết luận
Tập dữ liệu với 1470 dòng, 35 cột cung cấp thông tin toàn diện về nhân viên, phù hợp để phân tích tỷ lệ nghỉ việc (Attrition). Các cột như DailyRate, MonthlyIncome, MonthlyRate, YearsAtCompany có ngoại lệ nhưng nên giữ lại do đặc thù công ty. Các cột EmployeeCount, Over18, StandardHours không mang thông tin và nên loại bỏ. Sau xử lý (kiểm tra null, trùng lặp, mã hóa, scaling), dữ liệu sẵn sàng cho các mô hình học máy như SVM và Logistic Regression. Cần phân tích thêm tỷ lệ Attrition và tương quan với các cột để tối ưu hóa dự đoán.