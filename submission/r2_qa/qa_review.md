# QA review · B4-dense

- **Reviewer (vai B):** Nguyễn Đức Văn (MSSV: 2A202602115)
- **Chủ nhãn (vai A):** Trần Đăng Ka Song (MSSV: 2A202602228)
- **Slice:** B4-dense
- **Mã khóa:** F65B-8C12

| frame | object_ref | rule_id | điều nhìn thấy | điều cần kiểm lại |
|---|---|---|---|---|
| adasind_258420.jpg | L12 | R07 | Box L12 gán nhãn Bike vẽ trùm lên gương và thân xe ego ở góc dưới bên trái (pos: x=0.0, y=988.5, w=494.3, h=814.3); đồng thời frame thiếu polygon ignore_region (reason=ego_body). | Xóa box L12 (không gán nhãn chướng ngại vật cho xe ego) và chuyển sang vẽ polygon ignore_region với reason="ego_body" bao quanh phần thân xe/gương xe ego theo đúng quy ước R07. |
| adasind_258420.jpg | L10 | R03 | Box L10 gán nhãn Pedestrian (pos: x=275.8, y=785.2, w=28.1, h=68.2) nằm đè trực tiếp lên vị trí người ngồi trên xe ba bánh L1 ThreeWheeler (pos: x=289.0, y=759.0). | Kiểm tra người lái/người ngồi trên phương tiện ThreeWheeler; theo R03 người ngồi trong hoặc trên phương tiện không vẽ box Pedestrian riêng, cần xóa box L10 để tránh tính thừa (SPURIOUS). |
| adasind_258420.jpg | L9 | R03 | Box L9 gán nhãn Bike (pos: x=240.7, y=792.7, w=18.0, h=62.2) chồng lấn với thân xe ô tô L3 Car (x=207.1 đến 274.5), không thấy xe hai bánh riêng biệt. | Kiểm tra lại vùng ảnh xe ô tô L3; nếu không có xe hai bánh riêng biệt độc lập mà là bóng/người trong xe thì cần xóa box L9 theo R03. |
| adasind_270517.jpg | L5 | R07 | Box L5 gán nhãn Bike vẽ ở góc dưới bên trái (pos: x=0.0, y=996.3, w=165.3, h=743.7), thực chất là gương và thân xe ego; frame thiếu polygon ignore_region (reason=ego_body). | Xóa box L5 Bike và thay bằng polygon ignore_region với reason="ego_body" bao quanh phần xe ego theo R07. |
| adasind_270517.jpg | L7 | R04 | Box L7 gán nhãn Bus (pos: x=41.8, y=762.8, w=79.2, h=79.2) ở lề trái đường, nhưng hình dáng và kích thước thực tế trên ảnh là xe ô tô con/sedan cỡ nhỏ. | Kiểm tra đối tượng phương tiện: đây là ô tô con chứ không phải xe buýt/minibus; cần đổi nhãn từ Bus sang Car theo quy ước R04. |
| adasind_270517.jpg | L8 | R04 | Box L8 gán nhãn Bus (pos: x=275.7, y=755.0, w=97.6, h=74.4) đi phía trước ở làn giữa, hình dáng và kích thước nhỏ là ô tô con (hatchback/sedan). | Kiểm tra đối tượng phương tiện: đây là ô tô con, cần đổi nhãn từ Bus sang Car theo quy ước R04. |
| adasind_270517.jpg | L2 | R01 | Box L2 gán nhãn ThreeWheeler (pos: x=115.4, y=768.8, w=34.2, h=40.1) ở rất xa, bị che khuất gần hết và mờ, chiều cao sát ngưỡng H=40 px. | Kiểm tra xem đối tượng có đọc được rõ không; nếu quá mờ hoặc bị che khuất gần hết thì chuyển sang polygon ignore_region (reason="unreadable") theo R06, hoặc xóa nếu H < 40 px theo R01. |
| adasind_310008.jpg | L1 | R07 | Box L1 gán nhãn Bike vẽ ở góc dưới bên trái (pos: x=0.0, y=1016.2, w=268.2, h=686.5), là gương và thân xe ego; frame thiếu polygon ignore_region (reason=ego_body). | Xóa box L1 Bike và bổ sung polygon ignore_region với reason="ego_body" che phủ thân xe ego theo R07. |
| adasind_310008.jpg | L3 | R02 | Box L3 Pedestrian (pos: x=27.3, y=876.9, w=61.3, h=156.6) vẽ quá rộng về chiều ngang, trùm lấn sang người đi bộ L4 ở bên trái và L2 ở bên phải. | Thu gọn biên ngang của box L3 bám sát ranh giới thân người nhìn thấy trên ảnh fisheye gốc theo R02, không để box quá lỏng làm chồng lấn các đối tượng kế bên. |

## Bằng chứng ảnh chụp (submission/screenshots/)

1. `submission/screenshots/adasind_258420_L12_ego_body.png`: Minh chứng box L12 gán nhãn Bike cho gương và thân xe ego thay vì polygon ego_body.
2. `submission/screenshots/adasind_258420_L10_rider_split.png`: Minh chứng box L10 Pedestrian vẽ tách người ngồi trên xe ba bánh L1 ThreeWheeler.
3. `submission/screenshots/adasind_270517_L7_L8_misclass_bus.png`: Minh chứng box L7 và L8 phân loại nhầm ô tô con thành Bus.
4. `submission/screenshots/adasind_310008_L1_ego_L3_ped.png`: Minh chứng box L1 Bike cho thân xe ego và box L3 Pedestrian vẽ lỏng chồng lấn người bên cạnh.
