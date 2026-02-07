# **Báo cáo đề tài: Object Detection - Phát hiện vật thể**

## **Mục tiêu:**
* Xác định vị trí (Bounding Box) và phân loại nhiều vật thể trong cùng một bức ảnh.

# **Notebook này thực hiện quá trình huấn luyện mô hình phát hiện vật thể trên tập dữ liệu đầy đủ COCO 2017**
* Khác với phiên bản thử nghiệm (chỉ chạy trên tập val2017 5000 ảnh), notebook này sẽ huấn luyện trên toàn bộ tập train2017 với hơb 118k ảnh gốc
* Tập huấn luyện (Training Set): Sử dụng train2017 (~118.000 ảnh, 18GB).
  * Mục đích: Dùng để mô hình học các đặc trưng và cập nhật trọng số
* Tập kiểm định (Validation Set): Sử dụng val2017 (5.000 ảnh, 1GB).
  * Mục đích: Dùng để đánh giá khách quan hiệu suất mô hình (tính điểm mAP) sau mỗi epoch, giúp theo dõi quá trình hội tụ và ngăn chặn hiện tượng học vẹt (overfitting).

## **Kiến trúc mô hình:**
* Backbone (ResNet/FPN): Sử dụng ResNet để trích xuất đặc trưng và FPN (Feature Pyramid Network) để giúp mô hình nhận diện tốt vật thể ở nhiều kích thước khác nhau (lớn và nhỏ).
* Detection Head (YOLOstyle): Phần "đầu" dự đoán được thiết kế theo phong cách của YOLO (You Only Look Once), nổi tiếng với tốc độ xử lý nhanh.
* Bộ dữ liệu: COCO 2017: Hơn 200.000 hình ảnh, 80 danh mục vật thể, gồm:
  * Tập huấn luyện (Train 2017): Khoảng 118.000 ảnh. Dùng để huấn luyện chính cho mô hình.
  * Tập kiểm định (Val 2017): 5.000 ảnh. Dùng để kiểm tra hiệu suất và tinh chỉnh siêu tham số trong quá trình huấn luyện.
  * Tập kiểm thử (Test 2017): Khoảng 41.000 ảnh. Là tập kiểm thử. Do tập test 2017 không công khai nhãn (dùng riêng cho các cuộc thi) nên sẽ dùng tập val 2017 để đánh giá kết quả thực nghiệm
  * Tập chứa dữ liệu nhãn (annotations): Đây là các file định dạng JSON chứa tọa độ khung hình, tên đồ vật cho cả tập train và val. Dùng để đánh giá cuối cùng.

## **Các chỉ số chú ý trong báo cáo**
* mAP (Mean Average Precision): Đây là chỉ số quan trọng nhất để biết mô hình của bạn chính xác đến mức nào trên tất cả các loại vật thể.
* AP50: Độ chính xác khi khung hình chữ nhật của bạn khớp với đáp án ít nhất 50% (IoU > 0.5).
* Visualize: Vẽ các khung hình chữ nhật (bounding boxes) lên ảnh thực tế để kiểm tra bằng mắt thường.

