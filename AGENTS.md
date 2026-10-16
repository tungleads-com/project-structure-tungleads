# AGENTS.md — Hướng dẫn bắt buộc cho mọi AI agent làm việc trên repo này

**Repo:** <Tên dự án> — <mô tả ngắn>. <Ghi ranh giới kiến trúc nếu có, VD "child theme chỉ trình bày, business logic ở plugin X">.

**Chuẩn áp dụng:** [`project-structure-standard`](https://github.com/tungleads-com/project-structure-tungleads/blob/main/docs/project-structure-standard.md) (local: `~/.claude/docs/project-structure-standard.md`) — v1.4 <!-- ghi mọi chỗ lệch chuẩn kèm số đo + lý do + trigger xem lại -->

**Model chạy trên repo này:** <VD "chỉ 1 model (Claude Code)" hoặc "N model tuần tự: claude, deepseek, codex — KHÔNG bao giờ song song">.
<Nếu nhiều model: model sau chỉ bắt đầu khi model trước dừng hẳn và để lại nhật ký trong `.ai/WORKLOG.md`.
Nhãn commit chỉ được là tên model đã khai ở đây. Trước khi sửa: đọc `LOCK:` ở §1 WORKLOG — đang bị model khác giữ thì dừng, hỏi người dùng.>

**Quan hệ các file tài liệu (KHÔNG để trùng lặp):**
- **`AGENTS.md`** (file này) = luật làm việc duy nhất (checklist · làn A/B/C · sự thật/lịch sử · hạn mức · môi trường · kiểm chứng).
- **`CLAUDE.md`** = CHỈ MỤC (mỗi số 1 dòng, trỏ FEATURE_MAP). Tự nạp mỗi phiên ⇒ phải NHỎ, không viết chi tiết/quyết định/số đo vào đây.
- **`.ai/FEATURE_MAP.md`** = nơi DUY NHẤT chứa chi tiết kỹ thuật (quyết định đã chốt, số đo, bẫy, file thật). Chỉ đọc bằng `grep -n` + `sed -n`.
- **`.ai/WORKLOG.md`** *(nếu có)* = nhật ký (§1 ghi đè, §2 chỉ ghi thêm).

**Nguồn sự thật — phân biệt SỰ THẬT và LỊCH SỬ:**
- **SỰ THẬT HIỆN TẠI** = **§1 `.ai/WORKLOG.md`** *(nếu có)* + **`.ai/FEATURE_MAP.md`** (mục `### Px.y`). Hai chỗ này **ĐƯỢC PHÉP và PHẢI SỬA TẠI CHỖ** khi có gì đổi.
- **LỊCH SỬ** = **§2 `.ai/WORKLOG.md`** + `.ai/WORKLOG-archive-<mốc>.md`: **chỉ ghi thêm**, **không bao giờ là nguồn sự thật** (tra xong phải đối chiếu FEATURE_MAP trước khi dùng).
- **Khi phiên này phủ định điều đã ghi trước đó:** (1) sửa mục `### Px.y` trong FEATURE_MAP **tại chỗ**; (2) dòng §2 mới **mở đầu bằng `❌ ĐÍNH CHÍNH <ngày>:`**; (3) **THÊM nhãn** vào dòng cũ nếu gây hiểu nhầm — **chỉ THÊM, KHÔNG xoá/viết lại** nội dung dòng cũ (giữ audit).
- **Mẫu viết mục P trong FEATURE_MAP:** "**hiện tại là gì** → *trước <ngày>* là gì (nếu đã đổi)".

**Hạn mức tài liệu (kiểm `wc -c` trước khi commit — vượt thì CẮT hoặc TÁCH):**

| File | Hạn mức | Nếu vượt |
| :--- | :--- | :--- |
| `CLAUDE.md` | **≤ 8 KB** (phần viết tay; khối tool tự sinh nếu có không tính) | Bỏ chi tiết ⇒ chuyển sang `.ai/FEATURE_MAP.md` |
| `AGENTS.md` | **≤ 10 KB** | Bỏ ví dụ/diễn giải, giữ luật; tách chủ đề sang `.ai/rules/*.md` |
| `.ai/FEATURE_MAP.md` | Không giới hạn cứng, nhưng 1 mục >3KB → tách heading `### Px.y` riêng | — |
| 1 dòng §2 WORKLOG | **≤ 300 ký tự** | Rút còn "việc · file · trạng thái" |
| `.ai/WORKLOG.md` | Giữ ~10-20 mục/phiên gần nhất | Rotate nguyên văn sang `.ai/WORKLOG-archive-<mốc>.md` |

**Cấm chép lại nội dung giữa các file** — chỉ được **trỏ** (tên file + mục). Một sự thật chỉ có **một nhà**.

## Trước khi code (mỗi phiên)

1. Đọc `.ai/FEATURE_MAP.md` mục liên quan (`grep -n "^### Px.y"`) — có quyết định đã chốt thì KHÔNG tự ý revert.
2. *(Nếu có `.ai/WORKLOG.md`)* Đọc §1 + vài dòng cuối §2 + `git status` + `git log --oneline -5`.
3. Chọn làn thay đổi trước khi làm (bảng dưới).

## Làn thay đổi — chọn trước khi làm

| Làn | Khi nào | Kiểm chứng | Tài liệu | Báo cáo |
| :--- | :--- | :--- | :--- | :--- |
| **A — 1 thuộc tính** | Sửa nhỏ, không đổi cấu trúc/hành vi | Test/kiểm nhanh phần vừa sửa | 1 dòng §2 (nếu có WORKLOG), không đụng FEATURE_MAP | 1-2 dòng |
| **B — 1 khối** | 1 module/component, có logic/responsive | Test liên quan + kiểm biên | 1 dòng §2 + cập nhật mục `### Px.y` | 3-5 dòng |
| **C — tính năng/đổi mô hình** | Nhiều file, đổi cấu trúc, thêm UI/API | Đầy đủ + test E2E nếu có | Đồng bộ cả 3 lớp (CLAUDE/FEATURE_MAP/§1-§2) | Báo cáo có cấu trúc |

## Sau khi xong (trước khi dừng phiên)

1. Kiểm chứng phần vừa sửa (theo làn ở trên).
2. Đồng bộ: chỉ mục `CLAUDE.md` (chỉ khi có số P MỚI) → tag `// [Px.y][FE]` (hoặc `[BE]`/`[DB]`) trong code → chi tiết trong `.ai/FEATURE_MAP.md`.
3. *(Nếu có WORKLOG)* Ghi 1 dòng §2 + cập nhật §1 nếu còn việc dang dở.
4. Commit kèm P-index: `feat(P3.5): ...` (nhiều model: `feat(P3.5)[claude]: ...`).

## Môi trường & lệnh chạy

<Điền theo đúng stack dự án — VD:>
- **Port local:** lấy từ registry `~/.claude/docs/port-registry.md` (web `81NN`, DB `34NN`, phụ `82NN`) — đăng ký trước khi ghi vào `.env`/compose; không dùng port mặc định (8080, 3306, 3000, 8000…).
- Dev server: `<lệnh>`
- Test: `<lệnh>`
- Build: `<lệnh>`
- Lint/format: `<lệnh>`

## Kiểm chứng bắt buộc trước khi báo xong

<Điền theo loại dự án:>
- Dự án có UI: nêu cách đo (trình duyệt/breakpoint/screenshot...) — script tái dùng ở `docs/measure/`.
- Dự án API/backend: bộ test nào phải xanh trước khi báo hoàn thành.

## Luật bất biến

- Không xoá file/bảng dữ liệu, không chạy migration nguy hiểm, không deploy production khi chưa được yêu cầu rõ ràng.
- Không commit `.env`/secret. Không tự ý đổi cấu trúc thư mục đã tồn tại.
- <Thêm luật riêng của dự án nếu có>
