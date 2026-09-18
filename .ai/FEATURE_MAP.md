# FEATURE_MAP — <Tên dự án>

Nghĩa từng số ở `CLAUDE.md`. Bảng này liệt kê file + chi tiết kỹ thuật — nơi DUY NHẤT của sự thật hiện tại.

> ⚠️ **File có thể lớn dần** — CHỈ đọc bằng `grep -n "^### Px.y"` rồi `sed -n "X,Yp"` đúng mục cần. KHÔNG `cat`/mở cả file.
> CẤM viết narrative theo phiên (ai làm gì, lúc nào) vào đây — đó là việc của `.ai/WORKLOG.md` §2.
> Mục nào >3KB → tách heading `### Px.y` riêng bên dưới bảng chính (xem mẫu `P1.1` bên dưới).

| P | Chức năng | FE (file) | BE (file) | DB | Test/đo | Trạng thái |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `P1.1` | <Chức năng mẫu> | `<file frontend>` | `<file backend>` | `<bảng/cột nếu có>` | `<file test>` | Chưa làm |

## Mục chi tiết (khi 1 hàng bảng trên vượt ~3KB)

### P1.1
<Quyết định đã chốt · số đo thật · bẫy đã dính · lý do kỹ thuật — viết TẠI ĐÂY, không lặp ở CLAUDE.md/WORKLOG.>
