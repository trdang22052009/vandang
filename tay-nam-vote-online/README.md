# Tây Nam Vote Online

Ứng dụng bình chọn Đánh / Không đánh, gồm trang bình chọn, màn hình trình chiếu,
trang quản trị, QR Internet và cập nhật trực tiếp qua SSE.

## Lưu trữ
- Lưu phiếu bằng file JSON tại `data/votes.json`.
- Không dùng PostgreSQL, package `pg` hoặc biến `DATABASE_URL`.
- Trên Render Free, filesystem là tạm thời; dữ liệu có thể mất khi restart, redeploy
  hoặc instance bị thay thế. Hãy lưu kết quả ngay sau buổi bình chọn.

## Chạy local
Yêu cầu Node.js 20 trở lên.
```bash
npm install
# Windows PowerShell:
$env:ADMIN_PASSWORD="mat-khau-rieng"
npm start
```
Mở `/vote`, `/screen` hoặc `/admin` tại `http://localhost:3000`.

## Deploy Render Free
1. Đưa dự án lên GitHub và tạo/cập nhật Web Service Node.
2. Build: `npm install`; Start: `npm start`.
3. Đặt `NODE_ENV=production`, `ADMIN_PASSWORD` riêng, và
   `DATA_FILE=/opt/render/project/src/data/votes.json`. Render có thể tự tạo `SESSION_SECRET`.
4. Xóa `DATABASE_URL` khỏi Environment nếu còn. Deploy và kiểm tra `/health`;
   giá trị storage cần là `local-json`. `render.yaml` chỉ tạo Web Service, không tạo PostgreSQL.

## Lưu ý bảo mật
Đổi mật khẩu quản trị trước khi sử dụng. Không công khai mật khẩu hoặc SESSION_SECRET.
