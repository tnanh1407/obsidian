stitch-mcp tool list_projects : Lấy ra danh sách projects
stitch-mcp tool list_projects | ConvertFrom-Json | % projects | ft title, name : lấy ra danh sách ngắn gọn hơn
stitch-mcp tool delete_project -d '{"name":"projects/<MÃ_ID_DỰ_ÁN>"}' : Xóa tên dự án

$data = '{"name":"projects/<MÃ_ID_DỰ_ÁN>"}'
stitch-mcp tool delete_project -d $data

