# danasangha.org · danasangha

Website tĩnh phục vụ phần Branding của Google OAuth / Google Auth Platform. Không phải ứng dụng nhập sao kê và không chứa chức năng OAuth, khóa API hay backend.

## Xem trước

Yêu cầu Node.js 18+ và Python 3. Không cần cài thư viện.

```sh
npm run dev
```

Mở http://localhost:4173. Bản nháp có banner, noindex và các mục cần bổ sung.

## Hoàn thiện nội dung

Sửa `site.config.json`:

- `appName`: tên trùng màn hình OAuth consent.
- `operator`: tên cá nhân hoặc tổ chức thực sự vận hành.
- `supportEmail`: email hỗ trợ hoạt động.
- `processingAndStorage`: xử lý trên máy hay server; vị trí lưu email, tệp đính kèm, giao dịch, OAuth token; nơi lưu trữ và đơn vị vận hành hạ tầng.
- `retentionAndDeletion`: thời hạn cho từng loại dữ liệu, cách yêu cầu xóa, thời gian xử lý, bản sao lưu và trường hợp giữ lại theo pháp luật.
- `thirdPartyServices`: tên nhà cung cấp, mục đích, dữ liệu chuyển giao; ghi rõ có sử dụng AI hay không.
- `securityMeasures`: biện pháp bảo vệ thực sự được triển khai.

Đối chiếu toàn bộ văn bản trong `scripts/build.mjs` với ứng dụng thực tế, nhất là dữ liệu truy cập, chức năng, cam kết Limited Use và việc dùng AI. Theo chủ ứng dụng, danasangha chỉ đọc Gmail, lấy tệp sao kê và chuyển sang phần mềm bóc tách giao dịch, không lưu dữ liệu tại ứng dụng đọc Gmail. Cần xác nhận tên phần mềm nhận tệp, cách lưu trữ tại phần mềm đó, dịch vụ AI, OAuth token và log/cache trước khi công khai. Chỉ đặt `reviewed` thành `true` sau khi hoàn tất đối chiếu. Nội dung cam kết trên trang không tự triển khai cơ chế bảo vệ dữ liệu trong ứng dụng.

```sh
npm run build
```

Lệnh này sẽ từ chối xuất bản nếu thiếu cấu hình hoặc chưa đánh dấu đã rà soát. Thư mục `dist/` là toàn bộ kết quả; không đưa mã nguồn/cấu hình riêng lên web.

## Triển khai domain

Đưa nội dung `dist/` lên hosting tĩnh như Cloudflare Pages, Netlify hoặc Nginx. Build command: `npm run build`; output directory: `dist`. Kết nối domain `danasangha.org` qua mục Custom domains của hosting và làm theo bản ghi DNS mà nhà cung cấp hiển thị. Bật HTTPS. `/privacy` và `/terms` cần được redirect sang thư mục tương ứng; các hosting hỗ trợ directory index thường tự xử lý.

Nginx có thể dùng `try_files $uri $uri/ =404;` với root trỏ đến thư mục dist. Không rewrite mọi URL sang trang chủ.

Kiểm tra các trang công khai không cần đăng nhập:

- https://danasangha.org/
- https://danasangha.org/privacy/
- https://danasangha.org/terms/

Trong Google Auth Platform → Branding:

- Application home page: `https://danasangha.org/`
- Privacy policy: `https://danasangha.org/privacy/`
- Terms of service: `https://danasangha.org/terms/`
- Authorized domains: `danasangha.org`

Xác minh domain bằng Google Search Console theo yêu cầu Google. Nếu được cấp DNS TXT hoặc tệp HTML xác minh, sử dụng đúng giá trị do Google cấp; không có mã xác minh chung để tự tạo. Nếu dùng tệp HTML, đặt trong public/ và bổ sung bước copy vào build script, hoặc đưa thẳng vào hosting.

Audience → Publish app không đồng nghĩa hoàn tất xác minh scope. Quyền như gmail.readonly thuộc nhóm restricted; Google có thể yêu cầu scope verification, video mô tả luồng cấp quyền, và đánh giá bảo mật tùy cách dữ liệu được xử lý. Cấu hình redirect URI phải dùng callback thật của ứng dụng, không tự dùng domain website giới thiệu.

Tài liệu chính thức:
- https://developers.google.com/identity/protocols/oauth2/policies
- https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification

## Thông tin chủ ứng dụng đã cung cấp

- Tên: danasangha.
- Email hỗ trợ: fchienvuhoang@gmail.com.
- Tệp sao kê: ngân hàng VIB.
- Máy chủ nhận và bóc tách: Vercel.
- Không dùng AI để đọc hoặc lưu dữ liệu; không lưu dữ liệu Gmail theo mô tả của chủ ứng dụng.
- Chưa xác nhận: tên cá nhân/tổ chức vận hành, vòng đời dữ liệu giao dịch sau bóc tách, log/cache/token và biện pháp bảo mật thực tế.
