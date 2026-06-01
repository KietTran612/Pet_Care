# Project: Ứng dụng Nuôi Thú Ảo

## 1. Tổng quan dự án

Ứng dụng Nuôi Thú Ảo là một game/app mô phỏng trải nghiệm máy nuôi thú ảo cổ điển. Người chơi sẽ nhận một thú cưng ảo, chăm sóc nó hằng ngày thông qua các hành động như cho ăn, chơi, tắm rửa, dọn vệ sinh, chữa bệnh và cho ngủ.

Điểm cốt lõi của game là thú cưng vẫn thay đổi theo thời gian thật, kể cả khi người chơi không mở app. Nếu được chăm sóc tốt, thú sẽ khỏe mạnh, vui vẻ và phát triển thành các dạng tiến hóa tốt hơn. Nếu bị bỏ bê, thú có thể đói, buồn, bệnh, bẩn hoặc rời đi.

## 2. Mục tiêu chính

- Tạo trải nghiệm nuôi thú ảo đơn giản, dễ hiểu, dễ chơi.
- Người chơi có cảm giác thú cưng đang “sống” theo thời gian thật.
- Có hệ thống chỉ số rõ ràng để người chơi chăm sóc.
- Có vòng lặp gameplay ngắn nhưng lặp lại hằng ngày.
- Có khả năng mở rộng thêm mini game, shop, trang trí, nhiều pet và hệ thống tiến hóa.

## 3. Nền tảng dự kiến

Phiên bản đầu tiên có thể phát triển bằng Unity 2D.

Nền tảng ưu tiên:

- Android
- iOS
- PC test build trong giai đoạn phát triển

## 4. Phong cách game

- Thể loại: Virtual Pet / Cozy Casual / Simulation
- Góc nhìn: 2D
- Phong cách hình ảnh: dễ thương, đơn giản, rõ ràng
- Nhịp chơi: nhẹ nhàng, chăm sóc hằng ngày
- Cảm giác chính: thân thiện, thư giãn, có sự gắn bó với pet

## 5. Vòng lặp gameplay chính

```text
Nhận trứng / nhận pet
        ↓
Đặt tên pet
        ↓
Theo dõi chỉ số pet
        ↓
Cho ăn / chơi / tắm / dọn vệ sinh / chữa bệnh / cho ngủ
        ↓
Pet thay đổi trạng thái
        ↓
Pet lớn lên hoặc tiến hóa
        ↓
Mở khóa nội dung mới
        ↓
Tiếp tục chăm sóc hằng ngày
```

## 6. Phạm vi phiên bản MVP

Phiên bản MVP là phiên bản nhỏ nhất nhưng vẫn có cảm giác giống máy nuôi thú ảo cổ điển.

### 6.1. Chức năng bắt buộc trong MVP

- Tạo pet mới
- Đặt tên pet
- Hiển thị pet trên màn hình chính
- Hiển thị các chỉ số cơ bản
- Cho ăn
- Chơi với pet
- Tắm hoặc làm sạch pet
- Dọn vệ sinh
- Chữa bệnh
- Cho ngủ / đánh thức
- Pet thay đổi trạng thái cảm xúc
- Chỉ số giảm theo thời gian thật
- Lưu dữ liệu khi thoát app
- Tính thời gian offline khi mở lại app
- Pet lớn lên theo tuổi
- Pet có thể bị bệnh nếu bị bỏ bê

### 6.2. Chức năng chưa bắt buộc trong MVP

Các chức năng này có thể làm sau:

- Shop
- Coin
- Mini game phức tạp
- Trang trí phòng
- Nhiều loại pet
- Kết bạn online
- Kết hôn / sinh thế hệ mới
- Sự kiện theo mùa
- Cloud save
- Đăng nhập tài khoản

## 7. Màn hình chính

Màn hình chính là nơi người chơi tương tác nhiều nhất với pet.

### 7.1. Thành phần giao diện

- Khu vực hiển thị pet
- Tên pet
- Tuổi pet
- Trạng thái hiện tại của pet
- Thanh chỉ số đói/no
- Thanh chỉ số vui vẻ
- Thanh chỉ số sạch sẽ
- Thanh chỉ số năng lượng
- Thanh chỉ số sức khỏe
- Các nút hành động:
  - Cho ăn
  - Chơi
  - Tắm
  - Dọn vệ sinh
  - Chữa bệnh
  - Ngủ
  - Xem thông tin

### 7.2. Trạng thái hiển thị của pet

Pet cần có các biểu cảm hoặc animation cơ bản:

- Bình thường
- Vui
- Đói
- Buồn
- Bẩn
- Bệnh
- Mệt
- Ngủ
- Tức giận
- Đang ăn
- Đang chơi
- Đang được tắm

## 8. Hệ thống chỉ số pet

Mỗi pet có nhiều chỉ số để xác định tình trạng hiện tại.

### 8.1. Hunger / Độ no

Tên gợi ý trong code: `Hunger` hoặc `Fullness`.

Ý nghĩa:

- Đại diện cho mức độ no của pet.
- Chỉ số càng thấp thì pet càng đói.
- Giảm dần theo thời gian.
- Tăng khi người chơi cho pet ăn.

Giá trị:

```text
0   = rất đói
100 = rất no
```

Ảnh hưởng:

- Nếu quá thấp, pet chuyển trạng thái đói.
- Nếu duy trì thấp quá lâu, sức khỏe giảm.
- Nếu sức khỏe giảm nhiều, pet có thể bị bệnh.

### 8.2. Happiness / Độ vui vẻ

Ý nghĩa:

- Đại diện cho cảm xúc của pet.
- Tăng khi chơi, ăn snack hoặc được chăm sóc.
- Giảm dần nếu bị bỏ bê.

Giá trị:

```text
0   = rất buồn
100 = rất vui
```

Ảnh hưởng:

- Nếu thấp, pet buồn và ít phản ứng tích cực.
- Nếu thấp lâu, có thể ảnh hưởng đến sức khỏe hoặc tiến hóa.

### 8.3. Cleanliness / Độ sạch sẽ

Ý nghĩa:

- Đại diện cho mức độ sạch của pet và môi trường sống.
- Giảm khi pet đi vệ sinh.
- Tăng khi tắm hoặc dọn vệ sinh.

Giá trị:

```text
0   = rất bẩn
100 = rất sạch
```

Ảnh hưởng:

- Nếu thấp, pet có trạng thái bẩn.
- Nếu thấp lâu, pet dễ bị bệnh.
- Có thể ảnh hưởng đến hình dạng tiến hóa.

### 8.4. Energy / Năng lượng

Ý nghĩa:

- Đại diện cho sức lực của pet.
- Giảm khi chơi hoặc hoạt động.
- Tăng khi ngủ.

Giá trị:

```text
0   = kiệt sức
100 = đầy năng lượng
```

Ảnh hưởng:

- Nếu quá thấp, pet không thể chơi.
- Nếu quá thấp, pet cần ngủ.
- Nếu ngủ đủ, pet hồi phục năng lượng.

### 8.5. Health / Sức khỏe

Ý nghĩa:

- Đại diện cho tình trạng sức khỏe tổng thể.
- Giảm khi pet quá đói, quá bẩn, quá buồn hoặc bị bệnh.
- Tăng khi được chăm sóc đúng cách hoặc dùng thuốc.

Giá trị:

```text
0   = nguy hiểm
100 = khỏe mạnh
```

Ảnh hưởng:

- Nếu thấp, pet bị bệnh.
- Nếu về 0 trong thời gian dài, pet có thể rời đi hoặc kết thúc vòng đời.

### 8.6. Age / Tuổi

Ý nghĩa:

- Đại diện cho thời gian pet đã sống.
- Tăng theo thời gian thật hoặc theo số ngày chăm sóc.
- Dùng để quyết định giai đoạn phát triển.

Ví dụ giai đoạn:

```text
0 ngày      = trứng
1 ngày      = baby
2 - 3 ngày  = child
4 - 6 ngày  = teen
7+ ngày     = adult
```

### 8.7. Weight / Cân nặng

Ý nghĩa:

- Tăng khi ăn.
- Giảm khi chơi.
- Nếu quá cao, pet có thể chậm chạp hoặc dễ bệnh.

Chỉ số này có thể đưa vào MVP hoặc để phiên bản sau.

### 8.8. Discipline / Kỷ luật

Ý nghĩa:

- Đại diện cho mức độ ngoan của pet.
- Tăng khi người chơi phản ứng đúng với hành vi của pet.
- Có thể ảnh hưởng đến tiến hóa.

Chỉ số này nên để phiên bản sau nếu MVP cần đơn giản.

## 9. Hệ thống hành động chăm sóc

## 9.1. Cho ăn

Mục đích:

- Tăng độ no.
- Có thể tăng nhẹ vui vẻ.
- Có thể tăng cân nặng nếu có hệ thống cân nặng.

Luồng xử lý:

```text
Người chơi bấm nút Cho ăn
        ↓
Hiển thị danh sách thức ăn
        ↓
Người chơi chọn món
        ↓
Pet ăn
        ↓
Tăng độ no
        ↓
Cập nhật animation ăn
        ↓
Lưu dữ liệu
```

Loại thức ăn cơ bản:

- Bữa chính
- Snack
- Đồ ăn đặc biệt

Quy tắc đề xuất:

```text
Bữa chính:
- Tăng no nhiều
- Tăng vui ít
- Ít tác dụng phụ

Snack:
- Tăng vui nhiều
- Tăng no ít
- Nếu ăn quá nhiều có thể giảm sức khỏe

Đồ ăn đặc biệt:
- Có thể ảnh hưởng tiến hóa
- Có thể mở khóa bằng shop hoặc nhiệm vụ
```

## 9.2. Chơi với pet

Mục đích:

- Tăng vui vẻ.
- Giảm năng lượng.
- Có thể giảm cân nặng.
- Có thể kiếm coin nếu có mini game.

Luồng xử lý đơn giản trong MVP:

```text
Người chơi bấm nút Chơi
        ↓
Pet thực hiện animation vui
        ↓
Tăng Happiness
        ↓
Giảm Energy
        ↓
Giảm Hunger nhẹ
        ↓
Lưu dữ liệu
```

Điều kiện:

- Nếu Energy quá thấp, pet từ chối chơi.
- Nếu Health quá thấp, pet không thể chơi.
- Nếu pet đang ngủ, không thể chơi.

## 9.3. Tắm / làm sạch pet

Mục đích:

- Tăng Cleanliness.
- Loại bỏ trạng thái bẩn.
- Giảm nguy cơ bệnh.

Luồng xử lý:

```text
Người chơi bấm Tắm
        ↓
Pet chuyển sang animation tắm
        ↓
Cleanliness tăng
        ↓
Nếu đang bẩn thì xóa trạng thái bẩn
        ↓
Lưu dữ liệu
```

Quy tắc đề xuất:

- Tắm tăng Cleanliness từ 20 đến 40 điểm.
- Nếu Cleanliness đã đầy thì hiển thị thông báo: “Pet đã sạch rồi.”

## 9.4. Dọn vệ sinh

Mục đích:

- Dọn phân hoặc rác trong phòng.
- Giữ môi trường sạch.
- Tránh pet bị bệnh.

Luồng xử lý:

```text
Theo thời gian, pet có thể đi vệ sinh
        ↓
Icon phân/rác xuất hiện trong phòng
        ↓
Người chơi bấm Dọn vệ sinh
        ↓
Xóa icon phân/rác
        ↓
Tăng Cleanliness hoặc giảm mức bẩn
        ↓
Lưu dữ liệu
```

Quy tắc đề xuất:

- Nếu có phân/rác mà không dọn, Cleanliness giảm dần.
- Nếu để quá lâu, Health giảm.
- Nếu dọn nhanh, có thể tăng nhẹ Happiness.

## 9.5. Chữa bệnh

Mục đích:

- Khôi phục trạng thái pet khi bị bệnh.
- Tăng Health.
- Xóa trạng thái Sick nếu đủ điều kiện.

Nguyên nhân pet bị bệnh:

- Hunger quá thấp trong thời gian dài.
- Cleanliness quá thấp trong thời gian dài.
- Ăn quá nhiều snack.
- Không ngủ đủ.
- Health giảm dưới ngưỡng nguy hiểm.

Luồng xử lý:

```text
Pet bị bệnh
        ↓
Hiển thị icon bệnh
        ↓
Người chơi bấm Chữa bệnh
        ↓
Dùng thuốc
        ↓
Health tăng
        ↓
Nếu Health vượt ngưỡng, xóa trạng thái bệnh
        ↓
Lưu dữ liệu
```

Quy tắc đề xuất:

- Nếu Health < 30 thì pet bị bệnh.
- Mỗi lần chữa bệnh tăng Health từ 25 đến 40 điểm.
- Có thể cần chữa nhiều lần nếu bệnh nặng.

## 9.6. Ngủ / đánh thức

Mục đích:

- Cho pet hồi phục năng lượng.
- Tạo nhịp sinh hoạt giống sinh vật thật.

Luồng xử lý:

```text
Người chơi bấm nút Ngủ
        ↓
Pet chuyển sang trạng thái Sleeping
        ↓
Trong khi ngủ, Energy tăng theo thời gian
        ↓
Một số hành động bị khóa
        ↓
Người chơi có thể đánh thức hoặc pet tự thức dậy
```

Quy tắc đề xuất:

- Khi ngủ, Hunger vẫn có thể giảm nhưng chậm hơn.
- Khi ngủ, Happiness giảm chậm hơn.
- Energy tăng dần.
- Không thể chơi hoặc tắm khi pet đang ngủ.
- Có thể cho phép đánh thức nhưng làm giảm Happiness nhẹ.

## 10. Hệ thống trạng thái pet

Pet cần có trạng thái tổng hợp dựa trên các chỉ số.

### 10.1. Danh sách trạng thái

- Normal
- Happy
- Hungry
- Sad
- Dirty
- Sick
- Tired
- Sleeping
- Angry
- Dead hoặc Left

### 10.2. Quy tắc xác định trạng thái ưu tiên

Thứ tự ưu tiên đề xuất:

```text
1. Nếu pet đã rời đi hoặc chết → Left/Dead
2. Nếu đang ngủ → Sleeping
3. Nếu Health <= 20 → Sick
4. Nếu Energy <= 15 → Tired
5. Nếu Hunger <= 20 → Hungry
6. Nếu Cleanliness <= 20 → Dirty
7. Nếu Happiness <= 20 → Sad
8. Nếu Happiness >= 80 và Health >= 70 → Happy
9. Còn lại → Normal
```

## 11. Hệ thống thời gian thực

Đây là phần quan trọng nhất để app có cảm giác giống máy nuôi thú ảo.

### 11.1. Khi app đang mở

Theo chu kỳ thời gian, các chỉ số sẽ thay đổi.

Ví dụ:

```text
Mỗi 1 phút:
- Hunger giảm 1
- Happiness giảm 0 hoặc 1
- Energy giảm nhẹ nếu không ngủ
- Nếu đang ngủ, Energy tăng
```

```text
Mỗi 10 - 30 phút:
- Có khả năng pet đi vệ sinh
- Có khả năng pet cần tương tác
```

### 11.2. Khi app bị đóng

Khi người chơi mở lại app, game cần tính thời gian offline.

Luồng xử lý:

```text
Khi thoát app:
- Lưu LastSaveTime

Khi mở app:
- Lấy thời gian hiện tại
- So sánh với LastSaveTime
- Tính số phút/giờ đã trôi qua
- Áp dụng thay đổi chỉ số tương ứng
- Cập nhật trạng thái pet
- Lưu lại dữ liệu mới
```

Ví dụ:

```text
Offline 2 giờ:
- Hunger giảm theo 2 giờ
- Happiness giảm theo 2 giờ
- Cleanliness có thể giảm
- Có thể xuất hiện phân/rác
- Nếu chỉ số quá thấp, Health giảm
```

### 11.3. Giới hạn thay đổi offline

Để tránh người chơi mở app sau nhiều ngày và pet chết ngay lập tức, có thể giới hạn mức phạt.

Quy tắc đề xuất:

```text
Nếu offline dưới 8 giờ:
- Áp dụng đầy đủ thay đổi

Nếu offline 8 - 24 giờ:
- Áp dụng thay đổi mạnh nhưng không làm Health về 0 ngay

Nếu offline hơn 24 giờ:
- Pet rất yếu, đói, bẩn, buồn
- Health giảm mạnh
- Pet có thể bệnh
- Chưa nên chết ngay ở MVP, chỉ cảnh báo người chơi
```

## 12. Hệ thống tiến hóa

Pet phát triển qua nhiều giai đoạn dựa trên tuổi và chất lượng chăm sóc.

### 12.1. Giai đoạn phát triển

```text
Egg    → Baby → Child → Teen → Adult
Trứng  → Sơ sinh → Trẻ nhỏ → Thiếu niên → Trưởng thành
```

### 12.2. Điều kiện tiến hóa

Pet có thể tiến hóa khi đạt đủ tuổi.

Ví dụ:

```text
Egg → Baby:
- Sau vài phút hoặc sau khi người chơi bắt đầu game

Baby → Child:
- Sau 1 ngày

Child → Teen:
- Sau 3 ngày

Teen → Adult:
- Sau 7 ngày
```

### 12.3. Nhánh tiến hóa

Nhánh tiến hóa phụ thuộc vào cách chăm sóc.

Ví dụ:

```text
Chăm sóc tốt:
- Hunger thường trên 60
- Happiness thường trên 60
- Cleanliness thường trên 60
- Health thường trên 70
→ Tiến hóa thành dạng khỏe/vui/hiếm

Chăm sóc trung bình:
- Chỉ số dao động trung bình
→ Tiến hóa thành dạng bình thường

Chăm sóc kém:
- Thường xuyên đói, bẩn, buồn hoặc bệnh
→ Tiến hóa thành dạng yếu/buồn/lười
```

### 12.4. Điểm chăm sóc

Nên có biến ẩn để tính chất lượng chăm sóc.

Tên gợi ý:

```text
CareScore
CareMistakes
GoodCareCount
BadCareCount
```

Ví dụ:

```text
Nếu Hunger về 0 → CareMistakes +1
Nếu Cleanliness về 0 → CareMistakes +1
Nếu Health dưới 20 → CareMistakes +2
Nếu chăm sóc đầy đủ trong ngày → GoodCareCount +1
```

## 13. Hệ thống thông báo

Thông báo giúp người chơi quay lại chăm pet.

### 13.1. Loại thông báo

- Pet đói
- Pet buồn
- Pet bẩn
- Pet bị bệnh
- Pet buồn ngủ
- Pet đã thức dậy
- Pet nhớ bạn
- Có sự kiện hoặc phần thưởng mới

### 13.2. Quy tắc thông báo MVP

Trong MVP, chỉ cần các thông báo cơ bản:

```text
Nếu Hunger thấp:
"Pet của bạn đang đói!"

Nếu Happiness thấp:
"Pet của bạn đang buồn, hãy chơi với pet nhé!"

Nếu Cleanliness thấp:
"Pet của bạn cần được tắm hoặc dọn vệ sinh!"

Nếu Health thấp:
"Pet của bạn đang bị bệnh!"
```

### 13.3. Tần suất thông báo

Không nên gửi quá nhiều.

Quy tắc đề xuất:

```text
- Không gửi quá 1 thông báo mỗi 30 - 60 phút.
- Không gửi thông báo ban đêm nếu người chơi bật chế độ im lặng.
- Chỉ gửi khi chỉ số thật sự thấp.
```

## 14. Hệ thống lưu dữ liệu

Dữ liệu pet cần được lưu để không mất khi tắt app.

### 14.1. Dữ liệu cần lưu

- Tên pet
- Loại pet
- Giai đoạn phát triển
- Các chỉ số hiện tại
- Tuổi
- Cân nặng nếu có
- Trạng thái ngủ
- Trạng thái bệnh
- Số phân/rác trong phòng
- Điểm chăm sóc
- Lỗi chăm sóc
- Coin
- Item đang sở hữu
- Thời gian lưu cuối cùng
- Lịch sử ngày chăm sóc

### 14.2. Cách lưu trong MVP

Có thể dùng:

- JSON file
- PlayerPrefs cho bản test rất đơn giản

Khuyến nghị:

```text
Dùng JSON file để dễ mở rộng.
PlayerPrefs chỉ nên dùng cho setting nhỏ.
```

### 14.3. Cấu trúc dữ liệu pet gợi ý

```csharp
public class PetData
{
    public string PetId;
    public string PetName;
    public string SpeciesId;
    public string GrowthStage;

    public int Hunger;
    public int Happiness;
    public int Cleanliness;
    public int Energy;
    public int Health;
    public int AgeDays;
    public int Weight;

    public bool IsSleeping;
    public bool IsSick;
    public int PoopCount;

    public int CareScore;
    public int CareMistakes;

    public int Coins;

    public string CreatedAt;
    public string LastSaveTime;
}
```

## 15. Hệ thống mini game

Mini game là chức năng giúp tăng vui vẻ và tạo hoạt động cho người chơi.

### 15.1. Mini game MVP

MVP chỉ cần 1 mini game đơn giản.

Ví dụ:

- Đoán trái/phải
- Bắt đồ ăn rơi
- Né chướng ngại vật
- Bấm đúng thời điểm
- Ghi nhớ hình ảnh

### 15.2. Phần thưởng mini game

Khi chơi thắng:

```text
- Happiness +15
- Coin +10
- Energy -10
- Hunger -5
```

Khi chơi thua:

```text
- Happiness +5
- Energy -5
- Hunger -3
```

### 15.3. Điều kiện chơi mini game

- Pet không được đang ngủ.
- Energy phải đủ.
- Health không quá thấp.
- Nếu pet bệnh thì không thể chơi.

## 16. Hệ thống coin và shop

Nên để sau MVP, nhưng cần thiết kế sẵn để mở rộng.

### 16.1. Coin

Coin dùng để mua:

- Đồ ăn
- Snack
- Thuốc
- Đồ chơi
- Trang phục
- Đồ trang trí phòng

Nguồn nhận coin:

- Chơi mini game
- Nhiệm vụ hằng ngày
- Chăm sóc pet tốt
- Xem quảng cáo thưởng nếu app có ads
- Sự kiện

### 16.2. Shop

Shop có các nhóm item:

```text
Food
Snack
Medicine
Toy
Decoration
Accessory
Special
```

### 16.3. Item đồ ăn

Mỗi item đồ ăn có thể có chỉ số riêng:

```text
Rice Ball:
- Hunger +20
- Happiness +2
- Price: 10 coin

Cake:
- Hunger +5
- Happiness +20
- Health -2 nếu ăn quá nhiều
- Price: 20 coin

Herbal Soup:
- Hunger +10
- Health +10
- Price: 30 coin
```

## 17. Hệ thống item

Item giúp game có chiều sâu hơn.

### 17.1. Loại item

- Consumable: dùng một lần, ví dụ thức ăn, thuốc
- Toy: đồ chơi dùng nhiều lần
- Decoration: trang trí phòng
- Accessory: phụ kiện cho pet
- Special: item đặc biệt ảnh hưởng tiến hóa

### 17.2. Dữ liệu item gợi ý

```csharp
public class ItemData
{
    public string ItemId;
    public string ItemName;
    public string ItemType;
    public int Price;

    public int HungerEffect;
    public int HappinessEffect;
    public int CleanlinessEffect;
    public int EnergyEffect;
    public int HealthEffect;

    public bool IsConsumable;
}
```

## 18. Hệ thống nhiệm vụ hằng ngày

Nhiệm vụ giúp người chơi có mục tiêu mỗi ngày.

### 18.1. Nhiệm vụ gợi ý

- Cho pet ăn 3 lần
- Chơi với pet 1 lần
- Tắm cho pet 1 lần
- Dọn vệ sinh 1 lần
- Giữ Health trên 80
- Đăng nhập trong ngày
- Hoàn thành mini game

### 18.2. Phần thưởng

- Coin
- Item
- Điểm kinh nghiệm
- Điểm thân thiết
- Vé quay thưởng nếu có hệ thống gacha nhẹ

## 19. Hệ thống phòng của pet

Phòng là nơi pet sống và cũng là khu vực trang trí.

### 19.1. Chức năng phòng MVP

Trong MVP, phòng có thể rất đơn giản:

- Background cố định
- Pet đứng ở giữa
- Icon phân/rác xuất hiện khi cần dọn
- Một vài animation nhỏ

### 19.2. Chức năng phòng mở rộng

- Đổi nền phòng
- Đặt đồ nội thất
- Đổi sàn
- Đổi tường
- Đặt đồ chơi
- Pet tương tác với đồ vật

## 20. Hệ thống sưu tầm

Hệ thống sưu tầm giúp tăng giá trị chơi lâu dài.

### 20.1. Nội dung có thể sưu tầm

- Các loài pet
- Các dạng tiến hóa
- Đồ ăn
- Đồ chơi
- Trang phục
- Đồ trang trí
- Huy hiệu thành tựu
- Kỷ niệm các pet cũ

### 20.2. Pet Album

Pet Album lưu lại những pet người chơi từng nuôi.

Thông tin lưu:

- Tên pet
- Loài pet
- Dạng tiến hóa cuối
- Số ngày đã sống
- Ngày sinh
- Ngày rời đi nếu có
- Chất lượng chăm sóc

## 21. Hệ thống pet rời đi hoặc chết

Đây là chức năng nhạy cảm, nên thiết kế nhẹ nhàng.

### 21.1. Cách xử lý đề xuất

Thay vì dùng từ “chết”, có thể dùng:

- Pet rời đi
- Pet trở về hành tinh của nó
- Pet đi phiêu lưu
- Pet cần nghỉ ngơi dài hạn

### 21.2. Điều kiện pet rời đi

Ví dụ:

```text
Nếu Health = 0 trong thời gian dài
hoặc
Nếu người chơi bỏ bê nhiều ngày liên tục
→ Pet rời đi
```

### 21.3. Sau khi pet rời đi

- Lưu pet vào album
- Hiển thị lời tạm biệt
- Cho người chơi nhận trứng mới
- Giữ một phần coin/item nếu muốn nhẹ nhàng hơn

## 22. Hệ thống âm thanh

### 22.1. Âm thanh cần có

- Nhạc nền nhẹ nhàng
- Âm thanh bấm nút
- Âm thanh pet vui
- Âm thanh pet buồn
- Âm thanh ăn
- Âm thanh tắm
- Âm thanh nhận thưởng
- Âm thanh cảnh báo bệnh/đói

### 22.2. Quy tắc âm thanh

- Có nút bật/tắt nhạc
- Có nút bật/tắt hiệu ứng âm thanh
- Âm thanh không nên quá gắt vì game có tính thư giãn

## 23. Hệ thống setting

Setting cơ bản:

- Bật/tắt nhạc nền
- Bật/tắt hiệu ứng âm thanh
- Bật/tắt thông báo
- Chọn ngôn ngữ
- Xóa dữ liệu chơi
- Xem thông tin phiên bản

## 24. Cấu trúc scene trong Unity

Cấu trúc gợi ý:

```text
Scenes
├── BootScene
├── MainScene
├── MiniGameScene
├── ShopScene
└── CollectionScene
```

### 24.1. BootScene

Nhiệm vụ:

- Load dữ liệu người chơi
- Kiểm tra có pet hay chưa
- Chuyển sang MainScene hoặc màn hình tạo pet

### 24.2. MainScene

Nhiệm vụ:

- Hiển thị pet
- Hiển thị chỉ số
- Xử lý hành động chăm sóc
- Xử lý thời gian thật
- Lưu dữ liệu

### 24.3. MiniGameScene

Nhiệm vụ:

- Chạy mini game
- Tính điểm
- Trả phần thưởng
- Quay lại MainScene

### 24.4. ShopScene

Nhiệm vụ:

- Hiển thị item
- Mua item
- Dùng item

### 24.5. CollectionScene

Nhiệm vụ:

- Hiển thị album pet
- Hiển thị item đã sưu tầm
- Hiển thị thành tựu

## 25. Cấu trúc script gợi ý

```text
Scripts
├── Core
│   ├── GameManager.cs
│   ├── TimeManager.cs
│   ├── SaveManager.cs
│   └── EventManager.cs
│
├── Pet
│   ├── PetData.cs
│   ├── PetManager.cs
│   ├── PetStats.cs
│   ├── PetStateMachine.cs
│   ├── PetEvolutionManager.cs
│   └── PetAnimationController.cs
│
├── UI
│   ├── MainUIController.cs
│   ├── StatusBarUI.cs
│   ├── ActionButtonUI.cs
│   └── MessagePopupUI.cs
│
├── Items
│   ├── ItemData.cs
│   ├── InventoryManager.cs
│   └── ShopManager.cs
│
├── MiniGames
│   ├── MiniGameManager.cs
│   └── SimpleCatchGame.cs
│
└── Notifications
    └── NotificationManager.cs
```

## 26. Các class chính

### 26.1. GameManager

Vai trò:

- Quản lý trạng thái tổng thể của game.
- Khởi tạo dữ liệu.
- Kết nối các manager khác.
- Điều phối scene.

### 26.2. PetManager

Vai trò:

- Quản lý pet hiện tại.
- Xử lý hành động chăm sóc.
- Cập nhật chỉ số.
- Gọi lưu dữ liệu.

Hàm gợi ý:

```csharp
Feed()
Play()
Clean()
CleanPoop()
Heal()
Sleep()
WakeUp()
UpdatePetStats()
GetCurrentMood()
```

### 26.3. TimeManager

Vai trò:

- Tính thời gian trôi qua khi app đang mở.
- Tính thời gian offline.
- Gửi tick thời gian cho PetManager.

Hàm gợi ý:

```csharp
GetOfflineDuration()
ApplyOfflineProgress()
StartTimeTick()
StopTimeTick()
```

### 26.4. SaveManager

Vai trò:

- Lưu dữ liệu pet.
- Load dữ liệu pet.
- Kiểm tra dữ liệu có tồn tại không.
- Reset dữ liệu nếu cần.

Hàm gợi ý:

```csharp
SavePetData(PetData data)
LoadPetData()
HasSaveData()
DeleteSaveData()
```

### 26.5. PetStateMachine

Vai trò:

- Xác định trạng thái hiện tại của pet.
- Ưu tiên trạng thái nguy hiểm trước trạng thái thường.
- Gửi trạng thái cho animation và UI.

Hàm gợi ý:

```csharp
EvaluateState(PetData data)
SetState(PetState newState)
```

### 26.6. PetEvolutionManager

Vai trò:

- Kiểm tra pet đã đủ điều kiện tiến hóa chưa.
- Chọn nhánh tiến hóa dựa trên điểm chăm sóc.
- Thay đổi hình dạng pet.

Hàm gợi ý:

```csharp
CanEvolve(PetData data)
GetEvolutionResult(PetData data)
EvolvePet(PetData data)
```

## 27. Công thức chỉ số đề xuất

### 27.1. Giảm chỉ số theo thời gian

Mỗi 5 phút:

```text
Hunger -2
Happiness -1
Energy -1 nếu đang thức
Energy +3 nếu đang ngủ
```

Mỗi 15 phút:

```text
Cleanliness -1
Có xác suất pet đi vệ sinh
```

Nếu chỉ số thấp:

```text
Nếu Hunger < 20 → Health -1 mỗi chu kỳ
Nếu Cleanliness < 20 → Health -1 mỗi chu kỳ
Nếu Happiness < 20 → Health -1 sau một thời gian dài
```

### 27.2. Hành động chăm sóc

Cho ăn bữa chính:

```text
Hunger +25
Happiness +3
Weight +1
```

Cho ăn snack:

```text
Hunger +5
Happiness +15
Weight +2
Nếu ăn quá nhiều snack trong ngày → Health -5
```

Chơi:

```text
Happiness +20
Energy -15
Hunger -5
Weight -1
Coin +5 nếu thắng mini game
```

Tắm:

```text
Cleanliness +35
Happiness +3
```

Dọn vệ sinh:

```text
PoopCount -1
Cleanliness +10
Happiness +2
```

Chữa bệnh:

```text
Health +35
Nếu Health > 40 → IsSick = false
```

Ngủ:

```text
IsSleeping = true
Energy tăng theo thời gian
```

Đánh thức:

```text
IsSleeping = false
Nếu Energy < 50 → Happiness -5
```

## 28. Quy tắc giới hạn chỉ số

Tất cả các chỉ số chính nên được giới hạn trong khoảng 0 đến 100.

```csharp
value = Mathf.Clamp(value, 0, 100);
```

Các chỉ số cần clamp:

- Hunger
- Happiness
- Cleanliness
- Energy
- Health

## 29. UI/UX chi tiết

### 29.1. Nguyên tắc UI

- Nút to, dễ bấm trên mobile.
- Icon dễ hiểu.
- Không hiển thị quá nhiều thông tin cùng lúc.
- Chỉ số nên dùng thanh màu hoặc icon tim/ngôi sao.
- Pet luôn là trung tâm màn hình.

### 29.2. Thông báo trong game

Ví dụ thông báo:

```text
"Pet đang đói!"
"Pet vui hơn rồi!"
"Pet đã sạch sẽ!"
"Pet đang ngủ."
"Pet quá mệt để chơi."
"Pet đang bị bệnh, hãy dùng thuốc."
```

### 29.3. Feedback sau mỗi hành động

Mỗi hành động nên có:

- Animation ngắn
- Âm thanh ngắn
- Text phản hồi
- Cập nhật thanh chỉ số

## 30. Dữ liệu cấu hình

Nên tách dữ liệu cấu hình khỏi code để dễ chỉnh balance.

Có thể dùng:

- ScriptableObject trong Unity
- JSON config
- CSV đơn giản

Dữ liệu nên tách:

- Thức ăn
- Item
- Pet species
- Evolution rules
- Mini game reward
- Daily mission

## 31. Milestone phát triển

### Milestone 1: Prototype

Mục tiêu:

- Có một pet hiển thị trên màn hình.
- Có chỉ số cơ bản.
- Có nút cho ăn, chơi, tắm, ngủ.
- Chỉ số thay đổi được.

Checklist:

- [ ] MainScene
- [ ] PetData
- [ ] PetManager
- [ ] UI chỉ số
- [ ] Nút hành động cơ bản
- [ ] Animation trạng thái đơn giản

### Milestone 2: Save & Time System

Mục tiêu:

- Pet vẫn thay đổi khi app tắt.
- Dữ liệu không mất sau khi thoát.

Checklist:

- [ ] SaveManager
- [ ] Load dữ liệu khi mở app
- [ ] Lưu LastSaveTime
- [ ] Tính offline progress
- [ ] Clamp chỉ số
- [ ] Cập nhật trạng thái sau offline

### Milestone 3: Care System hoàn chỉnh

Mục tiêu:

- Có đầy đủ chăm sóc cơ bản giống máy nuôi thú ảo.

Checklist:

- [ ] Cho ăn
- [ ] Chơi
- [ ] Tắm
- [ ] Dọn vệ sinh
- [ ] Chữa bệnh
- [ ] Ngủ/thức
- [ ] Trạng thái đói/buồn/bệnh/bẩn/mệt

### Milestone 4: Growth & Evolution

Mục tiêu:

- Pet lớn lên theo thời gian.
- Cách chăm sóc ảnh hưởng tiến hóa.

Checklist:

- [ ] Age system
- [ ] Growth stage
- [ ] CareScore
- [ ] CareMistakes
- [ ] Evolution rules
- [ ] Đổi sprite/animation theo dạng tiến hóa

### Milestone 5: Mini Game & Reward

Mục tiêu:

- Người chơi có hoạt động để tăng vui vẻ và kiếm coin.

Checklist:

- [ ] 1 mini game đơn giản
- [ ] Kết quả thắng/thua
- [ ] Tăng Happiness
- [ ] Giảm Energy
- [ ] Thưởng coin
- [ ] Quay lại MainScene

### Milestone 6: Shop & Items

Mục tiêu:

- Người chơi dùng coin để mua vật phẩm.

Checklist:

- [ ] Coin system
- [ ] ItemData
- [ ] Inventory
- [ ] Shop UI
- [ ] Mua item
- [ ] Dùng item

### Milestone 7: Polish

Mục tiêu:

- Game có cảm giác hoàn chỉnh và dễ thương hơn.

Checklist:

- [ ] Âm thanh
- [ ] Hiệu ứng UI
- [ ] Animation mượt hơn
- [ ] Thông báo mobile
- [ ] Setting
- [ ] Fix bug
- [ ] Balance chỉ số

## 32. Backlog chức năng mở rộng

Các chức năng có thể làm sau MVP:

- Nhiều loài pet
- Nhiều phòng
- Trang trí nhà
- Trang phục pet
- Pet album
- Thành tựu
- Nhiệm vụ hằng ngày
- Sự kiện theo mùa
- Pet có tính cách riêng
- Pet học kỹ năng
- Kết bạn với pet người khác
- Gửi quà
- Cloud save
- Đăng nhập tài khoản
- Leaderboard mini game
- Battle mini game nhẹ
- Hệ thống thời tiết
- Chu kỳ ngày/đêm
- Cây trồng hoặc vườn nhỏ
- Pet đi dạo
- AR mode nếu muốn mở rộng lớn

## 33. Rủi ro thiết kế cần chú ý

### 33.1. Chỉ số giảm quá nhanh

Nếu chỉ số giảm quá nhanh, người chơi sẽ thấy game phiền.

Giải pháp:

- Giảm tốc độ tụt chỉ số.
- Dùng thông báo hợp lý.
- Không phạt quá nặng khi offline lâu.

### 33.2. Quá nhiều chỉ số

Nếu có quá nhiều chỉ số, người chơi mới sẽ khó hiểu.

Giải pháp:

- MVP chỉ nên hiển thị 4 - 5 chỉ số chính.
- Các chỉ số ẩn như CareScore không cần hiển thị.

### 33.3. Pet chết quá dễ

Nếu pet chết quá dễ, người chơi có thể bỏ game.

Giải pháp:

- Dùng cơ chế “rời đi” thay vì chết.
- Cho cơ hội cứu pet.
- Khi offline lâu, đưa pet vào trạng thái yếu/bệnh trước.

### 33.4. Gameplay lặp lại

Nếu chỉ có bấm nút, game dễ chán.

Giải pháp:

- Thêm mini game.
- Thêm tiến hóa.
- Thêm item.
- Thêm nhiệm vụ ngày.
- Thêm sưu tầm.

## 34. Định hướng MVP khuyến nghị

Để bắt đầu nhanh, nên làm phiên bản đầu tiên với phạm vi sau:

```text
1 pet duy nhất
1 phòng duy nhất
5 chỉ số: Hunger, Happiness, Cleanliness, Energy, Health
6 hành động: Feed, Play, Clean, CleanPoop, Heal, Sleep
Có save/load bằng JSON
Có offline progress
Có 5 trạng thái biểu cảm
Có 3 giai đoạn phát triển: Baby, Child, Adult
Có 1 mini game đơn giản
```

Không nên làm shop, online, nhiều pet hoặc trang trí phòng ngay từ đầu. Những phần đó nên để sau khi gameplay chăm sóc cơ bản đã ổn.

## 35. Kết luận

Dự án Nuôi Thú Ảo nên bắt đầu từ một hệ thống chăm sóc đơn giản nhưng có chiều sâu. Trọng tâm không phải là nhiều tính năng ngay từ đầu, mà là làm cho người chơi cảm thấy pet có phản ứng, có nhu cầu và có sự phát triển theo thời gian.

Phiên bản MVP chỉ cần có pet, chỉ số, hành động chăm sóc, lưu dữ liệu, thời gian offline và tiến hóa cơ bản là đã đủ tạo cảm giác giống máy nuôi thú ảo cổ điển. Sau đó có thể mở rộng dần sang mini game, shop, item, trang trí, sưu tầm và tương tác online.
