# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602208
- Ngày / CVAT local: 17/09/2026 / http://localhost:8080
- Công cụ đã dùng: CVAT (Brush, Polygon), SAM 2

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000458325.jpg`, chiếc ô tô đỗ bên lề phải phía trước tiền cảnh.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Quy tắc biên: Chỉ vẽ phần thân xe nhìn thấy thực tế (thân vỏ, kính xe, bánh xe); dừng biên tại mép tiếp giáp giữa lốp xe và mặt đường (không vẽ tràn bóng đổ của gầm xe xuống lòng đường); không tự ý mở rộng biên vào người đi bộ đứng sát cạnh.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Khi chạy SAM 2, một số đề xuất bị nuốt dính bóng đổ gầm xe vào mask hoặc gộp người đi bộ kế bên vào thân xe. Em đã dùng Brush xóa phần bóng đổ và tách người đi bộ thành object `person` riêng.
- Nếu không dùng gợi ý: Có sử dụng gợi ý SAM 2 và đối chiếu, gọt biên thủ công bằng Brush/Polygon.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `hard_panoptic` / ảnh `000000350023.jpg` và `000000460147.jpg`
- Lỗi thuộc loại: khác (sai định dạng export dataset và ranh giới panoptic)
- Bằng chứng tôi nhìn thấy: Khi export dataset ban đầu chọn nhầm định dạng "Segmentation mask 1.1", chạy script kiểm tra `inspect_submissions.py` báo lỗi thiếu file annotations COCO JSON (`annotations/instances_default.json`).
- Quy tắc và hành động sửa: Quay lại CVAT local, kiểm tra lại ranh giới các đối tượng và chọn xuất đúng chuẩn "COCO 1.0" theo đúng yêu cầu đề bài; sau đó kiểm tra lại bằng script thì đạt trạng thái `[OK]`.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại thành công file `hard_panoptic.zip` chuẩn COCO 1.0.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Script `scripts/inspect_submissions.py` và notebook tự kiểm trả về 9/9 task `[OK]`, không có lỗi hợp đồng.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `cp4_curb` (ảnh `7d83710e-4697c3b2.jpg` - mép đường và vỉa hè) | (A) Phân chia theo màu sắc pixel (màu sẫm là road, màu sáng là sidewalk); (B) Phân chia theo kết cấu bó vỉa và chức năng sử dụng | Quy tắc bài lab: ranh road–sidewalk theo chức năng và gờ bó vỉa, không chỉ dựa vào màu sắc ảnh | Chọn phân theo gờ bó vỉa: mặt đường xe chạy là `road`, bậc thềm phía trên là `sidewalk` |
| 2. `cp1_holes` (ảnh `000000144300.jpg` - kính chắn gió và kính cửa xe ô tô) | (A) Khoét rỗng kính trong suốt vì nhìn xuyên thấu cảnh phía sau; (B) Giữ liền khối kính trong mask của xe | Quy tắc checkpoint `cp1_holes`: kính và khe hở nằm trong mask của vật, không khoét tùy tiện | Chọn bao trùm toàn bộ kính xe vào mask của object `car` |
| 3. `cp5_occlusion` (ảnh `000000336232.jpg` - xe bị cột/biển báo che cắt ngang) | (A) Tách thành 2 object `car` riêng biệt cho 2 phần nhìn thấy; (B) Gộp 2 mảng nhìn thấy vào cùng 1 object/instance duy nhất | Quy tắc instance segmentation: một vật thể bị che thành các mảng rời rạc vẫn là một instance duy nhất | Nhóm cả 2 mảng nhìn thấy về chung 1 object `car`, không tạo 2 instance trùng lặp |
