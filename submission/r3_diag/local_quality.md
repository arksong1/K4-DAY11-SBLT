# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `f65b8c12e002578495a48d51b83e9d348026173a597f391369ca48f6e502e56c`; slice `B4-dense`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_258420.jpg, adasind_270517.jpg, adasind_310008.jpg. Frame thiếu trong export: không.
TP=17; FP=8; FN=3; số lần đối chiếu=26; mean IoU của TP=0.804.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.654 | 0.915 | 0.846 |
| precision | 0.680 | 0.475 | 0.000 |
| recall | 0.850 | 0.600 | 0.000 |
| jaccard | 0.607 | 0.475 | 0.000 |
| dice | 0.756 | 0.520 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 4 | 4 | 0 | 0.846 | 0.500 | 1.000 | 0.500 | 0.667 |
| Bus | 0 | 2 | 0 | 0.923 | 0.000 | 0.000 | 0.000 | 0.000 |
| Car | 0 | 1 | 3 | 0.846 | 0.000 | 0.000 | 0.000 | 0.000 |
| Pedestrian | 7 | 1 | 0 | 0.962 | 0.875 | 1.000 | 0.875 | 0.933 |
| ThreeWheeler | 6 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_258420.jpg | 7 | 5 | 1 | 0.538 | 0.583 | 0.875 |
| adasind_270517.jpg | 5 | 3 | 2 | 0.625 | 0.625 | 0.714 |
| adasind_310008.jpg | 5 | 0 | 0 | 1.000 | 1.000 | 1.000 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Bus | Car | Pedestrian | ThreeWheeler | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 4 | 0 | 0 | 0 | 0 | 0 |
| Bus | 0 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 2 | 0 | 0 | 0 | 1 |
| Pedestrian | 0 | 0 | 0 | 7 | 0 | 0 |
| ThreeWheeler | 0 | 0 | 0 | 0 | 6 | 0 |
| <extra> | 4 | 0 | 1 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
