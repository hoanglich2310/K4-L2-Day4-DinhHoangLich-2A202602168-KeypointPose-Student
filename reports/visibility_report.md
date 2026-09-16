# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 27 skeleton, trung bình 16.15 khớp có v > 0 mỗi người
- Tổng: v=2 341 | v=1 95 | v=0 23

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 23 | 4 | 0 | 15% |
| 1 | left_eye | 20 | 7 | 0 | 26% |
| 2 | right_eye | 19 | 8 | 0 | 30% |
| 3 | left_ear | 10 | 17 | 0 | 63% |
| 4 | right_ear | 14 | 13 | 0 | 48% |
| 5 | left_shoulder | 26 | 1 | 0 | 4% |
| 6 | right_shoulder | 27 | 0 | 0 | 0% |
| 7 | left_elbow | 24 | 3 | 0 | 11% |
| 8 | right_elbow | 23 | 4 | 0 | 15% |
| 9 | left_wrist | 21 | 6 | 0 | 22% |
| 10 | right_wrist | 19 | 7 | 1 | 26% |
| 11 | left_hip | 22 | 5 | 0 | 19% |
| 12 | right_hip | 24 | 3 | 0 | 11% |
| 13 | left_knee | 19 | 5 | 3 | 19% |
| 14 | right_knee | 21 | 3 | 3 | 11% |
| 15 | left_ankle | 14 | 5 | 8 | 19% |
| 16 | right_ankle | 15 | 4 | 8 | 15% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
