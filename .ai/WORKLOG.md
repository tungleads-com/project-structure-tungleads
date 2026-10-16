# WORKLOG — <Tên dự án>

> Chỉ tạo/dùng file này khi dự án có **nhiều model hoặc nhiều phiên xen kẽ nhiều ngày**.
> Dự án nhỏ 1 mình Claude làm liên tục → xoá file này, bỏ qua để đỡ 1 lớp thủ tục thừa.

- Model nào làm xong 1 phiên → cập nhật §1 + thêm 1 dòng vào §2 trước khi dừng.
- Model mới bắt đầu → đọc §1 + 10 dòng cuối §2 + `git status` + `git log --oneline -5`.
- §1 **ghi đè** (chỉ giữ khối mới nhất, đây là SỰ THẬT hiện tại — xem `AGENTS.md`) · §2 **chỉ ghi thêm** (LỊCH SỬ, không phải nguồn tra "hiện tại đúng là gì").
- Phủ định điều đã ghi trước → dòng §2 mới bắt đầu bằng `❌ ĐÍNH CHÍNH <ngày>:` + sửa `FEATURE_MAP.md` tại chỗ (xem luật ở `AGENTS.md`).
- §2 vượt ~20 dòng gần nhất → rotate nguyên văn các dòng cũ sang `.ai/WORKLOG-archive-<mốc>.md`.

## §1 ĐANG LÀM (bàn giao — ghi đè mỗi phiên, chỉ giữ 1 khối)

- **LOCK:** trống <!-- hoặc tên model đang giữ (claude/deepseek/codex); khoá quy ước, không phải khoá hệ thống -->
- **Model:** —
- **Việc đang làm / vừa xong:** —
- **File đã/sẽ chạm:** —
- **Việc tiếp theo:** —

## §2 NHẬT KÝ (chỉ ghi thêm, mới nhất ở dưới, mỗi dòng ≤300 ký tự)

| Ngày | Model | Việc | File | Trạng thái |
| :--- | :--- | :--- | :--- | :--- |
