<p align="center">
  <img src="logo.png" alt="SteamAccessFix Logo" width="600">
</p>

<h1 align="center">SteamAccessFix (SAF)</h1>

<p align="center">Công cụ mã nguồn mở dạng tập tin đơn (.cmd) giúp tự động khắc phục sự cố kết nối, mở khóa Steam (Store, Community, CDN), sửa lỗi màn hình đen / màn khói PUBG, hỗ trợ định tuyến Naraka & Delta Force, và tối ưu ping cho game thủ trên Windows 10 và 11.</p>

<p align="center">
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-blue?logo=windows" alt="Windows Support">
  <img src="https://img.shields.io/badge/Driver-Zero%20Dependency-brightgreen" alt="No Drivers">
  <img src="https://img.shields.io/badge/Anti--Cheat-100%25%20Safe-success" alt="Anti-Cheat Safe">
  <img src="https://img.shields.io/badge/Version-1.2.0-orange" alt="Version 1.2.0">
  <img src="https://img.shields.io/badge/License-MIT-lightgrey" alt="License">
</p>

<hr>

## Có gì mới ở v1.2.0

- **Bảng đo Ping & Lựa chọn Top 10 DNS Toàn cầu (Phím [D])**: Tự động đo ping đa luồng song song ICMP siêu tốc (~70ms) tới 10 máy chủ DNS uy tín nhất thế giới (Google, Cloudflare, Control D, Quad9, OpenDNS, AdGuard, NextDNS, AliDNS, DNS.SB, Comodo). Cho phép tự do lựa chọn theo ping thực tế trên màn hình, phím tắt `[F]` chọn nhanh DNS nhanh nhất, phím tắt `[0]` trả về DNS gốc của hệ thống (an toàn tuyệt đối cho máy dùng IP tĩnh/LAN).
- **Bộ tự động tìm MTU tối ưu (Auto MTU Tuning - Phím [T])**: Thuật toán nhị phân ICMP Don't Fragment (~40ms) tự động tìm kích thước MTU tối đa không bị phân mảnh gói tin trên đường truyền PPPoE (VNPT/FPT/Viettel), giúp đạn bay và nhận diện trúng đích (hitreg) ổn định hơn, triệt tiêu giật lag và ping spike trong PUBG, CS2.
- **Thu nhỏ xuống khay hệ thống (Minimize to System Tray - Phím [M])**: Ẩn cửa sổ console xuống khay đồng hồ Windows khi đang chơi game để tránh vướng víu hoặc vô tình bấm nhầm tắt. Click đúp vào biểu tượng khay để mở lại ngay lập tức.
- **Tự động làm sạch DNS Cache khi mở Game (Game Launch Hook)**: Module watcher chạy ngầm siêu nhẹ tự động phát hiện khi PUBG (`TslGame.exe`), Steam, CS2, Dota 2, Naraka vừa khởi động để kích hoạt API Win32 `DnsFlushResolverCache()`, ngăn chặn triệt để tình trạng dính IP cache bị chặn từ nhà mạng.
- **Khởi động siêu tốc & Tối ưu hóa toàn diện (<0.5s)**: Tăng tốc khởi động gấp 15 lần (từ ~8.5s xuống <0.5s) bằng cách caching card mạng, thay thế các tiến trình ngoài bằng Win32 API native (`DnsFlushResolverCache`, `InternetSetOption`), kiểm tra cập nhật GitHub bất đồng bộ (`FastUpdater.CheckAsync()`).
- **Lưới an toàn tuyệt đối cho mạng IP tĩnh (`Ensure-StaticDns` & `Set-DnsSafe`)**: Khắc phục triệt để lỗi mất mạng khi thoát tool trên các máy đặt LAN IP tĩnh (như phản hồi ở bản 1.1.4 cũ). Tự động điền Default Gateway + 8.8.8.8 nếu DNS bị trống, tuyệt đối không bao giờ để trắng DNS.
- **Giao diện người dùng (UI/UX) làm mới**: Bảng trạng thái trực quan, căn chỉnh ngay ngắn, đồng bộ định dạng `[Dang dung]`, lược bỏ các thông báo rườm rà.

---

## Tính năng cốt lõi

- **Mở khóa toàn diện Steam**: Khắc phục lỗi không tải được Steam Store, Community, hồ sơ người chơi, hình ảnh, CDN tải game và Steam Web API.
- **Hỗ trợ tối ưu CS2 & Dota 2**: Đảm bảo tải mượt mà CS2 / Dota 2 blog, cập nhật, cộng đồng, Steam API Game Coordinator (GC); lưu lượng trận đấu SDR UDP đi trực tiếp 100%.
- **Sửa triệt để lỗi PUBG (Direct Sniper Port 443 + Hosts Bypass)**: Giải quyết dứt điểm lỗi màn hình khói, **"Connection Lost"** và **"Servers are too busy, please try again later"** sau trận đấu. Sử dụng cơ chế bắt gói TLS trực tiếp trên cổng 443 kết hợp phân mảnh SNI, bảo vệ cả các kết nối socket C++ thuần và libcurl của game mà không phụ thuộc vào cài đặt proxy Windows.
- **Hỗ trợ định tuyến Naraka: Bladepoint & Delta Force**: Đảm bảo kết nối thông suốt đến các dịch vụ máy chủ và API sự kiện của game.
- **Tối ưu độ trễ và Ping Windows**: Tự động tinh chỉnh network stack Windows (`NetworkThrottlingIndex`, `SystemResponsiveness`, TCP AutoTuning) nhằm loại bỏ độ trễ và nghẽn băng thông khi chơi game.
- **Tự động dọn dẹp khi bấm [X] (SetConsoleCtrlHandler)**: Tích hợp hook native Win32 API. Khi người dùng tắt ngang cửa sổ bằng nút **[X]**, tool sẽ tự động dọn sạch Proxy, WinHTTP và Hosts trong 30ms trước khi thoát, ngăn chặn hoàn toàn việc mất mạng.
- **Tự chữa lành & Giải phóng mạng từ bản cũ (Self-Healing)**: Tự động phát hiện và thanh lọc các cấu hình proxy bị kẹt từ phiên bản cũ (v1.1.3 trở về trước) ngay lập tức khi khởi chạy.
- **100% Anti-Cheat Safe**: Hoạt động hoàn toàn ở chế độ người dùng (User-Mode), không cài driver kernel (`WinDivert`, GoodbyeDPI), an toàn tuyệt đối với BattlEye, Easy Anti-Cheat, Vanguard, VAC, ACE.

---

## Cách sử dụng

### Cách 1 - Chạy nhanh qua PowerShell (Khuyên dùng)

1. Mở **Start Menu**, tìm `PowerShell` (hoặc `Terminal`) và mở lên.
2. Dán đoạn mã bên dưới và nhấn **Enter**:

   ```powershell
   irm https://raw.githubusercontent.com/vuviett47/SteamAccessFix/main/SteamAccessFix.cmd | iex
   ```

   *Nếu lệnh trên bị chặn do DNS của nhà mạng, hãy dùng lệnh sau (tự động dùng DoH Cloudflare để tải):*
   ```powershell
   iex (curl.exe -s --doh-url https://1.1.1.1/dns-query https://raw.githubusercontent.com/vuviett47/SteamAccessFix/main/SteamAccessFix.cmd | Out-String)
   ```

---

### Cách 2 - Tải file trực tiếp (Truyền thống)

1. Tải về file kịch bản:
   * [**SteamAccessFix.cmd**](https://raw.githubusercontent.com/vuviett47/SteamAccessFix/main/SteamAccessFix.cmd) *(Nhấp chuột phải chọn Lưu liên kết dưới dạng... / Save link as...)*
2. Nhấp đúp chuột hoặc nhấp chuột phải chọn **Run as administrator** vào file `SteamAccessFix.cmd`.
3. Công cụ sẽ tự động phát hiện tình trạng mạng, áp dụng các tinh chỉnh và kích hoạt chế độ tối ưu nhất.

---

## Các cấp độ hoạt động (Progressive Detection)

Công cụ tuân theo nguyên tắc **thử từ nhẹ đến nâng cao** và **dừng ngay khi kết nối thành công**:

| Cấp độ | Phương pháp | Cơ chế kỹ thuật |
| :--- | :--- | :--- |
| **Level 0** | **Kiểm tra ban đầu** | Kiểm tra kết nối tới máy chủ Steam và PUBG. Nếu mạng đã hoạt động bình thường, công cụ chỉ áp dụng tinh chỉnh network giảm ping và không can thiệp sâu. |
| **Level 1** | **DNS Google (hoặc Top 10 DNS)** | Gán DNS công cộng chất lượng cao (Google, Cloudflare, Quad9...), xóa cache DNS để chặn triệt để tình trạng DNS poisoning từ modem/nhà mạng. |
| **Level 2** | **SplitProxy (SNI Fragmentation)** | Khởi chạy proxy nội bộ (C# nhúng sẵn). Phân mảnh gói tin TLS `ClientHello` (chia tách SNI) để vô hiệu hóa tường lửa DPI của nhà mạng FPT/VNPT. |
| **Level 3** | **DoH Fallback** | Truy vấn IP máy chủ gốc trực tiếp từ Cloudflare/Google qua DNS-over-HTTPS, hỗ trợ gán tạm thời vào file hosts nếu cần. |

---

## Điểm vượt trội về an toàn và hiệu năng

- **Zero-Driver (Không Driver)**: Hoàn toàn không cài đặt driver can thiệp sâu vào kernel hệ thống. Không bao giờ kích hoạt cờ cảnh báo của bất kỳ phần mềm chống gian lận nào.
- **Chỉ Proxy Web Game, Mọi Trang Khác & Match UDP Đi Thẳng**: Tệp cấu hình Proxy PAC chỉ định tuyến danh sách tên miền sảnh chờ và web Steam/PUBG/Naraka. Facebook, YouTube, Google, lướt web thông thường và toàn bộ lưu lượng trận đấu (UDP game match traffic) kết nối trực tiếp 100%, đảm bảo 0 ms độ trễ phát sinh.
- **Tự động khôi phục hoàn toàn khi bấm [X]**: Kể cả khi người dùng tắt đột ngột bằng nút [X] hoặc tắt máy, hook Win32 API bảo vệ sẽ dọn dẹp sạch sẽ toàn bộ cấu hình trước khi thoát.
- **Tự phục hồi sau sự cố**: Tự động phát hiện và dọn dẹp cấu hình dư thừa ở mỗi lần khởi động.

---

> [!TIP]
> - **Hãy giữ cửa sổ console mở** trong suốt quá trình chơi game hoặc duyệt Steam nếu công cụ đang chạy ở chế độ `Level 2 (SplitProxy)` (hoặc bấm `[M]` để thu nhỏ xuống khay đồng hồ).
> - **Phím tắt điều khiển linh hoạt:**
>   - Gõ `1` + Enter: **Chạy Cấp độ 1** (DNS + Tối ưu Ping, tắt Proxy).
>   - Gõ `2` + Enter: **Chạy Cấp độ 2** (SplitProxy SNI Fragmentation vượt chặn mạnh).
>   - Gõ `D` + Enter: **Bảng đo Ping & Chọn Top 10 DNS** (hoặc `0` để trả về DNS gốc cho IP tĩnh).
>   - Gõ `T` + Enter: **Tự động tìm & Tối ưu MTU cho game** (chống phân mảnh gói tin PPPoE).
>   - Gõ `M` + Enter: **Thu nhỏ xuống khay hệ thống (System Tray)** để không vướng màn hình khi chơi game.
>   - Gõ `A` + Enter: **Bật / Tắt tự khởi động NGẦM** cùng Windows (Task Scheduler).
>   - Gõ `K` + Enter: **Giữ lại (Keep)** thiết lập DNS và tinh chỉnh network trên máy rồi thoát.
>   - Gõ `R` + Enter: **Khôi phục mạng sạch 100% & Gỡ bỏ mọi thiết lập** rồi thoát ngay.
>   - Nhấn `Enter` hoặc `Q`: **Khôi phục toàn bộ cài đặt mạng ban đầu** và thoát an toàn.

---

<p align="center">
  <b>Phiên bản hiện tại:</b> 1.2.0 &bull; <b>Tác giả:</b> <a href="https://github.com/vuviett47">vuviett47</a>
</p>
