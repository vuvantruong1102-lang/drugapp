# Tra cứu Dược thư Quốc gia — Hướng dẫn triển khai

App tra cứu thông tin thuốc (Dược thư Quốc gia Việt Nam 2018), 683 chuyên luận. PWA chạy như app native, cài được lên màn hình chính, hoạt động offline.

## Các file trong gói
- `index.html` — toàn bộ app (giao diện + logic)
- `data.json` — dữ liệu 683 thuốc (đọc tĩnh, không cần backend)
- `manifest.json`, `sw.js` — cấu hình PWA + service worker (offline + cài đặt)
- `icon.svg`, `icon-192.png`, `icon-512.png`, `maskable-512.png` — icon app
- `supabase_import.sql` — (tùy chọn) script chuyển dữ liệu sang Supabase sau này

> Khi đưa lên GitHub, **không cần** upload `supabase_import.sql` nếu chỉ chạy bản tĩnh. Các file còn lại phải nằm ở **thư mục gốc** của repo (cùng cấp với `index.html`).

## Triển khai — hoàn toàn trên trình duyệt

### Bước 1 — Tạo repo GitHub
1. Vào github.com → nút **New** (tạo repository mới).
2. Đặt tên, ví dụ `duocthu-app`. Chọn **Public**. Nhấn **Create repository**.
3. Ở trang repo trống, nhấn **uploading an existing file**.
4. Kéo–thả tất cả các file trong gói (trừ file SQL nếu không cần) vào ô upload.
5. Nhấn **Commit changes**.

### Bước 2 — Deploy bằng Vercel
1. Vào vercel.com → đăng nhập bằng tài khoản GitHub.
2. Nhấn **Add New → Project**.
3. Chọn repo `duocthu-app` vừa tạo → **Import**.
4. Vercel tự nhận đây là trang tĩnh. Phần **Framework Preset** để **Other**, các ô Build/Output để trống.
5. Nhấn **Deploy**. Đợi ~30 giây.
6. Xong! Vercel cho một đường link dạng `https://duocthu-app.vercel.app`.

### Bước 3 — Cài lên điện thoại (PWA)
1. Mở link Vercel bằng **Chrome trên Android**.
2. Nhấn menu (⋮) góc trên phải → **Thêm vào màn hình chính** (Add to Home screen).
3. App xuất hiện với icon riêng, mở ra chạy **toàn màn hình** như app thật, dùng được cả khi mất mạng.

> iPhone: mở bằng **Safari** → nút Chia sẻ → **Thêm vào MH chính**.

## Cập nhật dữ liệu sau này
Sửa `data.json`, vào repo GitHub → mở file → biểu tượng bút chì (Edit) → dán nội dung mới → Commit. Vercel tự deploy lại. Trên máy người dùng, service worker sẽ tự lấy bản mới ở lần mở kế tiếp (có thể cần mở lại app 1–2 lần để cache cập nhật).

## Nếu muốn chuyển sang Supabase
Mở `supabase_import.sql`, copy toàn bộ, dán vào **SQL Editor** trong project Supabase rồi Run. Bảng `thuoc` sẽ được tạo và nạp đủ 683 dòng, đã bật RLS cho phép đọc công khai. Khi đó cần sửa `index.html` để gọi Supabase thay vì `fetch('data.json')` — mình có thể làm bước này khi bạn cần.

## Lưu ý chuyên môn
Dữ liệu được trích tự động từ file PDF Dược thư Quốc gia 2018. Phần lớn chính xác, nhưng với quyết định lâm sàng nên đối chiếu lại với bản gốc. Các nhãn "Cấm / Thận trọng" ở 5 nhóm đối tượng (phụ nữ có thai, trẻ em, người già, suy gan, suy thận) được phân loại tự động dựa trên nội dung chuyên luận, mang tính hỗ trợ tra cứu nhanh.
