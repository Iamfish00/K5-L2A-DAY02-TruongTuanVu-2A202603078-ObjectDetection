# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Trương Tuấn Vũ
- MSSV: 2A202603078
- Email: tvu562005@gmail.com
- Lớp: K5-L2A
- Link repo bài làm: https://github.com/Iamfish00/K5-L2A-DAY02-TruongTuanVu-2A202603078-ObjectDetection
- Link Colab đã chạy:https://colab.research.google.com/drive/1xXJzMYGrb459JKXrWOzmYGpIXg7_4cvT?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.
xe con bị cột che trong `drive_001.jpg`
xe van bị cắt ở mép ảnh trong `drive_002.jpg`
xe con quá nhiều ở ở mép ảnh trong `drive_002.jpg`

## 3. Annotation và self-QC

- Số file nhãn train:50 file 
- Kết quả checker và lỗi đã xử lý: YOLO đạt 50/50
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: drive_001.jpg tới drive_011.jpg
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
- Commit khóa nhãn ban đầu:`3722972b`.

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP |  474| |
| FP |567 | |
| FN |179 | |
| Precision |  0,4553| |
| Recall | 0,7259  | |
| F1 | 0,5596| |
| mean_iou_of_matches |0,8332 | |
| passed |false | |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
- Môi trường — Google Colab, CPU.
- Ultralytics — 8.4.208 theo metadata của checkpoint.
- Torch — [Điền phiên bản từ dòng đầu của log huấn luyện].
- Cấu hình — `yolo26n.pt`, 50 epoch, kích thước đầu vào 640, seed 20260909.
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:`/content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt`.

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0,4592 |
| Recall |0,2370 |
| mAP50 |0,2745 |
| mAP50–95 |0,2032 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.
[Ảnh dự đoán](assets/eval_predictions/visuals/) · [Log huấn luyện và đánh giá](assets/yolo26_runs/)
Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
   `bus`, với recall 0,0000
   [`drive_051.jpg`](assets/eval_predictions/visuals/drive_051.jpg),
   box `bus` dự đoán nằm lệch về mép phải so với xe buýt có nhãn
   eval ở gần cột.
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
   Khi yêu cầu độ trùng giữa box dự đoán và box chuẩn cao hơn, điểm giảm từ 27,45% xuống 20,32%. Cần xem từng cặp box để tìm khung lệch tâm, quá rộng  hoặc cắt mất một phần xe.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
   Trong
   [`drive_054.jpg`](assets/eval_predictions/visuals/drive_054.jpg), xe đỏ ở phía dưới bên phải có nhãn eval là `car`, nhưng model dự đoán `van` với confidence khoảng 0,95. Đây là ca cần đối chiếu cách phân biệt xe con và xe van theo dáng thân.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
   Trọng số được học từ 50 ảnhtrain. Mười ảnh eval dùng để theo dõi validation, chọn `best.pt` và báo chỉ số. Vì đã dùng để chọn checkpoint, tập eval không phải tập kiểm thử độc lập.
## 6. Khó khăn và cách xử lý
Tool 2 ban đầu báo thiếu `--student-labels` và `--gold-labels`. Sau khi truyền đúng hai đường dẫn trong PowerShell, tool chấm đủ 50 ảnh. Phiên Colab chạy bằng CPU và xuất được ZIP kết quả.
| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| | | | |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.
Đã có đủ 50 nhãn, kết quả checker, báo cáo chấm với gold và kết quả huấn luyện, đánh giá YOLO. F1 của nhãn chưa đạt ngưỡng mặc định. Recall của model là 23,70% trên 10 ảnh eval, trong đó `bus` và `van` là hai lớp có recall thấp nhất.
## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
Dùng Codex để kiểm tra lệnh PowerShell, xử lý lỗi môi trường
notebook
