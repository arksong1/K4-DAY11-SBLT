# Sensor context

Ảnh bãi đỗ xe (parking-lot-core.jpg, parking-lot-contrast.png)
Rig: đây là ảnh chụp bằng camera thông thường (không phải camera SVM gắn xe). Theo quan sát, camera đặt ở độ cao tầm mắt người đứng, hướng ngang về phía trước; không thấy cấu trúc gá camera hay dữ liệu rig/calibration đi kèm. Không có thông số nội tại/ngoại tại, nên không khẳng định vị trí gắn hay góc nhìn theo mét/độ.
ego_body: không nhìn thấy trong cả hai ảnh (không có capo, gương, tay lái hay phần thân xe nào của xe mang camera).
Vòng kính (lens circle): không có. Ảnh là ảnh chữ nhật kín khung, không có vành đen tròn; các vạch sơn và đường chân trời nhìn thẳng, không có biến dạng fisheye rõ rệt.
Ghi chú riêng từng ảnh:
core (960×640): nhìn ngang qua bãi đỗ về phía dãy nhà; ba vạch trắng ở góc dưới trái, bờ lề đường và dải cỏ ở giữa khung, vài xe đỗ ở xa.
contrast (960×720): bãi rất rộng và gần như trống; bầu trời chiếm khoảng nửa trên khung; một xe đỏ nhỏ ở xa bên trái; các vạch sơn ở phần dưới khung.
Giới hạn: một camera, ảnh tĩnh, không calibration; chỉ dùng để tập phân biệt vạch chia ô với lối xe chạy, không dùng để suy ra vùng lái xe an toàn.
B. Frame ADASIND của slice chung (SLICE_NHOM)

Tọa độ dưới đây là ước lượng bằng mắt trên ảnh gốc, kích thước 1080×1920 (ảnh dọc); xác nhận lại trên CVAT khi vẽ.

adasind_019560
Rig: camera mắt cá (fisheye) hướng về phía trước, chụp từ một phương tiện hai bánh đang chạy trên đường; bóng đổ của người lái và xe hiện ở tiền cảnh phía dưới bên trái nên camera đi cùng phương tiện đó. Ảnh không kèm tài liệu rig, nên không khẳng định điểm gắn chính xác hay thông số calibration.
ego_body: có nhìn thấy. Một mảng tối sát mép trái, phần dưới khung (khoảng y 1200–1550), có vẻ là phần thân/chân người lái hoặc phần xe mang camera, kèm một chi tiết tối nhỏ ở mép trái khoảng y 1090. Bóng đổ trên mặt đường ở phía dưới trái không phải thân xe ego, không vẽ ego_body cho phần bóng.
Vòng kính (lens circle): viền đen tròn bao quanh vùng ảnh. Mép trên vòng ở khoảng y 115, mép dưới khoảng y 1700; hai bên vòng chạm hoặc bị cắt bởi mép trái và phải khung. Vùng ảnh hữu ích chiếm khoảng bốn phần năm chiều cao khung; bốn góc và dải dưới khoảng 220 px là đen, nằm ngoài vòng kính.