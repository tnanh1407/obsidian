# VẤN ĐỀ
- **Stale Data** - dữ liệu bị lỗi thời
- **Duplicate Requests** - Gọi API trùng lặp
- **Mutation Sync** - Không đồng bộ sau khi thay đổi 
=> useEffect kéo dữ liệu về , không thể quản lí được

Fetch , Axios giúp kết nối với server
Tanstack query giúp đồng nhất dữ liệu với UI
1. **Deduplication** : chống trùng lặp request
2. **Background Refetch** : tự động cập nhật dữ liệu ở nền
3. **Automatic Revalidation** : tự đồng bộ sau khi tạo dữ liệu mới
4. **Prefetching** : Tải trước dữ liệu
5. **Optimustic UI** : phản hồi ngay lập tức
Server State : fetch -> catch -> đồng bộ -> retry 

