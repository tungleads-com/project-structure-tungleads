# <Tên dự án> — CHỈ MỤC (index) cho Claude Code

**<Mô tả 1 dòng: dự án làm gì, cho ai>.** Stack: <VD Laravel + Inertia/React, hoặc WordPress child theme, hoặc Next.js...>.

> ⚠️ **File này CHỈ là chỉ mục** (để phiên nào cũng nạp ít token). **Trước khi code, đọc:**
> 1. **`AGENTS.md`** — luật làm việc: checklist đầu/cuối phiên · làn thay đổi A/B/C · sự thật/lịch sử ·
>    môi trường & lệnh chạy · kiểm chứng bắt buộc · hạn mức kích thước tài liệu.
> 2. **`.ai/WORKLOG.md`** *(nếu dự án dùng — xem README "Khi nào cần file nào")* — §1 (đang làm) + 10 dòng cuối §2.
> 3. **`.ai/FEATURE_MAP.md`** — chi tiết từng số: quyết định đã chốt sau khi đo · file thật · test.
>    ⚠️ File có thể lớn dần: **chỉ đọc bằng `grep -n "^### Px.y"` + `sed -n "X,Yp"`**, KHÔNG mở cả file.

- **Ranh giới:** <VD "frontend chỉ trình bày, business logic ở đâu" — điền theo kiến trúc thật của dự án>.
- **Số P-index** đánh theo `P<nhóm>.<số>`. 3 lớp đồng bộ: chỉ mục dưới đây → tag `// Px.y` trong code → `.ai/FEATURE_MAP.md`.

## Nhóm (đề xuất mẫu — sửa lại theo domain dự án thật rồi xoá dòng này)

| Nhóm | Phạm vi |
| :--- | :--- |
| **P1** | Khung/hạ tầng — bootstrap, auth, cấu hình chung |
| **P2** | Quản trị (admin/dashboard) |
| **P3** | Front-end — trang người dùng cuối |
| **P4** | Xác thực & phân quyền |
| **P5** | Tính năng phụ trợ |
| **P6** | Cross-cutting — SEO, hiệu năng, bảo mật |

## Chỉ mục P-index (chức năng → tra chi tiết ở `.ai/FEATURE_MAP.md`)

| P | Chức năng | Chi tiết |
| :--- | :--- | :--- |
| `P1.1` | <VD: Bootstrap ứng dụng> | `.ai/FEATURE_MAP.md` → `### P1.1` |

> Xoá dòng mẫu trên khi seed số đầu tiên thật. Mỗi số CHỈ 1 dòng — không viết số đo/bẫy/lịch sử vào đây.

## Khi cần thêm

- **Script đo** (nếu dự án có UI): `docs/measure/README.md`.
- **Quyết định kiến trúc (tại sao chọn cách này)**: `docs/decisions/`.
- **Nhật ký theo phiên**: `.ai/WORKLOG.md` §2.
- **Checklist deploy**: `docs/runbook-deploy.md`.
