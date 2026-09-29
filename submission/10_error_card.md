# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | MISSING | 5 |
| center | B4 | SPURIOUS | 6 |
| center | B4 | WRONG_CLASS | 1 |
| center | C0 | SPURIOUS | 2 |
| edge | B4 | IGNORE_SCOPE | 1 |
| edge | B4 | MISSING | 1 |
| edge | B4 | SPURIOUS | 3 |
| edge | C0 | SPURIOUS | 1 |
| mid | B4 | BOX_GEOMETRY | 1 |
| mid | B4 | IGNORE_SCOPE | 1 |
| mid | B4 | MISSING | 3 |
| mid | B4 | SPURIOUS | 19 |
| mid | B4 | WRONG_CLASS | 1 |
| unknown | B4 | BOX_GEOMETRY | 1 |
| unknown | B4 | IGNORE_SCOPE | 3 |
| unknown | B4 | MISSING | 1 |
| unknown | B4 | SPURIOUS | 2 |
| unknown | B4 | WRONG_CLASS | 2 |

## Top defects
- SPURIOUS: 33 (ví dụ frame adasind_019560.jpg)
- MISSING: 10 (ví dụ frame adasind_258420.jpg)
- IGNORE_SCOPE: 5 (ví dụ frame adasind_258420.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy:
  - **Lỗi nổi bật nhất là `ego_body` (`IGNORE_SCOPE`, P0), lặp ở cả ba frame** của slice `B4-dense`: `adasind_258420` L12, `adasind_270517` L5, `adasind_310008` L1. Ở mỗi frame, gương và thân xe ego ở góc dưới bên trái bị vẽ thành box `Bike` thay vì polygon `ignore_region` với `reason=ego_body` (R07). Lỗi lặp đủ ba frame nên là lỗi hệ thống, không phải sai ngẫu nhiên: dòng `r2_qa` cùng cấu trúc ở cả ba frame, và `selfqc.md` đã ghi "thiếu ego_body" cho cả ba frame nhưng bản khóa vẫn giữ box `Bike`. Nguyên nhân khả dĩ (`E1_annotator_error`): gương và tay lái của xe ego có hình dáng gần với xe hai bánh trên ảnh fisheye ở mép ảnh, nên bị nhầm với vật cần gán nhãn. Đây là giả thuyết; ảnh minh chứng ủng hộ nhưng nhóm chưa có thí nghiệm đối chứng.
  - **Lỗi `SPURIOUS` (33 dòng) không thuần là lỗi của người gán nhãn.** 15 dòng là `M_only` (model thấy, reference không có), thuộc `E4_model_domain`. Phần còn lại phần lớn là đếm lặp cùng một vật qua `r1_craft`, `r2_qa` và `r3_diag`; chỉ có khoảng 8 vật của nhãn ở `adasind_258420` (L3, L8, L9, L10, L12) và `adasind_270517` (L5, L7, L8), cộng 3 dòng ở vòng C0. Vì thế con số 33 cao hơn số vật lỗi thật.
  - **Hai nguyên nhân khác, không phải lỗi nhãn:** (1) `adasind_258420` L10: người ở mép xe ba bánh L1 bị B ghi `SPURIOUS` theo R03, nhưng R03 chỉ nêu ô tô và xe buýt, không nêu xe ba bánh, nên là khoảng trống luật (`E2_guideline_gap`). (2) Các ca `M_only` và `LR_noM` tập trung ở zone `mid` (zone_table: 10 ca model thừa, 3 ca model thiếu), phù hợp giả thuyết model gốc huấn luyện trên ảnh phẳng nên lệch miền với fisheye (`E4_model_domain`); giả thuyết này cần xem thêm overlay, chưa kết luận chắc.
  - **Lỗi phân loại:** `adasind_270517` L7 và L8 là xe con nhưng gán `Bus` (R04, `WRONG_CLASS`); ma trận nhầm cho Car→Bus = 2, cùng hướng với nhận định này.
- Cách sửa và ai nhận việc (`owner`):
  - `ego_body`: xóa ba box `Bike`, vẽ polygon `ego_body` ở mỗi frame; owner `annotator` (A), B kiểm lại sau rework (`action=rework`, D01).
  - Bus → Car ở L7, L8: đổi class; owner `annotator` (D03). Hai dòng `R5+M3`, `R6+M1` ở `adasind_270517` là cùng hai xe này nên không thêm box mới.
  - L10 người ở mép xe ba bánh: escalate cho `guideline`, đề xuất R03a trong `20_guideline_patch.md`; chưa tính là lỗi của A cho đến khi có quyết định (`action=escalate`, D02, `30_escalation_ticket.md`).
  - Các ca `M_only` và `LR_noM`: không sửa nhãn theo model; owner `ai_team`, `action=keep_with_reason` (D07).
  - Việc cần kiểm thêm: `adasind_258420` `L3+M6` (`LM_noR`) có thể là lỗi của reference (E0); ca L9 và `adasind_270517` L2 chờ soát ảnh gốc (D06).
  - Kết quả rework v2 (`1D9A-1D41`, `rework/delta.md`): zone `center` matched 5→6, missing 1→0, spurious 1→0; `mid` matched 5→6, missing 2→1, spurious 6→4; `edge` spurious 1→0. Đã sửa: 3 lỗi `ego_body`, L7/L8 Bus→Car, `adasind_310008` L3. Chưa sửa: `adasind_258420` L8, L9, R5; L10 giữ nguyên chờ quyết định của guideline. Vì vậy rework mới đạt một phần, chưa coi là xong.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule):
  - Ảnh: `adasind_258420_L12_ego_body.png`, `adasind_310008_L1_ego_L3_ped.png`, `adasind_258420_L10_rider_split.png`, `adasind_270517_L7_L8_misclass_bus.png`.
  - Dòng `findings.csv`: `r2_qa` cho L12, L5, L1 (R07) và L7, L8 (R04); `r3_diag` L10 (`E2_guideline_gap`, `escalate`) và các dòng `M_only`/`LR_noM` (`E4_model_domain`).
  - Rule: R07 (`ego_body`), R04 (Bus/Car), R03 (rider và người trên phương tiện), R02 (box bám phần nhìn thấy).
  - Số liệu: `r3_diag/zone_table.md` (zone `mid` nhiều lỗi nhất), `r3_diag/local_quality.md` (Bike FP 4, Bus FP 2, Car FN 3).
  - Giới hạn: chỉ ba frame ADASIND của một camera, số ca nhỏ, và bảng đếm lặp một vật qua nhiều vòng, nên chỉ dùng để chọn ca cần soi, không đo được tỷ lệ lỗi thật.
