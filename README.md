# Yibohuy ☀️ Weather Forecast PWA (Dự Báo Thời Tiết)

**VN:** *Yibohuy* là website/ứng dụng PWA dự báo thời tiết vui nhộn, dễ dùng cho người Việt. Bạn có thể xem **thời tiết hôm nay**, **dự báo 5 ngày** và **tìm kiếm theo thành phố** để xem chi tiết **từng giờ**.  
**EN:** *Yibohuy* is a friendly **Weather Forecast PWA**. Check **today’s weather**, **5-day forecast**, and **search by city** to see **hourly details**.

> **SEO keywords (natural):** dự báo thời tiết, thời tiết hôm nay, dự báo 5 ngày, tìm kiếm thành phố, thời tiết từng giờ, ứng dụng PWA.

---

## Highlights / Điểm nổi bật

- **Weather at a glance**:  
  **VN:** Hiển thị thẻ thời tiết hiện tại (mặc định tải cho *Hà Nội*).  
  **EN:** Shows current weather (auto-loads for *Hanoi*).

- **5-Day Forecast**:  
  **VN:** Dự báo theo ngày (tối đa 5 ngày hiển thị).  
  **EN:** Daily forecast (up to 5 days shown).

- **City Search + Hourly Forecast**:  
  **VN:** Nhập tên thành phố hoặc chọn nhanh “chips” để xem kết quả.  
  **EN:** Search by city name or tap quick chips to view results.

- **Learn + Quiz**:  
  **VN:** Trang “Học Thời Tiết” có nội dung theo modal và mini quiz.  
  **EN:** A “Learn Weather” section with modal content and a mini quiz.

- **PWA Installation & Offline Assets**:  
  **VN:** Có banner “Cài Yibohuy về máy!”, hỗ trợ chế độ standalone.  
  **EN:** Install banner + `display: standalone` support.

- **Performance & UX (SPA navigation)**:  
  **VN:** Điều hướng nhanh giữa các mục (Trang Chủ / Học Thời Tiết / Tìm Kiếm).  
  **EN:** Fast SPA navigation between main sections.

---

## How it works / Cách hoạt động

### Weather Data Source / Nguồn dữ liệu thời tiết
- The site uses **Open-Meteo** APIs:
  - **Geocoding**: city search → latitude/longitude  
  - **Forecast**: weather forecast by coordinates
- **No API key required** for Open-Meteo (free endpoints).

**EN note:** WMO weather codes are mapped to friendly emoji + labels for a more engaging UI.

### SPA Navigation / Điều hướng SPA
- Pages are switched using internal `data-page` navigation (Home / Learn / Search).
- URL shortcut is supported via `?page=search`.

---

## PWA (Manifest + Service Worker) / PWA

### Manifest / manifest.json
- `name`, `short_name`, `description`
- `display: "standalone"`
- Theme & icons:
  - `icon-192.png` / `icon-512.png` (maskable)

### Offline behavior / Chế độ offline
- **Static assets** are cached for offline usage (CSS/JS/fonts).
- **API calls** use a **network-first** strategy:
  - If the network is unavailable, the UI falls back to a JSON error response (so the app won’t crash).

---

## SEO & Social / SEO & Social

- `lang="vi"` and mobile-friendly viewport meta are set.
- Includes:
  - Page title: **“Yibohuy ☀️ Dự Báo Thời Tiết”**
  - Meta description for search snippets
  - Social-ready metadata patterns (description, theme colors)

**Recommended (optional) for best SEO (if you deploy):**
- Add a proper `canonical` tag
- Add OpenGraph tags (`og:title`, `og:description`, `og:image`)
- Ensure correct hosting path so that `manifest.json` and `sw.js` load correctly

> No sensitive or private data is exposed in the repository.

---

## Tech Stack / Công nghệ sử dụng

- **Frontend:** HTML / CSS / Vanilla JavaScript
- **Weather APIs:** Open-Meteo (Geocoding + Forecast)
- **UI behavior:** SPA-style navigation, modal dialogs, quiz interaction
- **PWA:** Manifest + Service Worker caching
- **Fonts:** Google Fonts (Nunito, Baloo 2)

---

## Project Structure / Cấu trúc dự án

- `Web/index.html` — main UI (Home / Learn / Search)
- `Web/style.css` — styling & responsive layout
- `Web/script.js` — data fetching (Open-Meteo), rendering UI, PWA logic
- `Mobile/Manifest.json` — app manifest metadata
- `Mobile/sw.js` — service worker caching & offline behavior

> **Important for deployment (paths):** verify that URLs referenced in `index.html` (e.g. `manifest.json`, `./sw.js`) match your hosting structure.

---

## Run Locally / Chạy cục bộ

**VN:** Vì PWA/Service Worker hoạt động tốt nhất trên môi trường có HTTP, hãy dùng:
- VS Code extension **Live Server**, hoặc
- một local server tĩnh (static server)

**EN:** Serve the project via a local HTTP server (recommended for PWA). Then open the site in a browser.

---

## Privacy & Security / Bảo mật & Quyền riêng tư

- The app does **not** collect or expose personal user data.
- Weather is fetched from Open-Meteo, and offline caching only stores static assets for smoother UX.
- No secrets/API keys are required for Open-Meteo usage.

---

## Credits / Nguồn tham khảo

- Weather data: **Open-Meteo**
- Fonts: **Google Fonts (Nunito, Baloo 2)**

---

## License / Giấy phép

If you want, you can add a LICENSE file (MIT/Apache-2.0, etc.).  
(Hiện repository chưa cung cấp license cụ thể.)
