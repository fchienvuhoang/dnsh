# danasangha.org

Project website tĩnh sẵn sàng build trên Vercel: trang giới thiệu, `/privacy/`, `/terms/`. Đây là website thông tin cho Google OAuth Branding, không bao gồm backend đọc Gmail hay bóc tách sao kê.

## Chạy trên máy

Yêu cầu Node.js 22 trở lên. Không cần Python hoặc thư viện ngoài.

```sh
npm install
npm run dev
```

Mở http://localhost:4173.

## Deploy Vercel

1. Đưa project này lên repository GitHub của bạn.
2. Trong Vercel chọn Add New → Project → Import repository.
3. Root Directory: thư mục gốc project; Framework Preset: Other.
4. Build Command: `npm run build`; Output Directory: `dist` (đã khai báo trong `vercel.json`).
5. Chọn Deploy. Không cần biến môi trường hoặc API key.
6. Trong Settings → Domains thêm `danasangha.org`, rồi cập nhật DNS theo hướng dẫn Vercel.

Hoặc dùng Vercel CLI từ thư mục project: `npx vercel` để tạo preview, `npx vercel --prod` để deploy production.

## Nội dung chính sách

Sửa `site.config.json` để cập nhật thông tin. Nội dung trang nằm trong `scripts/build.mjs`, giao diện trong `public/styles.css`.

`npm run build` luôn tạo bản có thể deploy. Khi thiếu thông tin hoặc `reviewed` chưa là `true`, website hiển thị banner bản nháp, các mục cần bổ sung và chỉ thị noindex. Không dùng bản nháp để gửi Google xét duyệt.

Để hoàn thiện: điền `operator` (cá nhân/tổ chức vận hành), `retentionAndDeletion` (vòng đời email, tệp, giao dịch, token, log/cache và cách yêu cầu xóa), `securityMeasures` (biện pháp thực tế). Đối chiếu toàn bộ nội dung với ứng dụng, sau đó đặt `reviewed: true`. `npm run build:reviewed` kiểm tra thông tin này và từ chối build nếu còn thiếu. Cam kết trên website không tự triển khai bảo mật trong backend.

Thông tin đã cung cấp: tên danasangha; email fchienvuhoang@gmail.com; lấy sao kê VIB từ Gmail, chuyển sang chức năng bóc tách chạy trên Vercel; không dùng AI; chủ ứng dụng cho biết không lưu dữ liệu Gmail. Việc lưu giao dịch sau bóc tách và chi tiết log/cache/token cần xác nhận thêm.

## Google Auth Platform → Branding

- Application home page: `https://danasangha.org/`
- Privacy policy: `https://danasangha.org/privacy/`
- Terms of service: `https://danasangha.org/terms/`
- Authorized domains: `danasangha.org`

Các trang phải công khai, không yêu cầu đăng nhập. Xác minh domain bằng giá trị DNS TXT do Google Search Console cấp nếu được yêu cầu. Callback OAuth phải là URL thực tế của ứng dụng xử lý đăng nhập. Publish app không đồng nghĩa hoàn tất xét duyệt quyền Gmail.

Tài liệu: [Vercel configuration](https://vercel.com/docs/project-configuration/vercel-json), [Google OAuth policies](https://developers.google.com/identity/protocols/oauth2/policies), [Restricted scope verification](https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification).
