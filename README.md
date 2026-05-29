# Tra cứu Dược thư Quốc gia

PWA tra cứu thông tin thuốc — Dược thư Quốc gia Việt Nam 2018 (683 chuyên luận).
Chạy tĩnh, không cần backend, hoạt động offline.

## Cấu trúc
- `index.html` — app
- `data.json` — dữ liệu thuốc
- `manifest.json`, `sw.js` — PWA
- `icon*.png`, `icon.svg`, `maskable-512.png` — icon
- `supabase/supabase_import.sql` — (tùy chọn) chuyển sang Supabase
- `HUONG_DAN.md` — hướng dẫn deploy chi tiết

## Deploy nhanh
Upload toàn bộ lên GitHub → Import vào Vercel (Framework: Other, để trống Build/Output) → Deploy.
Chi tiết xem `HUONG_DAN.md`.
