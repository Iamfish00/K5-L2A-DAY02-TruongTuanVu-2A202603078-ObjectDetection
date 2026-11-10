# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` |ô tô con , là phương tiện cá nhân  |khá nhỏ gọn |
| `truck` | xe ô tô dùng để chở hàng hóa , vật nặng | to , có thùng để đồ đằng sau|
| `bus` | xe ô to tô chở được nhiều người | là loại phương tiên công cộng , lớn |
| `van` | xe ô tô kín chở được nhiều người| thường dùng để chở từ 5-7 người hoặc hàng hóa , kín   |

## Quy tắc chung

- Box bám sát vật thể nghĩa là:• Bounding box (hộp giới hạn) phải vừa khít tuyệt đối với các cạnh ngoài cùng của vật thể. Không được để thừa quá nhiều khoảng trống (background) xung quanh và không được cắt lẹm vào bộ phận của vật thể.
- Vật thể bị che khuất: ẫn phải vẽ box bao quanh toàn bộ vật thể bao gồm cả phần bị che khuất dựa trên ước lượng hoặc phán đoán logic, trừ khi quy định dự án yêu cầu chỉ gắn nhãn phần nhìn thấy được
- Vật thể bị cắt bởi rìa ảnh: • Vẽ box kéo dài sát đến tận biên (rìa) của bức ảnh để bao trọn phần vật thể còn xuất hiện trong khung hình. Không vẽ box vượt ra ngoài phạm vi pixel của ảnh.
- Vật thể rất nhỏ/mơ hồ: • Nếu vật thể quá nhỏ (ví dụ: dưới 10-15 pixel) hoặc quá mờ đến mức mắt người không thể nhận diện được đó là gì, thì bỏ qua không gắn nhãn, hoặc gắn nhãn vào danh mục đặc biệt (như ignore hoặc dontcare) tùy theo bộ quy chuẩn riêng của từng dự án.


## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_001.jpg` |Xe trắng ở làn bên phải bị cột che một phần |giữ một box `car`|Phần thân xe còn thấy đủ để nhận diện và xác định đây là cùng một xe|
| `drive_002.jpg` |Xe thân cao màu sáng bị cắt ở mép phải ảnh |Giữ một box `van` trong phạm vi ảnh |  Phần thân còn thấy đủ để nhận diện. Box bám phần xe nằm trong khung hình|
| `drive_008.jpg` |Xe dài màu vàng-xanh và xe thùng đỏ ở cùng giao lộ | Gán xe vàng-xanh là `bus`, xe thùng đỏ là `truck`|Xe buýt có dãy cửa kính hành khách, còn xe tải có thùng chở hàng phía sau cabin |
