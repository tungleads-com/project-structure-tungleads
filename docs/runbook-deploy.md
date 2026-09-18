# Runbook — Deploy production

> Checklist đọc được độc lập (không nhét trong script deploy) — script chỉ THỰC THI, file này để THAM CHIẾU bằng `grep`.

## Trước khi đẩy

1. Backup DB (nếu có thay đổi schema/data).
2. `git status` sạch, đã test local xanh.
3. Xác nhận người yêu cầu deploy rõ ràng — không tự ý deploy khi "đã xong việc".

## Các bước

1. <VD: rsync/push code>
2. <VD: chạy migration>
3. <VD: clear cache>
4. <VD: restart service>

## Sau khi đẩy

1. Smoke test các trang/luồng chính.
2. Cập nhật `.ai/WORKLOG.md` §1 (nếu dự án dùng) — trạng thái deploy mới nhất.

## Rollback

<Cách quay lại bản trước nếu deploy hỏng>
