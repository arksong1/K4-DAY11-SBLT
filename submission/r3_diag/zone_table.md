# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 6 | 1 | 1 | 4 | 5 | WRONG_CLASS (1) |
| mid | 7 | 2 | 6 | 3 | 10 | SPURIOUS (4) |
| edge | 7 | 0 | 1 | 1 | 1 | SPURIOUS (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: Cả người (L) và model (M) đều mắc lỗi nhiều nhất ở zone **mid**. Đối với L, có tới 6 lỗi SPURIOUS. Đối với model (M), có 10 lỗi thừa (M_only + LM_noR) và 3 lỗi missing.
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: Nguyên nhân chính là do hiệu ứng méo ảnh fisheye làm các vật thể ở vùng mid bị biến dạng hoặc chồng lấn, dẫn đến việc vẽ box quá lỏng (như trường hợp Pedestrian) hoặc nhầm nhãn (Bus thay vì Car). Bên cạnh đó, việc L gán nhầm vùng `ego_body` thành Bike cũng đóng góp vào số lỗi SPURIOUS lớn. Giới hạn của slice chỉ có 3 frame khiến các lỗi cá biệt (như gán nhầm `ego_body` ở cả 3 ảnh) làm lệch đáng kể tỷ lệ lỗi.
