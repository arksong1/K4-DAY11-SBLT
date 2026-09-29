# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Đường kẻ dài chạy ngang chia cách khu vực đỗ xe (có nhiều điểm nối) và các vạch kẻ dọc phân chia từng ô đỗ xe ở nửa dưới ảnh.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Không vẽ các mép lề đường (curb) vì đó là ranh giới vật lý, không phải vạch sơn đỗ xe (parking line).
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Bao phủ khu vực đường đi (driveway) giữa các dãy đỗ xe, dừng ở sát mép các vạch đỗ và không vẽ đè lên xe cộ hoặc chướng ngại vật (nếu có).
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): Không có
