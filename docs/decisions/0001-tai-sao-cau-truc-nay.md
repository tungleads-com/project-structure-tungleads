# ADR-0001: Vì sao dùng cấu trúc tài liệu này

**Ngày:** <điền ngày seed dự án> · **Trạng thái:** Chấp nhận

## Bối cảnh

Dự án dùng AI agent (Claude Code + có thể nhiều model khác) làm việc lặp lại nhiều phiên. Nếu không có
quy ước rõ ràng, tài liệu dự án dễ phình không kiểm soát (dẫn chứng thật: 1 dự án để `CLAUDE.md` phình
tới 131KB vì nhét cả nhật ký đo đạc vào bảng chỉ mục; 1 dự án khác để `WORKLOG.md` phình tới 214KB/1.586
dòng vì không có cơ chế rotate) — vừa tốn token mỗi phiên, vừa khó tra cứu.

## Quyết định

Áp dụng chuẩn cấu trúc tại `AGENTS.md`/`CLAUDE.md`/`.ai/FEATURE_MAP.md`/`.ai/WORKLOG.md` với:
- `CLAUDE.md` chỉ là chỉ mục (auto-nạp, phải nhỏ), chi tiết dồn về `FEATURE_MAP.md` (đọc theo yêu cầu).
- Tách bạch "sự thật hiện tại" (sửa tại chỗ) và "lịch sử" (chỉ ghi thêm, có rotate).
- Luật đính chính bằng nhãn, không xoá lịch sử — giữ audit trail cho việc nhiều model bàn giao chéo.

Chi tiết đầy đủ + bảng hạn mức: `~/.claude/docs/project-structure-standard.md` (chuẩn gốc, dùng chung
mọi dự án của chủ repo).

## Hệ quả

- (+) Token mỗi phiên thấp và ổn định theo thời gian, không tăng dần.
- (+) Audit trail đầy đủ khi nhiều model làm việc tuần tự.
- (-) Cần kỷ luật: mỗi lần sửa phải đúng đồng bộ 3 lớp, không tiện tay ghi tắt vào 1 chỗ.

## Ghi đè quyết định này

Không sửa/xoá ADR cũ — tạo `0002-...md` mới trỏ ngược lại ADR này nếu có thay đổi lớn về cấu trúc.
