# Escalation ticket

## Ticket 1

- **Frame:** `adasind_258420.jpg` (slice `B4-dense`), đối tượng `L10` (Pedestrian) đè lên mép trái của `L1` (ThreeWheeler).
- **Ảnh chụp:** `submission/screenshots/adasind_258420_L10_rider_split.png`
- **Expected impact:** Nếu không có luật rõ, L10 bị tính là SPURIOUS của người gán nhãn (một trong các lỗi mid của frame này ở `findings.csv`) và làm tăng số lỗi zone `mid` ở `zone_table.md`, trong khi nguyên nhân có thể là khoảng trống luật (E2). Nhiều người gán nhãn sẽ vẽ ca này khác nhau, làm nhãn không nhất quán và gold set về sau lệch. Ở hệ SVM bốn camera, xe ba bánh chở người xuất hiện ở seam cũng sẽ gặp cùng vấn đề.
- **Owner:** `guideline`
- **Recommendation:** Guideline owner quyết định và bổ sung luật cho người ngồi hoặc bám trên xe ba bánh; nhóm đề xuất R03a trong `20_guideline_patch.md` (rules_version v1.0.0 → v1.1.0). Trong lúc chờ, chưa tính L10 là lỗi của người gán nhãn trong thống kê; sau khi có quyết định thì cập nhật `findings.csv` và bản rework, và Lab Coach xác nhận trên chính frame này.
