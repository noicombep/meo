# MEOWLAND ♡ — UI/UX BLUEPRINT

**Phiên bản:** 1.0 · **Định dạng:** responsive web game 2D · **Đối tượng:** một người nhận quà · **Trải nghiệm dự kiến:** 5–8 phút · **Thời gian:** không giới hạn.

## 1. Nguyên tắc trải nghiệm

- **Câu chuyện:** Miu đánh rơi 5 mảnh trái tim, người chơi đi qua 5 địa điểm để mang chúng về chiếc rương.
- **Không có thất bại:** không tính điểm phạt, không đếm ngược, không cần phản xạ nhanh; mọi lựa chọn quiz đều được đón nhận vui vẻ.
- **Mở khóa tuần tự:** nhiệm vụ kế tiếp chỉ mở khi nhiệm vụ trước hoàn thành; rương mở khi đủ 5 trái tim.
- **Mỗi tương tác có phản hồi:** vật phẩm đổi trạng thái, hiển thị câu thoại của Miu, và có hiệu ứng khi nhận thưởng.
- **Bí mật được hé lộ dần:** quà cuối gồm ba lớp: thư tình → kỷ niệm → voucher hẹn hò.
- **Mobile-first:** chơi bằng chạm, hạn chế di chuyển phức tạp; nút chính cao tối thiểu 48 px, có nhãn và trạng thái rõ ràng.

## 2. Sơ đồ điều hướng (Information Architecture)

```text
Welcome / Màn chào
  └─ CTA Bắt đầu
      └─ World Map / Bản đồ 6 điểm
         ├─ Cat House / Cho mèo ăn cá ─────┐
         ├─ Heart Garden / Tìm trái tim ───┤
         ├─ Memory House / Ghép tranh ─────┤→ Reward / Nhận 1 trái tim → Bản đồ
         ├─ Cat Café / Quiz tình yêu ──────┤
         ├─ Moon Hill / Bắt sao ───────────┘
         └─ Secret Treasure / Rương bí mật (sau đủ 5 trái tim)
            ├─ Thư tình
            ├─ Kỷ niệm (ảnh/video thật trong bản chính thức)
            └─ Voucher / Lời hẹn

Thanh điều hướng cố định theo trang:
  Logo → Bản đồ · 0–5 trái tim · Nhật ký · Bật/tắt hiệu ứng âm thanh
```

## 3. Layout và design system

| Thuộc tính | Quy cách |
|---|---|
| Khung nội dung desktop | tối đa 1190 px, căn giữa |
| Mobile | ưu tiên màn 360–430 px; xếp một cột, nút rộng |
| Khoảng cách chính | 8 / 12 / 16 / 24 / 32 px |
| Nền trang | `#FFF9F3` kem sữa |
| Primary / CTA | `#E776A4` hồng |
| Secondary | `#FFE1EC` hồng phấn |
| Mint / thành công | `#CBEBD7` |
| Lavender / đêm | `#E8DDF8` |
| Màu chữ | `#5B4054` |
| Card | bo góc 24–35 px, viền hồng rất nhạt |
| Nút primary | bo 18 px, bóng đổ dạng 3D nhẹ, cao tối thiểu 51 px |
| Chuyển động | 150–300 ms ở tương tác; hiệu ứng nền nhẹ, hỗ trợ reduced motion |
| Phản hồi | thành công: tim + lời nhắn; đang khóa: icon 🔒; đã hoàn thành: ✓ |

**Bố cục trên desktop:** bản đồ khoảng 70% bề ngang bên trái, bảng tiến độ và quest log ở bên phải. **Bố cục trên mobile:** header → bản đồ → bảng tiến độ → quest log. Trong màn nhiệm vụ, khung cảnh nằm trên, nội dung/hướng dẫn nằm dưới.

## 4. Đặc tả từng màn hình

### 01 — Welcome

- **Mục tiêu:** cá nhân hóa, giới thiệu Miu, tạo hứng thú.
- **UI:** logo Meowland; tên người nhận nổi bật; lời mở đầu; chú mèo chibi, ngôi nhà nhỏ, mây và mặt trời; CTA **Bắt đầu hành trình**.
- **Tương tác:** nhấn CTA → World Map. Có nút xem bản đồ để xem trước không làm tiến độ thay đổi.
- **Lời thoại gợi ý:** “Meow~ Em đến rồi! Đi chơi cùng Miu nha!”

### 02 — World Map

- **Mục tiêu:** bản đồ hub, định hướng, nhìn thấy tiến độ.
- **UI:** một bản đồ kéo dọc nhẹ màu cỏ + trời; đường mòn uốn từ nhà Miu tới rương; 6 điểm: Nhà Miu → Vườn trái tim → Nhà kỷ niệm → Quán mèo → Đồi sao → Rương bí mật.
- **Điểm map:** có emoji/hình minh họa, tên địa điểm và một trong ba trạng thái: `locked`, `available`, `completed`.
- **Bảng bên:** thanh tiến độ 0/5; nút **Tiếp tục** tự tới màn đang mở; danh sách 5 nhiệm vụ; bong bóng thoại Miu.
- **Luật:** không cho vào điểm chưa mở; không gắn điểm số hay giới hạn thời gian.
- **Hoàn thành game:** nút đổi thành **Mở rương tình yêu**.

### 03 — Nhà Miu: Cho ăn

- **Mục tiêu:** tương tác đầu tiên phải rất dễ, tạo cảm giác chăm sóc mèo.
- **UI:** phòng bếp pastel, mèo ở giữa, chiếc bát và ba nút hình cá.
- **Tương tác:** chạm từng con cá hoặc kéo con cá vào bát. Mỗi lần thành công hiện +1, bát cập nhật 1/3 → 3/3.
- **Hoàn thành:** nút **Nhận mảnh trái tim** xuất hiện; hoàn thành xong tới màn Reward.
- **Cảm xúc:** “Yêu em từ những điều nhỏ bé nhất.”

### 04 — Vườn trái tim: Tìm đồ vật

- **Mục tiêu:** tăng khám phá, hé lộ lời nhắn ngọt ngào.
- **UI:** căn phòng/vườn có chậu cây, gấu bông và chiếc giường; 3 ô tiến độ.
- **Tương tác:** chạm từng đồ vật → xuất hiện trái tim, gợi một dòng thương yêu và đánh dấu đã tìm.
- **Hoàn thành:** khi tìm đủ 3 đồ vật, nhận trái tim thứ hai.
- **Phản hồi:** đồ vật đã tìm hiển thị trái tim và không bấm lặp.

### 05 — Nhà kỷ niệm: Ghép tranh

- **Mục tiêu:** biến một kỷ niệm thành mini game.
- **UI:** bức minh họa hai chú mèo được chia 2×2, xáo trộn 4 mảnh.
- **Tương tác:** chọn hai ô để hoán đổi vị trí; ô đang chọn hiện viền nổi bật.
- **Hoàn thành:** khi 4 ô đúng vị trí, hiện lời khen và nút nhận trái tim thứ ba.
- **Bản nâng cấp:** thay hình minh họa bằng ảnh thực của hai bạn, chọn ảnh dễ nhận diện.

### 06 — Quán mèo: Quiz tình yêu

- **Mục tiêu:** cá nhân hóa bằng những câu hỏi của riêng hai người.
- **UI:** quán cà phê mèo, bánh ngọt và ly trà; một câu hỏi + 3 đáp án mỗi lượt.
- **Tương tác:** bấm một đáp án → Miu phản hồi bằng một câu dễ thương → **Câu tiếp theo**.
- **Hoàn thành:** 3 câu trả lời → trái tim thứ tư.
- **Quan trọng:** không có đáp án sai; câu hỏi mang tính kỷ niệm và vui vẻ, tránh thử thách gây áp lực.

### 07 — Đồi sao: Thu thập sao

- **Mục tiêu:** tạo cảm xúc lắng lại trước khi mở quà.
- **UI:** bầu trời tím pastel, sao sáng, chú mèo ngồi dưới đồi.
- **Tương tác:** chạm 5 ngôi sao đặt rải rác trong cảnh → mỗi sao hiện một điều bạn thích ở cô ấy.
- **Hoàn thành:** đủ 5 sao → trái tim cuối, mở khóa rương.
- **Âm thanh:** có thể phát chuông nhẹ cho mỗi sao; luôn có nút tắt.

### 08 — Reward (màn trung gian dùng chung)

- **UI:** trái tim lớn, confetti, thông điệp riêng của địa điểm, nút tiếp tục.
- **Tương tác:** nút đưa về bản đồ; sau nhiệm vụ cuối đưa tới rương.
- **Yêu cầu:** không phát thưởng lặp khi người chơi vào lại một nhiệm vụ đã xong.

### 09 — Secret Treasure

- **Điều kiện:** `completed.length === 5`.
- **Lớp 0:** rương đóng và nút dùng chìa khóa.
- **Lớp 1:** phong thư chứa lời tâm sự dài; nút mở tiếp.
- **Lớp 2:** album 3 kỷ niệm; **bản demo hiện thẻ minh họa, chưa có ảnh thực**.
- **Lớp 3:** voucher hẹn hò dành riêng cho người yêu, có dòng “Không có hạn sử dụng”.
- **Kết:** một lời thoại Miu và nút xem lại bản đồ.

### 10 — Love Journal / Nhật ký

- **UI:** modal đọc lời nhắn của 5 khu vực.
- **Trạng thái:** khu vực chưa chơi hiện khóa; khu vực đã hoàn thành hiện câu chữ riêng.
- **Tương tác:** mở từ header, đóng bằng nút `×` hoặc nhấn ra ngoài.

## 5. Hệ thống trạng thái và chuyển màn

- `completed`: danh sách id 0–4 đã nhận tim.
- `feed`: số cá đã cho ăn (0–3).
- `found`: các đồ vật đã tìm (0–2).
- `puzzle`: vị trí hiện tại của bốn miếng ghép.
- `quiz`: câu hỏi hiện tại (0–3), `quizAnswer` là lựa chọn đang hiển thị phản hồi.
- `stars`: danh sách ngôi sao đã chạm (0–4).
- `giftStep`: lớp quà đang mở (0–3).
- `soundOn`: bật hoặc tắt hiệu ứng âm thanh.

Lưu trạng thái trên trình duyệt bằng `localStorage` trong bản mẫu. Khi triển khai website thật, có thể dùng một mã link dành riêng cho người nhận và dịch vụ lưu dữ liệu nếu muốn đồng bộ trên nhiều thiết bị.

## 6. Danh sách nội dung cần cá nhân hóa

1. Tên bạn gái và cách bạn tự xưng.
2. Tên/chân dung chú mèo đại diện cho hai bạn.
3. Một lời mở đầu ngắn (2–3 câu).
4. Ba câu quiz mang ý nghĩa riêng.
5. Năm lời nhắn khi chạm sao.
6. Một lá thư tình cuối game.
7. Ba bức ảnh thật kèm chú thích (và video nếu có).
8. Voucher hẹn hò/lời hứa cuối cùng.

Trong file HTML mẫu, các chuỗi nội dung được tập trung ở biến `CONFIG` gần đầu phần JavaScript.

## 7. Quy tắc UX để bản chính thức dễ thương mà không rối

- Hiển thị hướng dẫn một câu ngắn ngay trong khung quest; không mở tutorial dài.
- Nút chính mỗi màn chỉ có một hành động ưu tiên; khi chưa đủ điều kiện thì ẩn, không gây nhầm.
- Cho phép quay về bản đồ mà không mất tiến độ.
- Tránh âm thanh tự động phát khi người nhận vừa mở website.
- Giao diện hỗ trợ sử dụng bằng bàn phím cơ bản, có nhãn cho các nút tương tác và phản hồi trực quan.
- Ưu tiên vector/ảnh nén nhẹ, tránh video tự phát tải chậm trên mạng di động.
- Album riêng tư và thông tin cá nhân không nên công khai trên đường dẫn không được bảo vệ.

## 8. Kiểm thử trước khi gửi

- Có thể vào đủ 5 nhiệm vụ theo đúng thứ tự, không mở được rương trước thời điểm.
- Game xong nhiệm vụ vẫn có thể xem lại bản đồ và nhật ký.
- Không có màn nào đòi drag-and-drop bắt buộc trên điện thoại.
- Quiz không gây bế tắc dù chọn bất kỳ phương án nào.
- Sau khi đủ sao, nhấn nhận tim để mở rương.
- Mở được lần lượt thư, kỷ niệm và voucher.
- Giao diện không cuộn ngang ở màn 390 px.
- Mọi nội dung placeholder đã được thay bằng ảnh, tên và kỷ niệm thật trước khi chia sẻ.
