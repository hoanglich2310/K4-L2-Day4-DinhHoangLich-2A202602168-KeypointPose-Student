# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Đinh Hoàng Lịch   Nhóm: ______   Ngày: 16/9/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số                         |                     Giá trị |
| -------------------------------- | ----------------------------: |
| Số ảnh đã gán               |                            20 |
| Số skeleton                     |                            27 |
| v=2 / v=1 / v=0                  | v=2 - 341/ v=1 - 95/ v=0 - 23 |
| Thời gian trung bình mỗi ảnh |                               |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_ear
2. right_ear
3. right_eye

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

- Chúng đúng là những khớp khó gán, vì những khớp đó thường ở phần đầu và bị che khuất khi người quay mặt đi hoặc đội mũ, đeo kính,...

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số                | Trước rework | Sau rework |
| ----------------------- | -------------: | ---------: |
| OKS trung bình         |          0.947 |      1.000 |
| OKS@0.50                |          0.931 |      1.000 |
| OKS@0.75                |          0.931 |      1.000 |
| Lỗi`dao_trai_phai`   |              0 |            |
| Lỗi`nham_nguoi`      |              0 |            |
| Lỗi`xoa_khop_bi_che` |              0 |            |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- Ảnh "train_13", thiếu 2 người mờ ở phía sau, tôi đánh thêm 2 skeleton
- 
- 

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

- Lỗi này tôi gặp khi chấm với model, không phải chấm với gold. Ở ảnh "train_16" nhân vật hướng người về phía trước nhưng quay mặt ra ngoài -> khó đánh các khớp trên mặt và bị đánh lỗi đảo trái/phải

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

## 3. Kiểm chéo

Bạn cùng nhóm: `KHÔNG KIỂM CHÉO`

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| ----- | ---: | --: | ----: | --------------------------------------- |
|       |      |     |       |                                         |
|       |      |     |       |                                         |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số       | yolo26n-pose gốc | Sau fine-tune |  Chênh |
| -------------- | ----------------: | ------------: | ------: |
| pose_mAP50     |         `0.845` |     `0.845` |       0 |
| pose_mAP50-95  |        `0.6853` |     `0.702` |  0.0167 |
| pose_precision |        `0.9734` |     `0.979` |  0.0056 |
| pose_recall    |        `0.8462` |     `0.846` |  0.0002 |
| box_mAP50-95   |        `0.8119` |     `0.811` | -0.0009 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
   * `pose_mAP50-95` thay đổi -0.0009. Với tập validation chỉ ~13 người, mức giảm 0.0009 nằm trong sai số thống kê nên khó khẳng định là suy giảm thật. Về mặt định tính, 20 ảnh mới nhiều khả năng dạy model thích nghi với góc chụp/bối cảnh/tư thế đặc thù của tập dữ liệu tôi, chưa được COCO bao phủ tốt. Đổi lại, khi xem toàn bộ log huấn luyện, tôi phát hiện tại epoch 13 training bị sụp đổ đột ngột (loss nổ, mAP về gần 0) và không hồi phục hoàn toàn — dấu hiệu cho thấy có thể một vài nhãn/keypoint trong 20 ảnh mới bị lỗi định dạng, gây mất ổn định gradient. `best.pt` nộp là checkpoint trước khi sụp đổ nên vẫn tốt, nhưng tôi cần rà lại nhãn của 20 ảnh mới trước khi kết luận về chất lượng dữ liệu.
2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
   * box_mAP50-95 (0.811) cao hơn pose_mAP50-95 (0.702) khoảng 0.109. Điều này cho thấy model tìm *người* dễ hơn tìm  *khớp* : phát hiện bounding box chỉ cần định vị một vùng lớn nên dung sai lỗi cao, trong khi định vị 17 keypoint đòi hỏi độ chính xác pixel-level cho từng điểm nhỏ, dễ bị ảnh hưởng bởi che khuất, mờ chuyển động và nhầm lẫn trái/phải — đây là lý do pose luôn là bài toán khó hơn box trong cùng một kiến trúc model
3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):
   * Ảnh "train_16" - đánh lỗi đảo trái/phải
4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
   * Ảnh "train_11" - Tôi thấy tôi đúng vì, ảnh này khó để đánh các khớp, tôi đang đánh 2 khớp left_ankle và right_ankle là v0 vì tôi thấy mép ảnh có thể đã cắt qua nhưng model lại đánh giá là người đã nằm trọn trong ảnh.
5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?
   * Ảnh "train_13", tôi đánh thiếu 2 người vì chất lượng ảnh thấp không rõ được vật thể, trong trường hợp nếu đó là tấm fomex in hình người thì sẽ thế nào? có xác định đó vẫn là người không?

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

- Keypoint trong ảnh core "`train_11`" là left_ankle và right_ankle. Ảnh mô tả người phụ nữ bị bàn che mất phần thân dưới, tôi đang phân vân giữa việc xem nhân vật đó đang đứng hay ngồi. Rồi đưa ra quyết định keypoint đó tôi đặt là v=0 vì tôi phải ước lượng tỷ lệ cơ thể thì phần chân đã bị mép ảnh cắt nên tôi chỉ giữ lại phần khớp left và right_knee ở trường hợp v=1.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
