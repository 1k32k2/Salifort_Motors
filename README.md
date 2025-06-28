# Dự đoán nghỉ việc của công ty Salifort Motors

Mục đích của dự án này là nhằm tìm hiểu xem tại sao nhân viên lại nghỉ việc và có cách nào dự đoán được chuyện đó không. Đây là một việc làm khá quan trọng vì giữ chân nhân tài luôn tốt hơn, ít tốn thời gian hơn, cũng như ít tốn kém hơn là tuyển nhân viên mới. 

## Trong bộ dataset này có tổng cộng 14,999 dòng, mỗi dòng có 10 cột bao gồm:
| Cột | Ý nghĩa |
| ----------- | ----------- |
| satisfaction_level | Mức độ hài lòng của nhân viên |
| last_evaluation | Điểm đánh giá hiệu suất gần nhất của nhân viên |
| number_project | Tổng số dự án mà nhân viên đã tham gia |
| average_monthly_hours | Số giờ làm việc trung bình hàng tháng của nhân viên |
| time_spend_company | Thời gian (số năm) nhân viên làm việc tại công ty |
| Work_accident | Thông tin cho biết nhân viên có từng gặp tai nạn lao động hay không |
| left | Biến mục tiêu, cho biết liệu nhân viên đó có nghỉ việc hay không (Đây là biến cần dự đoán) |
| promotion_last_5years | Thông tin về việc nhân viên có được thăng chức trong 5 năm gần nhất hay không |
| Department | Bộ phận hoặc phòng ban làm việc của nhân viên |
| salary | Mức lương của nhân viên (có thể ở các cấp độ như 'low', 'medium', 'high') |

## Bước 1: Quan sát dữ liệu
Đây là một phần của dữ liệu (ảnh)

1

Không có ô nào không chứa dữ liệu (null) (ảnh)

2

Có 3008 dòng trùng dữ liệu với nhau (ảnh)

3

Kiểm tra dữ liệu ngoại lai bằng biểu đồ (ảnh)

4

Đào sâu và dữ liệu có sẵn, ta có thể thấy rằng đã có 1991 nhân viên đã nghỉ việc và 10,000 không nghỉ việc

5

Thời gian mỗi tháng dành cho các dự án (ảnh)

6

Đáng nhận thấy, số người rời đi ở 7 dự án là 145 người; chiếm tỉ lệ 100% (ảnh)

7

Số giờ trung bình trong tháng so với điểm đánh giá hiệu suất (ảnh)

8

Sự hài lòng so với thâm niên (ảnh)

9

Phân bổ lương theo thâm niên (ảnh)

10

Trung bình giờ trong tháng so với lần đánh giá cuối cùng (ảnh)

11

Mối quan hệ giữa giờ trung bình tháng với thăng chức (ảnh)

12

Lượng nhân viên không nghỉ/đã nghỉ giữa các phòng ban ( ảnh)

13

Mối tương quan giữa các hệ số (ảnh)

14

## Xây dựng mô hình dự đoán Logistic Regression

Mối tương quan giữa các hệ số 

15

Sau khi thực hiện huấn luyện mô hình, ta thu được Confusion Matrix sau

17

Độ chính xác của mô hình

18

## Xây dựng mô hình bằng Decision Tree và Random Forest

### Giai đoạn 1:

Tìm mô hình tối ưu cho Decision Tree

19

Độ chính xác của Decision Tree

20

Tìm mô hình tối ưu cho Random Forest

21

So sánh evaluation score của tập train đối với Decision Tree và Random Forest

22

### Giai đoạn 2:

Sau khi nhận thấy có nguy cơ rò rỉ dữ liệu, chúng tôi đã tiến hành xử lý.

Chúng tôi nhận thấy rằng có một số nhân viên không có đánh giá mức độ hài lòng. Bên cạnh đó, cột ```average_monthly_hours``` cũng bị chúng tôi coi là rò rỉ dữ liệu. Nếu một nhân viên có kế hoạch nghỉ việc từ trước hoặc bị sa thải, họ cũng có số giờ làm ít hơn. Vì thế, chúng tôi đã tách cột này ra khỏi bảng dữ liệu.

So sánh mô hình Decision Tree trước và sau

23

Nhìn chung điểm số đã giảm đi chút ít, chúng tôi cho rằng điều đó là do việc cắt bớt dữ liệu. Tuy nhiên, nhìn chung thì kết quả vẫn tốt.

Sau khi tiến hành train mô hình Random Forest lần 2 thì ta được bảng kết quả sau

24

Confusion matrix của Random Forest 

25


Mô hình tree 

16

Độ quan trọng giữa các tham số đối với các mô hình

27

28

## Tổng kết

Mô hình Hồi quy tuyếb tính đạt được 80% precision, 83% recall, 80% f1-score và độ chính xác 83% trên tập test.

Sau khi áp dụng feature engineering, DEcision Tree đạt 93,8% AUC, 87% precision, 90,4% recall, 88,7% f1-score và độ chính xác 96,2% trên tập test. Random Forest cho hiệu suất cao hơn Decision Tree.

## Kết luận, đề xuất và hướng đi tiếp theo:

Thông qua những gì đã thấy, ta có thể kết luận rằng nhân viên đã bị quá tải.

Để giữ chân người tài, chúng tôi đề xuất như sau:
- Giới hạn số lượng dự án nhân viên làm cùng lúc.
- Cân nhắc thăng chức cho những người đã làm trên 4 năm, hoặc tìm hiểu sâu hơn tại sao những người này không hài lòng với công việc.
- Có thể thưởng thêm cho những người làm quá giờ, hoặc không bắt họ làm quá giờ.
- Nếu nhân viên không đồng ý với chính sách làm thêm giờ của công ty, hãy thông báo cho họ. Nên làm rõ ràng về khối lượng công việc và thời gian nghỉ.
- Tổ chức các cuộc họp cho toàn công ty và cho từng nhóm nhỏ để hiểu và giải quyết các vấn đề liên quan đến văn hóa công ty, trên mọi phương diện và trong các bối cảnh cụ thể.
- Điểm đánh giá cao không nên dành cho những người làm 200+ giờ mỗi tháng. Cân nhắc chuyển sang thang điểm khác để khen thưởng những người có đóng góp nhiều hơn.
