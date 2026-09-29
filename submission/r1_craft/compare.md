# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_258420.jpg
- L3+R5 mid BOX_GEOMETRY
- L8 mid SPURIOUS
- L9 mid SPURIOUS
- L10 mid SPURIOUS
- L12 mid SPURIOUS
## adasind_270517.jpg
- L2 mid IGNORE_SCOPE
- L5 edge SPURIOUS
- L7+R6 mid WRONG_CLASS
- L8+R5 center WRONG_CLASS
## adasind_310008.jpg
- L1 edge IGNORE_SCOPE

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 6 | 5 | 1 | 1 |
| mid | 7 | 5 | 2 | 6 |
| edge | 7 | 7 | 0 | 1 |
