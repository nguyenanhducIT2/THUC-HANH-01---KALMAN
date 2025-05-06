PHÂN TÍCH CHUỖI THỜI GIAN PODCAST BẰNG KALMAN 


*TQH
mô hình trạng thái ẩn 
(https://imgur.com/a/r07KYqO)
ảnh em vẽ bằng draw.io
 mô hình Kalman Filter, bản chất  là 1 mô hình trạng thái ẩn ,theo em hiểu nó có nghĩa là: dữ liệu mà nhìn thấy như thời gian nghe podcast mỗi ngày chỉ là biểu hiện bên ngoài, còn bên trong sẽ có 1 trạng thái ẩn thật mà mình không nhìn được –như là xu hướng thực sự của người nghe.
Kalman Filter tính các trạng thái ẩn đó theo thời gian, bằng cách kết hợp 2 yt:

Dự đoán từ ngày hôm trướctheo trạng thái trước

Và điều chỉnh lại theo dữ liệu thật ở ngày hôm nay.
 khi khai báo KalmanFilter() và truyền vào các ma trận để em xây dựng 

mô hình 1 hệ thống có trạng thái ẩn

1. Giới thiệu đề tài
Trong bài thực hành này, em triển khai ba mô hình Kalman Filter để phân tích chuỗi thời gian từ dữ liệu nghe Podcast.Theo mã số sinh viên của em, đề bài tương ứng là đề số 4 – tức là phân tích các bản phát hành vào ngày Thứ Năm (Thursday).

2. Dữ liệu sử dụng
Link dữ liệu: https://www.kaggle.com/competitions/playground-series-s5e4/overview
theo đề bài trên teams
Listening_Time_minutes: Tổng thời gian nghe của người dùng ( đây laf biến mục tiêu)

Likes: Số lượt thích

Publication_Day: Ngày phát hành

Một số cột phân loại khác như: Podcast_Name, Genre,...

Em đã lọc dữ liệu theo Publication_Day == "Thursday" để thực hiện đúng yêu cầu đề bài.

3. Tiền xử lý dữ liệu
Các bước em tiền xử lý  gồm có:

Nội suy giá trị thiếu bằng phương pháp nội suy tuyến tính

Mã hóa biến phân loại bằng LabelEncoder cho các cột dạng chuỗi

Chuẩn hóa dữ liệu bằng StandardScaler để đưa các đặc trưng về cùng thang đo

4. Các mô hình Kalman Filter em đã triển khai
4.1 Kalman Filter một chiều 1D)
Làm mượt chuỗi thời gian Listening_Time_minutes

Kết quả đánh giá:

MSE: 410.1238

RMSE: 20.2515

MAE: 16.6921

R²: 0.4702

4.2 Kalman Filter kết hợp hồi quy 
Áp dụng thuật toán EM (Expectation-Maximization) để tối ưu tham số

Kết quả đánh giá tương tự 1D nếu không cos thêm đặc trưng mới

4.3 Kalman Filter đa biến 
Sử dụng thêm biến Likes để dự báo Listening_Time_minutes

Kết quả đánh giá:

MSE: 2787.4065

RMSE: 52.7959

MAE: 44.8697

R²: -2.6008 

5. Trực quan hóa kết quả
Em đã vẽ biểu đồ để so sánh kết quả giữa các mô hình:

Kalman 1D cho kết quả làm mượt ổn định, phù hợp với xu hướng tổng thể

Kalman Regression cải thiện độ khớp so với dữ liệu thực

Kalman M variate chưa cho kết quả tốt, có thể do ảnh hưởng của đặc trưng chưa phù hợp

6. Hướng phát triển
Em dự định tối ưu lại mô hình để cho có đánh giá tốt hơn và  triển khai mô hình trên Streamlit để trực quan hóa kết quả trên giao diện web

Các mô hình tải lên Hugging Face để lưu trữ và sử dụng lại 


7. Cách chạy mã

### **Cài đặt thư viện:**
```bash
pip install -r requirements.txt
```
### **Mở notebook Jupyter để chạy mô hình:**

```bash
jupyter notebook notebooks/kalman_analysis.ipynb
```
