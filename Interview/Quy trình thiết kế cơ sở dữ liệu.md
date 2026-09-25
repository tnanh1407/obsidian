# I , Chuẩn hóa cơ sở dữ liệu
## 1. Định Nghĩa
-  là khái niệm quan trọng
- tối ưu hóa cấu trúc CSDL bằng cách giảm thiểu sự trùng lặp dữ liệu và cải thiện tính toàn vẹn dữ liệu.
- Chuẩn hóa là một tập hợp các quy tắc và hướng dẫn giúp tổ chức dữ liệu một cách hiệu quả và ngăn ngừa các lỗi dữ liệu phổ biến như lỗi cập nhật, lỗi chèn và lỗi xóa.\
## 2. Tại sao cần chuẩn hóa dữ liệu
- **Toàn vẹn dữ liệu** : Chuẩn hóa giúp duy trì độ chính xác và tính nhất quán của dữ liệu bằng cách giảm thiểu sự trùng lặp. Khi dữ liệu được lưu trữ theo cách không lặp lại, nó ít dễ bị lỗi hơn.
- **Lưu trữ hiệu quả** : Các cơ sở dữ liệu đã được chuẩn hóa thường chiếm ít không gian lưu trữ hơn vì dữ liệu trùng lặp được giảm thiểu. Điều này giúp giảm chi phí lưu trữ tổng thể.
- **Tối ưu hóa truy vấn:** Các truy vấn trở nên hiệu quả hơn trong các cơ sở dữ liệu đã được chuẩn hóa vì chúng chỉ cần truy cập các bảng nhỏ, được cấu trúc tốt thay vì các bảng lớn, chưa chuẩn hóa.
- **Tính linh hoạt** : 1. Các cơ sở dữ liệu đã được chuẩn hóa có tính linh hoạt hơn khi cần thích ứng với những thay đổi về yêu cầu dữ liệu hoặc quy tắc kinh doanh.

## 3. Các cấp độ chuẩn hóa
![[Pasted image 20260911142850.png]]
- **Dạng chuẩn thứ nhất (1NF)** : Đảm bảo rằng mỗi cột trong bảng chứa các giá trị nguyên tử, không thể chia nhỏ. Không được có các nhóm lặp lại, và mỗi cột phải có tên duy nhất.
	![[Pasted image 20260911143022.png]]
- **Dạng chuẩn thứ hai (2NF)** : Dựa trên 1NF, 2NF loại bỏ các phụ thuộc riêng phần. Một bảng ở dạng 2NF nếu nó ở dạng 1NF và tất cả các thuộc tính không khóa đều phụ thuộc hàm vào toàn bộ khóa chính.
	![[Pasted image 20260911143244.png]]
- **Dạng chuẩn thứ ba (3NF)** : Dựa trên 2NF, 3NF loại bỏ các phụ thuộc bắc cầu. Một bảng ở dạng 3NF nếu nó ở dạng 2NF và tất cả các thuộc tính không khóa đều phụ thuộc hàm vào khóa chính, nhưng không phụ thuộc vào các thuộc tính không khóa khác.
	![[Pasted image 20260911143451.png]]
- **Dạng chuẩn Boyce-Codd (BCNF)** : Một phiên bản nghiêm ngặt hơn của 3NF, BCNF đảm bảo rằng mọi phụ thuộc hàm không tầm thường đều là siêu khóa. Điều này có nghĩa là không được phép có các phụ thuộc riêng phần hay phụ thuộc bắc cầu.
	![[Pasted image 20260911143937.png]]
- **Dạng chuẩn thứ tư (4NF)** : 4NF xử lý các phụ thuộc đa giá trị, nơi một thuộc tính phụ thuộc vào một thuộc tính khác nhưng không phải là hàm của khóa chính.
	![[Pasted image 20260911144340.png]]

