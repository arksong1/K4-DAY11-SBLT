# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `ego_body`: frame `adasind_258420`, `adasind_270517`, `adasind_310008` | 3 ca `IGNORE_SCOPE` (box `Bike` vẽ lên gương/thân xe ego thay vì polygon `ego_body`), mỗi frame một ca, mức P0 | Cùng một lỗi lặp lại ở cả ba frame nên là lỗi hệ thống, sai R07 chứ không phải sai ngẫu nhiên; và có thể góp vào 4 FP của class `Bike` ở `local_quality.md` cùng số liệu zone | `qa_review.md` dòng L12, L5, L1; ảnh `adasind_258420_L12_ego_body.png`, `adasind_310008_L1_ego_L3_ped.png`; `selfqc.md` ghi thiếu `ego_body` cả ba frame; rule R07 |
| Zone `mid` (nổi bật ở `adasind_258420`) | Người (L): 6 ca SPURIOUS, 2 ca thiếu; model (M): 10 ca thừa, 3 ca thiếu (`zone_table.md`); ví dụ L8, L9, L10, L12 và `L3+M6` ở `adasind_258420` | Zone có nhiều lỗi nhất ở cả người lẫn model. Nguyên nhân lẫn hai loại: lỗi nhãn (E1, owner annotator, cần rework) và model lệch miền fisheye (E4, owner ai_team, giữ với lý do), nên cần tách để không sửa nhầm nhãn theo model | `zone_table.md`; các dòng `r3_diag` trong `findings.csv`; `model_compare.md`; ảnh `adasind_258420_L10_rider_split.png` |

Giới hạn của kết luận từ ba frame ADASIND: ba frame chỉ từ một camera và một tình huống đường, số ca lỗi nhỏ nên một hai ca (như `ego_body` lặp ở cả ba frame) đã làm lệch tỷ lệ theo zone. Kết luận về zone hay loại lỗi nào nhiều nhất chỉ cho biết nơi nên soi trước, không đo được tỷ lệ lỗi thật. Teaching reference dùng để so chỉ là bản dạy học trên vài frame, có thể sai, nên bất đồng với nó chưa phải lỗi của người gán nhãn. Ba frame này không đại diện cho camera trước, sau, trái, phải của xe.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`: đếm số *cảnh* khác nhau trong từng ô camera × normal/hard, không đếm số frame. Nhiều frame liền nhau trong cùng một cảnh gần như là một ca, nên mỗi cảnh chỉ lấy vài frame cách nhau đủ xa, và tổng số cảnh của mỗi ô phải đủ để không phụ thuộc vào một tình huống duy nhất. Sau đó đối chiếu hard case của từng camera với danh sách ở `46_gold_set_plan.md` (ánh sáng xấu, vật sát thân xe, vùng seam, vật bị vòng kính cắt) để chắc mỗi nhóm có ít nhất một cảnh. Ô nào thiếu cảnh thì bổ sung trước khi review.

Kế hoạch này chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: 200 frame được chọn có chủ ý thiên về ca khó nên không phải mẫu ngẫu nhiên của 50.000 frame, và tập này là tình huống giả lập, không có dữ liệu bốn camera thật. Muốn ước lượng tỷ lệ lỗi cần thêm một mẫu ngẫu nhiên riêng, được review độc lập.
