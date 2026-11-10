# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp     | Định nghĩa của bạn                                                     | Ví dụ/điểm phân biệt                                                |
| ------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `car`   | Ô tô con chủ yếu dùng chở người.                                       | Ví dụ sedan, hatchback, SUV. Không phân lớp chỉ theo kích thước.    |
| `truck` | Xe tải có thiết kế chủ yếu để chở hàng.                                | Thường có cabin và thùng/sàn chở hàng phía sau; ví dụ xe tải thùng. |
| `bus`   | Xe buýt hoặc xe khách được thiết kế chở nhiều hành khách.              | Thường có khoang hành khách dài, nhiều hàng cửa sổ.                 |
| `van`   | Xe dạng van, có thân kín với khoang chở hàng hoặc chở người liền thân. | Phân biệt bằng kiểu thân và công năng thể hiện trong ảnh            |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: bốn cạnh box bao sát phần thân xe nhìn thấy được, hạn chế nền thừa; không gộp nhiều xe vào một box. Mỗi xe hợp lệ có một box riêng.
- Vật thể bị che khuất: vẫn gán nếu nhận diện chắc lớp; vẽ box bao quanh phần nhìn thấy được, không suy đoán phần bị che. Hai xe chồng nhau có hai box riêng.
- Vật thể bị cắt bởi rìa ảnh: chỉ gán phần nhìn thấy được và đặt cạnh box đúng rìa ảnh; không kéo box vượt ảnh hay đoán phần ngoài khung.
- Vật thể rất nhỏ/mơ hồ: nếu vẫn nhận diện chắc lớp thì gán theo phần nhìn thấy; nếu chỉ còn mảnh quá nhỏ hoặc không chắc thì không được phép tự đoán.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh         | Tình huống                                                                                                                                            | Quyết định cuối                                    | Lý do theo schema                                                                           |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `drive_004` | Xe cam phía dưới bên phải bị cắt bởi mép ảnh.                                                                                                         | Gán một box car cho phần xe nhìn thấy.             | xe bị cắt khung khi vẫn nhận diện được lớp.                                                 |
| `drive_009` | Xe con màu đỏ ở gần giữa ảnh, ngay dưới đầu xe buýt đỏ phía trên và sau nóc xe buýt lớn ở tiền cảnh, bị che nhiều nhưng vẫn thấy phần nóc và kính xe. | Gán một box car riêng bao phần nhìn thấy của xe đỏ | Vật thể bị che vẫn được gán nếu nhận diện được lớp                                          |
| `drive_011` | Phương tiện hai/ba bánh chở thùng vàng cạnh xe buýt dễ bị nhầm thành xe tải nhỏ.                                                                      | Không gán box cho phương tiện.                     | Chỉ gán phương tiện thuộc bốn lớp car, truck, bus, van. Không gán xe đạp hoặc mô tô/xe máy. |
