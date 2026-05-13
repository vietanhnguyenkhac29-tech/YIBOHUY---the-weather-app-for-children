# Yibohuy ☀️ — Dự Báo Thời Tiết

**Yibohuy** là một website dự báo thời tiết thân thiện (UI vui nhộn, nhiều hiệu ứng) cho phép người dùng:
- Xem **thời tiết hiện tại** và **dự báo 5 ngày** (trang Home)
- Tìm kiếm theo **tên thành phố** để xem **thời tiết chi tiết theo giờ + 5 ngày** (trang Search)
- “Học thời tiết” theo chủ đề bằng **modal** (trang Learn)
- Chơi **quiz** để củng cố kiến thức về thời tiết (trang Learn)

Website được xây dựng bằng **HTML/CSS/Vanilla JavaScript** (không dùng framework) và lấy dữ liệu từ **Open-Meteo**.

---

## Tính năng nổi bật ✨
- **Home tự động tải** thời tiết cho một thành phố mặc định (Hà Nội).
- **Search theo thành phố**:
  - Tự động geocode (đổi tên thành phố → tọa độ)
  - Hiển thị **Current weather**, **Hourly (tới 24 giờ)**, **Forecast (5 ngày)** và **Details** (độ ẩm, gió, hướng gió, áp suất, UV, bình minh/hoàng hôn, xác suất mưa).
- **Learn modal**:
  - Trời nắng, có mây, trời mưa, dông bão, tuyết rơi, cầu vồng, gió, sương mù…
  - Nội dung học nằm trong `learnData` và mở bằng `openModal(key)`.
- **Quiz thời tiết**:
  - Trắc nghiệm nhiều câu
  - Hiển thị giải thích sau khi chọn đáp án
  - Tính điểm & thông báo kết quả
- **Hiệu ứng giao diện**:
  - Navbar sticky + hamburger cho mobile
  - Particle nền (emoji bay nổi)
  - Animation cho card/forecast/quiz
- **Không cần API key** (theo cấu hình hiện tại).

---

## Demo / Cách xem giao diện
Bạn có thể chạy ngay theo 1 trong các cách sau:

### Cách 1: Mở trực tiếp file HTML
- Mở `Web/index.html` trong trình duyệt.

> Gợi ý: nếu fetch gặp lỗi do chặn CORS/không đúng chế độ, hãy dùng Cách 2.

### Cách 2: Dùng VSCode Live Server (khuyến nghị)
- Cài **Live Server** (extension của VSCode)
- Chuột phải `Web/index.html` → **Open with Live Server**

---

## Cách website hoạt động (luồng xử lý) 🧠
### 1) Geocoding (tên thành phố → tọa độ)
Khi người dùng tìm kiếm:
- Gọi endpoint:
  - `https://geocoding-api.open-meteo.com/v1/search`
- Lấy kết quả đầu tiên (lat, lon, tên hành chính)

### 2) Weather Forecast (tọa độ → dữ liệu thời tiết)
Sau khi có `lat/lon`, gọi:
- `https://api.open-meteo.com/v1/forecast`

Website yêu cầu các nhóm dữ liệu (current/hourly/daily) để render:
- **Current**
- **Hourly**: nhiệt độ, code thời tiết, xác suất mưa
- **Daily**: code thời tiết, nhiệt độ max/min, sunrise/sunset, xác suất mưa tối đa, UV tối đa

### 3) Mapping WMO code → biểu tượng & nhãn
Dữ liệu thời tiết từ Open-Meteo sử dụng **weather_code**.
Website có bảng mapping để hiển thị emoji/nhãn tương ứng (được định nghĩa trong `getWMO(code)`).

### 4) Render UI
Tùy theo trang:
- Home: render card hiện tại + forecast
- Search: render full kết quả (current + hourly + 5 ngày + details)
- Learn: mở modal theo key
- Quiz: render câu hỏi + xử lý đáp án + chuyển câu

---

## Hướng dẫn sử dụng theo từng trang
### 🏠 Trang Home
- Khi tải trang, website tự gọi và hiển thị:
  - Thời tiết hiện tại (card)
  - Dự báo 5 ngày (forecast)
- Nút “Xem thời tiết ngay” dẫn đến trang Search

### 🔍 Trang Search
- Nhập tên thành phố vào ô tìm kiếm
- Hoặc bấm nhanh “chip” thành phố (Hà Nội, Sài Gòn, Đà Nẵng, Huế, …)
- Nhấn nút **Tìm** hoặc bấm **Enter**
- Kết quả xuất hiện:
  - Card thông tin tổng quan
  - Hourly (tới ~24 giờ, tự lọc theo thời gian hiện tại)
  - Forecast (5 ngày)
  - Details (các chỉ số chuyên sâu)

Nếu không tìm thấy thành phố:
- UI hiển thị thông báo lỗi tại khu vực Search.

### 📚 Trang Learn
- Bấm vào từng card để mở modal với nội dung tương ứng (sunny/cloudy/rainy/…).

### 🎮 Quiz (trong Learn)
- Chọn đáp án cho từng câu
- Sau mỗi câu sẽ có:
  - ✅/❌ theo kết quả
  - giải thích (explain)
  - nút “Câu tiếp theo”
- Khi hết câu:
  - Hiển thị mức độ dựa theo điểm
  - Có nút “Chơi lại”

---

## Công nghệ & Thư viện / Nguồn dữ liệu
- **Frontend**: HTML, CSS, Vanilla JavaScript
- **Fonts**:
  - Google Fonts: **Baloo 2**, **Nunito**
- **Weather API**: **Open-Meteo**
  - Geocoding: `geocoding-api.open-meteo.com`
  - Forecast: `api.open-meteo.com`
- **Không dùng key**:
  - Trong mã hiện có biến `API_KEY_WEATHER` nhưng để trống và Open-Meteo được dùng theo cơ chế miễn phí.

---

## Cấu trúc thư mục
```text
.
├─ Web/
│  ├─ index.html
│  ├─ style.css
│  └─ script.js
└─ README.md
```

- `Web/index.html`: bố cục giao diện, các section (Home/Learn/Search), modal, footer
- `Web/style.css`: toàn bộ style + animation + responsive
- `Web/script.js`: gọi API, render UI, xử lý quiz & modal, particle

---

## Lưu ý / Giới hạn
- Website phụ thuộc vào **kết nối Internet**:
  - Nếu không fetch được, UI sẽ hiển thị trạng thái lỗi (đặc biệt ở Home/Search).
- API forecast có thể trả về nhiều ngày hơn UI hiển thị:
  - Mã render đang hiển thị tối đa **5 ngày** (dù request có `forecast_days: 6`).
- Tất cả xử lý chạy ở trình duyệt:
  - Không có backend.
  - Không lưu trữ dữ liệu người dùng.

---

## Bảo mật & Thông tin nhạy cảm 🔒
- Dự án **không chứa API key thật** để tránh rò rỉ.
- Khuyến nghị nếu bạn sau này muốn thay đổi:
  - Không commit key vào repo
  - Nếu có cấu hình riêng, hãy dùng biến môi trường / file cấu hình bị ignore

---

## Gợi ý cải tiến (nâng cấp dự án)
- Thêm lựa chọn **đơn vị nhiệt độ (°C/°F)** và **gió (km/h/mph)**
- Cache kết quả theo thành phố để giảm số lần gọi API
- Thêm trang “About” hoặc hiển thị nguồn dữ liệu rõ hơn trong UI
- Bổ sung trạng thái skeleton/loading chi tiết hơn cho Search

---

## License
Bạn có thể bổ sung giấy phép cho dự án tại đây (ví dụ: MIT/Apache-2.0) nếu dùng vào học tập hoặc phát hành công khai.

---

## Tác giả
Có thể bổ sung tên tác giả hoặc nhóm phát triển tại đây.
