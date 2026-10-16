# Project Structure Template

Repo mẫu chuẩn cấu trúc tài liệu cho dự án làm việc với Claude Code (và các AI agent khác) —
đúc kết từ 2 dự án thật (WordPress multi-model, Laravel Boost), đã kiểm chứng bằng chứng
đo được (không suy đoán). Chi tiết lý do từng quyết định: `docs/decisions/0001-tai-sao-cau-truc-nay.md`.

## Dùng template này cho dự án mới

1. Clone/dùng nút "Use this template" trên GitHub.
2. Thay `<Tên dự án>` + các chỗ `<…>` trong `CLAUDE.md`, `AGENTS.md`, `.ai/FEATURE_MAP.md`, `.ai/WORKLOG.md`, ngày ở ADR-0001; viết lại `README.md` này thành README thật của dự án.
   Kiểm: `grep -rn "<[^>]*>" CLAUDE.md AGENTS.md .ai docs` — còn gì thì là chưa điền (bỏ qua chú thích trong `<!-- -->`).
3. Xoá phần không cần theo quy mô dự án (xem bảng "Khi nào cần file nào" bên dưới) — **đừng giữ file
   rỗng không dùng tới, chỉ làm rối repo**. Riêng `docs/project-structure-standard.md` + `docs/CHANGELOG.md`
   và `docs/lessons.md` là của repo mẫu: **xoá khỏi dự án con**; `AGENTS.md`/ADR-0001 đã có link tới repo mẫu,
   chỉ cần giữ `**Chuẩn áp dụng:** … — vX.Y`.
4. Đề xuất bộ nhóm P-index phù hợp domain dự án (thay bảng mẫu trong `CLAUDE.md`) → người dùng duyệt
   → bắt đầu seed số đầu tiên.
5. Điền `AGENTS.md` mục "Môi trường & lệnh chạy" theo đúng stack (Laravel/Next.js/WordPress...).

## Cây thư mục

```
.
├── CLAUDE.md                 ≤8KB — CHỈ MỤC (auto-nạp mọi phiên). 1 dòng/số P-index → FEATURE_MAP.
├── AGENTS.md                 ≤10KB — LUẬT DUY NHẤT: checklist · làn A/B/C · sự thật/lịch sử ·
│                              đính chính · hạn mức · môi trường & lệnh chạy · kiểm chứng bắt buộc.
├── README.md                 File này — cách dùng template, sau khi seed thì đổi thành README thật.
├── PRODUCT.md                 Nghiệp vụ · phạm vi · thuật ngữ                        (tuỳ dự án)
├── .ai/
│   ├── FEATURE_MAP.md        BẢNG TRA CỨU + nơi DUY NHẤT của sự thật kỹ thuật hiện tại.
│   ├── WORKLOG.md             §1 (ghi đè) + §2 (chỉ ghi thêm, ≤20 dòng)     (chỉ multi-model/multi-phiên)
│   └── rules/                 index.md (router glob→rule) + rule theo chủ đề          (tuỳ quy mô)
├── docs/
│   ├── measure/                Script đo tái dùng + README ý nghĩa từng script         (có UI)
│   ├── project-structure-standard.md + CHANGELOG.md   Chuẩn gốc (chỉ có ở repo mẫu)
│   ├── lessons.md                Bài học từ dự án thật → đầu vào để nâng version chuẩn (chỉ có ở repo mẫu)
│   ├── decisions/               ADR — TẠI SAO chọn cách này                            (tuỳ dự án)
│   └── runbook-deploy.md        Checklist deploy đọc độc lập, không nhét trong script
├── .gitignore
├── .editorconfig
└── .env.example
```

## Khi nào cần file nào

| File/thư mục | Bắt buộc? | Bỏ qua khi nào |
| :--- | :--- | :--- |
| `CLAUDE.md`, `AGENTS.md`, `.ai/FEATURE_MAP.md` | Luôn cần (trừ dự án siêu nhỏ) | Script 1 file, prototype nhanh |
| `.ai/WORKLOG.md` + archive | Chỉ khi nhiều model/nhiều phiên xen kẽ | 1 mình Claude làm liên tục |
| `.ai/rules/` | Chỉ khi dự án nhiều concern kỹ thuật khác nhau | Dự án nhỏ/1 stack đơn giản — gộp vào `AGENTS.md` |
| `docs/decisions/` (ADR) | Tuỳ dự án | Dự án không có quyết định kiến trúc gây tranh cãi |
| `docs/measure/` | Chỉ dự án có UI cần đo/kiểm chứng | Dự án backend/API thuần |
| `PRODUCT.md` | Tuỳ dự án | Dự án nội bộ nhỏ, nghiệp vụ đơn giản |

Chuẩn đầy đủ (nguyên tắc, bảng hạn mức, luật chống trùng lặp, lý do từng quyết định):
[`project-structure-standard.md`](docs/project-structure-standard.md) — bản gốc do Claude Code duy trì,
đồng bộ với `~/.claude/docs/project-structure-standard.md` của chủ dự án.

## Phản hồi ngược về chuẩn

Bài học rút ra từ dự án thật ghi **thẳng vào repo mẫu này** (clone local: `/Volumes/DATA/Claude-Code/project-structure-tungleads`),
không ghi ở repo dự án con: thêm 1 mục vào `docs/lessons.md` → khi chốt sửa chuẩn thì bump version, ghi `docs/CHANGELOG.md`,
gắn tag `vX.Y`.
