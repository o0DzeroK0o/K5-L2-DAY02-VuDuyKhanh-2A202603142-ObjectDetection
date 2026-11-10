# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Vũ Duy Khanh
- MSSV: 2A202603142
- Email: khanhvd.ldm.0299@gmail.com
- Lớp: L2
- Link repo bài làm: https://github.com/o0DzeroK0o/K5-L2-DAY02-VuDuyKhanh-2A202603142-ObjectDetection.git
- Link Colab đã chạy: https://colab.research.google.com/drive/11Ha0w7ctyA4NHJGVethq10F1mWugPcT-?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý:
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: drive_001.jpg, drive_002.jpg, drive_003.jpg, drive_004.jpg, drive_005.jpg, drive_006.jpg, drive_007.jpg, drive_008.jpg, drive_009.jpg, drive_010.jpg
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
- Commit khóa nhãn ban đầu: f82bf4f3ac0c02b1457494827bebe3e2782e5e1d

## 4. Gold QC và rework

| Chỉ số              | Trước sửa | Sau sửa nếu có |
| ------------------- | --------: | -------------: |
| TP                  |       417 |            442 |
| FP                  |       352 |            457 |
| FN                  |       236 |            211 |
| Precision           |    0.5423 |         0.4917 |
| Recall              |    0.6386 |         0.6769 |
| F1                  |    0.5865 |         0.5696 |
| mean_iou_of_matches |    0.8529 |         0.8431 |
| passed              |     false |          false |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: torch-2.14.1+cu130 CUDA:0 (Tesla T4, 14913MiB)
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval | Giá trị |
| ----------------------- | ------: |
| Precision               |  0.4105 |
| Recall                  |  0.2302 |
| mAP50                   |  0.2722 |
| mAP50–95                |  0.2016 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
   Lớp nào recall là Van. Ảnh **`drive_051.jpg`** và**`drive_056.jpg`**
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
   Cần kiểm tra độ chính xác của vị trí và bốn cạnh box:
	- Box có thừa nền, cắt mất phần xe hoặc lệch tâm không?
	- Có gộp hai xe vào một box không?
	- Với xe bị che/cắt khung, nhãn có nhất quán theo quy tắc bao phần nhìn thấy không?
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
   Nhầm car thành van. Dữ kiện trong ảnh: drive_051.jpg có xe đỏ ở tiền cảnh được dự đoán van 0.99.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
   Không đưa chúng vào train để giữ một tập ảnh không tham gia cập nhật trọng số, giúp kiểm tra khả năng nhận diện ngoài dữ liệu huấn luyện. Train rồi chấm trên cùng ảnh có thể làm kết quả quá lạc quan.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm               | Lỗi quan sát                                                                                     | Cách đã thử                                          | Kết quả/còn thiếu                                                                                                                                     |
| ---------------------------- | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Gán nhãn và rà ảnh trên CVAT | Một số xe bị che khuất, cắt khung hoặc có phản chiếu khiến việc xác định cạnh box khó nhất quán. | Rà bằng mắt các ảnh drive_001 đến drive_010          | Đã có quy tắc bao phần xe nhìn thấy, không đoán phần bị che và không lấy phản chiếu làm xe riêng. Chưa ghi đầy đủ từng box đã sửa và kết quả checker. |
| Chấm nhãn với gold set       | Cả hai kết quả đánh giá đều chưa đạt: F1 lần lượt 0.5696 và 0.5865, trong khi yêu cầu là 0.80.   | Xem báo cáo đánh giá, phân tích TP/FP/FN và mean IoU | vẫn còn lỗi bỏ sót, sai lớp hay lệch box                                                                                                              |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.

|Công cụ|Bước sử dụng|Mục đích|
|---|---|---|
|CVAT|Gán nhãn dữ liệu|Vẽ bounding box, chọn lớp phương tiện và xuất nhãn định dạng YOLO.|
|YOLO (`yolo26n.pt`)|Huấn luyện và đánh giá|Huấn luyện mô hình nhận diện `car`, `truck`, `bus`, `van`; đánh giá và xem ảnh dự đoán trên tập eval.|
|Google Colab|Chạy notebook|Chạy huấn luyện, đánh giá mô hình và lưu checkpoint `best.pt` cùng các chỉ số.|
|ChatGPT|Hỗ trợ hiểu yêu cầu và phân tích kết quả|Giải thích TP/FP/FN, IoU, mAP; hỗ trợ soạn mini guideline và nhận xét các tình huống mơ hồ từ ảnh.|