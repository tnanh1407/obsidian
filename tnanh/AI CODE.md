- AGENTS.md : Nội quy (Làm gì và không được làm gì trong PixelMart).
- .gemini : cấu hình công cụ của IDE file gemini/settings.json khai báo 4 server  MCPP
- .agents  : skill sâu hơn của mcp sinh ra từ câu lệnh npx skills add

## 1. Package trong dự án
trace < debug < info < warn < error < fatal : các level của pino từ thấp đến cao
đặt là silent : tắt log hoàn toàn khi chạy pnpm test : ci 