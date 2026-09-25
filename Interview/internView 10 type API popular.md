# 1. REST API

REST không phải giao thức riêng. Nó là phong cách thiết kế API, thường hoạt động trên HTTP/HTTPS và trao đổi dữ liệu bằng JSON.
## Vì sao phổ biến?

- Dễ sử dụng
- Dễ triển khai
- Tương thích với nhiều nền tảng
- Sử dụng HTTP có sẵn
## Hạn chế

### 1. Dư thừa dữ liệu (Over-fetching)

Client chỉ cần tên nhưng API trả về toàn bộ thông tin người dùng:

```json
{
  "id": 1,
  "name": "Ngọc Anh",
  "email": "example@gmail.com",
  "phone": "0123456789",
  "address": "Hà Nội"
}
```
### 2. Thiếu dữ liệu (under - fetching)

Muốn lấy user 

- SOAP API : giao thức nhắn tin có tiêu chuẩn chặt chẽ , thường sử dụng XML
	-  Ưu điểm :
		- quy chuẩn rõ ràng , nghiêm ngặt
	-  Hạn chế :
		- khó học , xml dài dòng , khó debug
	
-  gRPC : làm framework RPC Sử dụng Protocol Buffers để định nghĩa dữ liệu và thường truyền dữ liệu nhị phân qua HTTP/2
	`service VocabularyService {
	  `rpc GetVocabulary(GetVocabularyRequest)
      `returns (VocabularyResponse);
		`}
		`

	- 4 Mô hình  giao tiếp mạnh mẽ
		- giao tiếp 1 chiều Request response : giống như API
		- streaming giúp máy chủ đẩy dữ liệu liên
- GraphQL :
- webhook api : tự động thông báo cho ứng dụng thay đổi thay vì phải truy vấn
- websocket api : trao đổi thông tin 2 chiều
- webRTC :truyền trực tiếp với nhau mà không cần trung gian , gọi video 