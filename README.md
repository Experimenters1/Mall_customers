# Mall_customers
Customer segmentation via K-Means &amp; Hierarchical clustering

#
### Overview (Tổng quan)
Phân khúc khách hàng là một trong những ứng dụng quan trọng nhất của học tập không giám sát. Sử dụng các kỹ thuật phân cụm, các công ty có thể xác định một số phân khúc khách hàng cho phép họ nhắm mục tiêu cơ sở người dùng tiềm năng. 
#
![image](https://user-images.githubusercontent.com/64000769/218736170-546c3adc-d6a0-4f2c-ab4a-4059d148519e.png)

### Dataset
Bộ dữ liệu được lấy từ kaggle và liên kết được cung cấp bên dưới:
<a href="https://www.kaggle.com/nelakurthisudheer/mall-customer-segmentation" target="_blank">kaggle</a>

Bộ dữ liệu bao gồm năm tính năng sau của 200 khách hàng:
-  CustomerID: ID duy nhất được gán cho khách hàng
-  Gender: Giới tính của khách hàng
-  Age: Tuổi của khách hàng
-  Annual Income (k$): Thu nhập hàng năm của khách hàng
-  Spending Score (1-100): Điểm do trung tâm mua sắm chỉ định dựa trên hành vi và tính chất chi tiêu của khách hàng.

###Thuật toán K-Means là gì
Thuật toán K-Means là một thuật toán phân cụm dữ liệu (clustering) trong học máy. Nó tìm cách chia tập dữ liệu thành k nhóm dựa trên đặc trưng của chúng. Thuật toán hoạt động bằng cách chọn ngẫu nhiên k điểm dữ liệu ban đầu làm trung tâm của k nhóm, sau đó lặp đi lặp lại quá trình gán các điểm dữ liệu vào nhóm gần nhất và cập nhật trung tâm của các nhóm này cho đến khi không có sự thay đổi nào nữa. Kết quả cuối cùng là k nhóm dữ liệu được phân chia và trung tâm của các nhóm đó.

#
The Elbow method là một kỹ thuật được sử dụng trong phân cụm dữ liệu để tìm ra số lượng nhóm tối ưu (tức là giá trị k) để phân cụm dữ liệu. Kỹ thuật này hoạt động bằng cách lặp lại thuật toán phân cụm với các giá trị k khác nhau, sau đó tính toán tổng bình phương khoảng cách giữa các điểm dữ liệu và trung tâm của các nhóm tương ứng với mỗi giá trị k. Kết quả được biểu thị trên biểu đồ dạng đường cong, và số lượng nhóm tối ưu được chọn là điểm gập của đường cong này (tức là điểm trên đường cong mà khi ta kết nối nó với điểm bắt đầu của đường cong, tạo ra một góc "khuỷu tay" giống như khuỷu tay của khuỷu tay con người). Phương pháp này được gọi là "Elbow" vì điểm gập trên đường cong thường trông giống như khuỷu tay.

#
###Within-Cluster-Sum-of-Squares (WSS)
Within-Cluster-Sum-of-Squares (WSS) là một phương pháp đánh giá chất lượng phân cụm trong học máy. WSS là tổng bình phương khoảng cách giữa mỗi điểm dữ liệu và trung tâm của nhóm nó thuộc về. Phương pháp này cũng được gọi là Sum of Squared Errors (SSE). Mục đích của WSS là đánh giá mức độ tập trung dữ liệu trong từng nhóm phân cụm. Nếu WSS nhỏ, có nghĩa là dữ liệu trong từng nhóm phân cụm được tập trung và phân chia tốt. Ngược lại, nếu WSS lớn, có nghĩa là dữ liệu trong nhóm không được tập trung và phân chia không tốt. WSS thường được sử dụng kết hợp với phương pháp Elbow để tìm số lượng nhóm tối ưu trong phân cụm dữ liệu.

Công thức tính toán WSS/SSE trong phân cụm K-Means là:

WSS = Σi=1->k Σx∈Ci (distance(x, ci))^2

Trong đó:

+) k là số lượng nhóm cần phân chia
+) Ci là tập hợp các điểm dữ liệu thuộc nhóm thứ i
+) x là một điểm dữ liệu bất kỳ trong tập dữ liệu
+) ci là trung tâm của nhóm thứ i
+) distance(x, ci) là khoảng cách Euclid giữa x và ci


![image](https://user-images.githubusercontent.com/64000769/218742831-e82ce293-3872-4e75-a3a8-7c50bbf49ca1.png)
![image](https://user-images.githubusercontent.com/64000769/218743160-a41ecf3e-9434-4279-b9aa-1ec79998c442.png)

#
###Hierarchical clustering
Hierarchical clustering là một kỹ thuật phân cụm dữ liệu được sử dụng trong học máy để tìm kiếm cấu trúc tự nhiên của dữ liệu. Phương pháp này sử dụng thuật toán để xây dựng một cấu trúc phân cấp của các nhóm dữ liệu, bắt đầu từ việc mỗi điểm dữ liệu được coi là một nhóm đơn lẻ. Sau đó, các nhóm được gộp lại thành các nhóm lớn hơn, dựa trên khoảng cách giữa chúng, và quá trình này được tiếp tục cho đến khi tất cả các điểm dữ liệu được gộp vào một nhóm duy nhất.

Hierarchical clustering có hai loại chính: phân cấp trên xuống (agglomerative) và phân cấp dưới lên (divisive). Phương pháp phân cấp trên xuống là phổ biến hơn, bắt đầu với mỗi điểm dữ liệu là một nhóm riêng biệt và gộp các nhóm lại với nhau dựa trên khoảng cách giữa chúng, bắt đầu từ những cặp nhóm có khoảng cách gần nhau nhất. Trong quá trình này, một cây phân cấp (dendrogram) được xây dựng, cho thấy sự phân nhánh của các nhóm dữ liệu. Kết quả của hierarchical clustering thường được biểu diễn bằng dendrogram, cho phép ta quan sát cấu trúc của dữ liệu và chọn số lượng nhóm phù hợp cho mục đích của mình.
![image](https://user-images.githubusercontent.com/64000769/218746533-f263a787-d3ee-4de2-b987-4296e0ed885c.png)

#
###Dendrogram
Dendrogram là một biểu đồ cây phân cấp được sử dụng để mô tả cấu trúc phân cụm của dữ liệu trong phương pháp hierarchical clustering. Dendrogram có thể được sử dụng để trực quan hóa sự phân nhánh của các nhóm dữ liệu và khoảng cách giữa chúng. Trong dendrogram, mỗi nhóm được biểu diễn bằng một nút trên cây, và khoảng cách giữa các nhóm được biểu thị bằng chiều dài của các cành trên cây. Các nhóm được gộp lại tại các nút cha chung, và quá trình này được tiếp tục cho đến khi tất cả các điểm dữ liệu được gộp vào một nhóm duy nhất.

Dendrogram thường được sử dụng để chọn số lượng nhóm phù hợp trong phân cụm hierarchical clustering. Khi ta quan sát dendrogram, ta có thể chọn số lượng nhóm bằng cách cắt cây ở một chiều cao (hoặc giá trị khoảng cách) nhất định, và các nhóm được gộp lại ở mức độ này sẽ được coi là số lượng nhóm phù hợp. Dendrogram cũng có thể được sử dụng để đánh giá chất lượng của các phương pháp phân cụm khác, bằng cách so sánh cấu trúc phân nhánh của các cây phân cấp khác nhau.


![image](https://user-images.githubusercontent.com/64000769/218750864-95024fae-80ac-4007-905c-3de39e4c8aa7.png)






