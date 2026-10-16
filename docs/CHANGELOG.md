# CHANGELOG — Chuẩn cấu trúc tài liệu dự án

**Quy ước bump** (áp cho `project-structure-standard.md`):

| Loại | Khi nào | Bắt buộc |
| :--- | :--- | :--- |
| **PATCH** `v1.0.1` | sửa câu chữ/chính tả, **không đổi nghĩa** | 1 dòng dưới |
| **MINOR** `v1.1` | **thêm/sửa quy tắc** hoặc **đổi hạn mức** | 1 dòng (sửa gì · vì sao); dự án **không buộc** nâng ngay — nâng khi phiên chạm phần liên quan |
| **MAJOR** `v2.0` | đổi **nguyên tắc nền**: cấu trúc thư mục · luật SỰ THẬT↔LỊCH SỬ · lock đa model · định dạng tag | thêm mục **“Ảnh hưởng”** (dự án nào đang pin bản cũ, cần làm gì) + **thông báo mọi dự án** + 1 phiên “đồng bộ chuẩn” |

Không dùng **ngày** làm version (ngày chỉ nằm trong file này). Mỗi dự án pin số version trong `AGENTS.md`
(`**Chuẩn áp dụng:** … — vX.Y`) và khai báo mọi chỗ lệch kèm số đo.

---

## v1.4 — 2026-10-16 · MINOR

- Thêm mục "Áp chuẩn cho dự án có sẵn `CLAUDE.md`/`AGENTS.md` riêng": quy trình gộp 1 lần trên branch (kiểm kê 3 nhóm trùng/riêng/mâu thuẫn, ưu tiên, luật an toàn không nới lỏng, kiểm sau gộp, chủ dự án duyệt diff). Chưa dùng marker tự thay phần chuẩn.

## v1.3 — 2026-10-16 · MINOR

- Thêm mục "Cấu hình Claude Code theo dự án" (settings/hook/plugin/skill/MCP: vị trí + luật, cấm secret trong `.mcp.json`). Template thêm `.claude/settings.json` tối thiểu (deny đọc `.env*`, `secrets/**`) và `.gitignore` chặn `.claude/settings.local.json`. Dự án đang chạy không buộc nâng ngay.

## v1.2 — 2026-10-16 · MINOR

- Template: thêm trường `LOCK:` vào `WORKLOG` §1 + nhắc kiểm LOCK trong `AGENTS.md` (chuẩn đã yêu cầu nhưng template thiếu); thêm dòng `Chuẩn áp dụng: … — vX.Y` vào `AGENTS.md` mẫu; thêm luật port local (registry) vào `AGENTS.md` + `.env.example`. `.gitignore` chặn `.env.*` (trừ `.env.example`). Dự án đang chạy không buộc nâng ngay.

## v1.1 — 2026-10-12 · MINOR

- Chốt tag `// [Px.y][FE|BE|DB]` là định dạng duy nhất cho dự án mới (trước đó standard ghi "đề xuất", `CLAUDE.md`/`AGENTS.md` mẫu ghi `// Px.y` trần → lệch). Sửa `CLAUDE.md` + `AGENTS.md` mẫu cho khớp. Dự án đang chạy không buộc nâng ngay.

## v1.0 — 2026-09-18 · bản chốt đầu tiên (bắt đầu có version)

Đúc kết từ 2 dự án thật (`TLA Theme` + `web-video-learning`), sau **phản biện 2 chiều** (Cline ↔ Claude Code):

1. **Khối tool tự sinh** (Laravel Boost / Cursor rules sync / Copilot instructions sync…): **KHÔNG tay sửa, KHÔNG di dời, KHÔNG copy**; hạn mức 8KB của `CLAUDE.md` **chỉ tính phần viết tay**; khối tool **đo riêng và ghi số (byte ≈ token) vào `AGENTS.md`**; **> ~3.000 token ⇒ bắt buộc** chọn 1 trong 3: đổi config · tắt tính năng · **ghi ngoại lệ có lý do + số đo** (không được im lặng). *Đính chính so với bản nháp:* đích ghi của Boost là **CONFIG** (`boost.agents.claude_code.guidelines_path`), không phải “đích cố định”; Boost còn có `BOOST_RULES_SCOPED_GUIDELINES` (tách guideline theo path ra `.ai/rules/boost/`) và `boost.guidelines.exclude`.
2. **Tag code có tầng**: `// [Px.y][FE]` · `[BE]` · `[DB]` (bản nháp chỉ có `// Px.y` ⇒ grep ra lẫn FE/BE).
3. **FEATURE_MAP**: làm rõ **CẤM kể chuyện theo phiên** nhưng **PHẢI ghi** quyết định · số đo · bẫy · file thật; bảng **7 cột có FE/BE/DB**; hàng > 3 KB ⇒ tách `### Px.y`.
4. **Ngân sách token/phiên**: phần **do dự án viết** ≤ ~6.000 token (mục tiêu; thực tế 6–8k chấp nhận được **nhưng phải ghi số đo**); khối tool đo riêng theo mục 1.
5. **Nhiều repo**: mặc định **1 dự án = 1 repo có remote**; khi buộc tách (WordPress parent/child/plugin…) ⇒ map repo ở repo gốc + **AGENTS/CLAUDE riêng từng repo** + kiểm `git status` **cả nhóm** + ghi thứ tự commit khi deploy.
6. **Cấm nhân bản skill/lệnh**: 1 bản thật, chỗ khác dùng **symlink** (bằng chứng: `web-video-learning` có `.claude/skills` **và** `.agents/skills` giống hệt, 176 KB × 2).
7. **“Khởi tạo dự án mới”** bổ sung: tệp nền (`.gitignore` · `.editorconfig` · `.env.example`) · **lệnh verify theo stack** · commit đầu · **mức bỏ bớt cho dự án nhỏ** (bỏ `.ai/WORKLOG.md`, `.ai/rules/`, `docs/measure/`, `docs/decisions/`).

**Trước v1.0:** chưa có versioning; file được sửa nhiều lần trong ngày 2026-09-18 (bản nội bộ gọi là “2026-09-18b”).
