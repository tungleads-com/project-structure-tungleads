# Chuẩn cấu trúc tài liệu dự án — áp dụng cho mọi dự án mới

> Đúc kết từ 2 dự án thật: `TLA Theme` (tungleads-theme-cp — 2 model claude/deepseek chạy tuần tự,
> đã tối ưu CLAUDE.md 131KB → 6.9KB) và `web-video-learning` (Laravel Boost — bằng chứng sống cho
> việc KHÔNG rotate WORKLOG sẽ phình tới 214KB/1.586 dòng không kiểm soát được).
> Bản 2026-09-18b — sau phản biện 2 chiều, sửa 6 điểm: lý do khối tool tự sinh (đích ghi là **CONFIG**,
> không phải “cố định”), tag tầng `[FE]/[BE]/[DB]`, làm rõ “CẤM narrative” ở FEATURE_MAP, **ngân sách
> token/phiên**, quy tắc **nhiều repo**, cấm **nhân bản skill/lệnh**.
> File này được `~/.claude/CLAUDE.md` trỏ tới — không lặp lại nội dung ở đó.
> ⚠️ Chỗ trỏ đó phải là **TRỎ** (nhắc đường dẫn), **KHÔNG `@import`** — kẻo nạp thêm ~2,9KB mỗi phiên cho MỌI dự án.

## Cây thư mục

```
<project-root>/
├── CLAUDE.md        ≤8KB PHẦN VIẾT TAY  — CHỈ MỤC (auto-nạp mọi phiên) — 1 dòng/số P-index → FEATURE_MAP.
│                          Dự án dùng tool tự sinh guideline (Laravel Boost…): GIỮ NGUYÊN khối tool ghi,
│                          KHÔNG di dời (xem "Vì sao không di dời" bên dưới). Hạn mức 8KB chỉ tính phần
│                          viết tay bên dưới khối tool — không tính khối tool tự sinh.
├── AGENTS.md        ≤10KB LUẬT DUY NHẤT: checklist đầu/cuối phiên · làn thay đổi A/B/C ·
│                          luật SỰ THẬT ↔ LỊCH SỬ · luật đính chính (❌ ĐÍNH CHÍNH <ngày>: …,
│                          chỉ THÊM nhãn, không xoá) · bảng hạn mức kích thước · môi trường & lệnh chạy ·
│                          quy tắc kiểm chứng bắt buộc trước khi báo xong · LOCK đa model (xem dưới) ·
│                          nhãn model khi commit
├── README.md              Cho người: cài đặt / chạy / deploy tóm tắt
├── PRODUCT.md             Nghiệp vụ · phạm vi · thuật ngữ                          (tuỳ dự án)
├── .ai/
│   ├── FEATURE_MAP.md     BẢNG TRA CỨU + nơi DUY NHẤT của "sự thật kỹ thuật hiện tại". 7 cột:
│   │                      | ID | Chức năng | FE (file) | BE (file) | DB | Test/đo | Trạng thái |
│   │                      Mục >3KB → tách heading `### Px.y` riêng bên dưới bảng chính.
│   │                      CẤM: kể chuyện theo phiên (ai làm gì, lúc nào) — việc đó của WORKLOG §2.
│   │                      PHẢI ghi: quyết định đã chốt · số đo thật · bẫy · file thật (mục `### Px.y`).
│   │                      Dòng đầu file: cảnh báo "chỉ đọc bằng grep -n + sed -n, không mở cả file".
│   ├── WORKLOG.md         §1 ĐANG LÀM — ghi đè mỗi phiên (LOCK + trạng thái + việc tiếp theo, ≤10 dòng)
│   │                      §2 NHẬT KÝ — chỉ ghi thêm, ≤20 dòng gần nhất, mỗi dòng ≤300 ký tự
│   │                      CHỈ tạo file này khi dự án nhiều model/nhiều phiên xen kẽ — dự án nhỏ 1 mình
│   │                      Claude làm liên tục thì bỏ qua để đỡ 1 lớp thủ tục thừa.
│   ├── WORKLOG-archive-<mốc>.md   BẮT BUỘC có cơ chế rotate ngay từ đầu, không có ngoại lệ (bằng chứng:
│   │                      web-video-learning không rotate → 214KB/1.586 dòng, mất kiểm soát).
│   │                      §2 vượt hạn mức → chuyển NGUYÊN VĂN các dòng cũ sang đây, dòng đầu file archive
│   │                      ghi rõ "chỉ tra cứu khi cần, không đọc khi bắt đầu phiên".
│   └── rules/             TUỲ CHỌN — chỉ tạo khi dự án đủ lớn/nhiều concern kỹ thuật khác nhau
│       ├── index.md       #   (VD Laravel: auth/models/routes/migrations/css/js riêng biệt).
│       ├── auth.md        #   index.md là ROUTER: khai glob pattern → file rule tương ứng.
│       ├── models.md      #   Mỗi file 1 chủ đề, ngắn (1–3KB). AGENTS.md TRỎ tới, không lặp nội dung.
│       └── ...             #   Dự án nhỏ/1 stack đơn giản → bỏ qua thư mục này, gộp vào AGENTS.md.
├── docs/
│   ├── measure/            Script đo tái sử dụng (Playwright/wp-cli/…) + README ý nghĩa từng script
│   ├── decisions/          ADR — TẠI SAO chọn cách này (không phải CÁI GÌ — đó là việc của FEATURE_MAP)  (tuỳ dự án)
│   └── runbook-deploy.md   Checklist deploy dạng đọc được độc lập — KHÔNG nhét trong script deploy
│                           (tránh lặp: script chỉ THỰC THI, docs mới là nơi THAM CHIẾU được bằng grep)
├── .github/ (tuỳ tool)     instructions/*.md (tự gắn theo glob) · skills/<tên>/SKILL.md · prompts/*.md
└── (mã nguồn theo ĐÚNG cấu trúc chuẩn của stack — không tự bịa lại cấu trúc mặc định của framework)
```

## Nguyên tắc xuyên suốt

| Nguyên tắc | Áp dụng |
| :--- | :--- |
| **1 sự thật 1 nhà** | Nội dung kỹ thuật chỉ xuất hiện ở ĐÚNG 1 file; chỗ khác chỉ TRỎ (tên file + mục), không copy. |
| **Sự thật vs Lịch sử** | Sự thật hiện tại = `CLAUDE.md` (nghĩa) + `FEATURE_MAP.md` (chi tiết, **sửa tại chỗ**) + `WORKLOG §1` (đang làm, **ghi đè**). Lịch sử = `WORKLOG §2` + archive (**chỉ ghi thêm**, không bao giờ là nguồn tra "hiện tại đúng là gì"). |
| **Đính chính không xoá** | Phiên sau phủ định điều phiên trước ghi → sửa `FEATURE_MAP` tại chỗ + dòng §2 mới bắt đầu bằng `❌ ĐÍNH CHÍNH <ngày>:` + dán nhãn vào dòng cũ nếu gây hiểu nhầm — chỉ THÊM nhãn, không xoá/viết lại nội dung dòng cũ (giữ audit trail). |
| **Tag code → số + tầng** | `// [Px.y][FE]` · `[BE]` · `[DB]` (CSS/JS: `/* [Px.y][FE] */`) ở entry point: route, controller/handler, model chính, page/component gốc. Tra 1 tầng: `grep -rn "\[Px.y\]\[BE\]"`; tra cả chức năng: `grep -rn "\[Px.y\]"`. ⚠️ **Đề xuất MỚI, chưa có bằng chứng thực tế** (khác các mục còn lại trong bảng này) — áp dụng cho **dự án mới**, KHÔNG bắt buộc gắn lại tag cũ ở dự án đang chạy (VD TLA Theme đang dùng `// CPx.y` trần, không cần retrofit). |
| **Tối ưu token/phiên** | Chỉ `CLAUDE.md` tự nạp mỗi phiên (≤8KB phần viết tay); mọi file còn lại đọc theo yêu cầu bằng `grep -n` + `sed -n`, không `cat` cả file. |
| **Multi-model an toàn** | Chạy TUẦN TỰ, không song song. Nhãn commit kèm model: `feat(P3.5)[claude]: ...`. §1 đang ghi việc dang dở của model khác → không tự sửa tiếp file đó, hỏi người dùng trước. |
| **LOCK đa model (soft lock)** | Trường `LOCK:` ở đầu §1 WORKLOG ghi rõ model nào đang giữ / trống — nhìn phát biết ngay, không phải đọc văn xuôi để suy luận. ⚠️ Đây là **khoá quy ước**, KHÔNG phải khoá hệ thống file thật — không chặn ghi song song bằng cơ chế OS, chỉ giúp agent tự giác tuân theo. |
| **Sửa 1 số đã có** | PHẢI `grep` mục `FEATURE_MAP.md` tương ứng trước khi code — nhiều quyết định đã chốt sau khi đo (kích thước, màu, hành vi cụ thể) không được tự ý revert chỉ vì không thấy ghi ở `CLAUDE.md`. |
| **Ngân sách token/phiên** | Cả phiên nạp ≤ **~6.000 token** = `CLAUDE.md` + `AGENTS.md` + `WORKLOG §1` + 2–3 dòng §2 cuối (đo thật trên TLA sau tối ưu: ~5.980). Kiểm 1 lệnh: `wc -c CLAUDE.md AGENTS.md .ai/WORKLOG.md .ai/FEATURE_MAP.md`. Nghi trùng lặp ⇒ quét cụm 8 từ giữa các file (≥5% là có mùi). |
| **Không nhân bản skill/lệnh** | 1 skill / 1 lệnh chỉ có **1 bản thật**; tool khác cần chỗ khác ⇒ **symlink** (`ln -s ../.claude/skills .agents/skills`), **cấm copy**. Bằng chứng đã dính: `web-video-learning` có `.claude/skills` 176KB **và** `.agents/skills` 176KB là 2 bản copy thật. |

## Khối tool tự sinh guideline (Laravel Boost, Cursor rules sync, Copilot instructions sync…)

Cơ chế chung của loại tool này: tìm **marker cố định** (`<!-- boost:start -->…`, `<laravel-boost-guidelines>`…)
rồi **ghi đè đúng khối đó** mỗi lần sync (cập nhật package, chạy lại lệnh cài).

**Luật:** **KHÔNG tay sửa · KHÔNG tay di dời · KHÔNG copy** khối này sang file khác. Làm vậy thì lần sync sau tool
sinh lại một bản mới tại chỗ cũ, còn bản đã dời thành **bản chết** ⇒ lệch dữ liệu âm thầm, vi phạm “1 sự thật 1 nhà”.

**Hạn mức 8KB của `CLAUDE.md` chỉ tính PHẦN VIẾT TAY** bên dưới khối tool — **khối tool không tính** (quyết định của
chủ dự án: không đánh nhau với tool).

**Muốn giảm token do khối tool ⇒ làm bằng CONFIG, không bằng tay:**

1. Kiểm tool có khoá config không: `grep -rn "guidelines_path\|guidelines\|exclude\|rules" vendor/<tool>/config/*.php`
   (đã kiểm Laravel Boost: `boost.agents.claude_code.guidelines_path` ⇒ **đích ghi là CONFIG**, `CLAUDE.md` chỉ là
   *giá trị mặc định*; thêm `BOOST_RULES_SCOPED_GUIDELINES=true` ⇒ tool **tự tách guideline theo path ra `.ai/rules/boost/`**;
   `boost.guidelines.exclude` ⇒ bỏ pack không dùng).
2. Tool **không** có khoá nào ⇒ chọn: (a) **đo rồi chấp nhận** + ghi số token vào bảng hạn mức của `AGENTS.md`, hoặc
   (b) tắt hẳn tính năng guideline nếu model không cần nữa.
3. **Chứng minh bằng test, không bằng suy luận:** `shasum <file>` → chạy sync → `shasum` lại → `diff`; **chạy 2 lần**
   để chắc tool không sinh bản thứ hai ở nơi khác.

## Một repo hay nhiều repo

- Mặc định **1 dự án = 1 repo** và **có remote** (⇒ backup, PR, review). Chỉ tách khi vận hành buộc
  (WordPress parent/child/plugin, monorepo nhiều service…).
- Khi tách: (1) ghi **map repo** trong `README.md` của repo gốc (repo nào giữ gì); (2) **mỗi repo có
  `AGENTS.md` + `CLAUDE.md` riêng** và sự thật của repo nào nằm ở repo đó — **không** để “sự thật ở root, code ở con”;
  (3) kết thúc phiên phải kiểm `git status` **cả nhóm repo**; (4) `AGENTS.md` của repo con ghi rõ **thứ tự commit
  khi deploy** (VD plugin → parent → child → root).

## Khởi tạo dự án mới

0. **Tệp nền tối thiểu (mọi dự án):** `.gitignore` · `.editorconfig` · `.env.example` — **không bao giờ commit** `.env`/file nhạy cảm.
1. Dự án đủ phức tạp cần P-index (không áp cho script 1 file/prototype/landing tĩnh — hỏi trước khi áp máy móc):
   - Đề xuất bộ nhóm P-index (VD `P2` quản trị · `P3` front-end · `P4` xác thực · `P5` phụ trợ · `P6` cross-cutting) → chờ duyệt → seed.
   - Tạo `CLAUDE.md` (chỉ mục) + `AGENTS.md` (luật) + `.ai/FEATURE_MAP.md` (bảng tra cứu 7 cột, có cảnh báo grep-only từ lúc tạo).
   - Chỉ tạo `.ai/WORKLOG.md` khi dự án nhiều model/nhiều phiên xen kẽ.
   - Chỉ tạo `.ai/rules/` khi dự án đủ lớn/nhiều concern kỹ thuật khác nhau.
2. **Lệnh kiểm chứng theo stack** (VD `php artisan test --compact`, `npm test`, `npx playwright test`) → ghi vào `AGENTS.md`
   mục “kiểm chứng bắt buộc”. Dự án có UI ⇒ tạo `docs/measure/` + `docs/measure/README.md` (ý nghĩa từng script đo).
3. **Commit đầu:** `chore: khung dự án chuẩn (AGENTS/CLAUDE/.ai)` — nội dung commit ghi rõ đã tạo những file nào.
4. Commit sau kèm P-index: `feat(P3.5): ...` (dự án nhiều AI: `feat(P3.5)[claude]: ...`).
5. **Dự án nhỏ** (script 1 file, landing tĩnh, 1 model làm liên tục) ⇒ bỏ `.ai/WORKLOG.md`, `.ai/rules/`, `docs/measure/`,
   `docs/decisions/`; giữ `AGENTS.md` + `CLAUDE.md` + `README.md` là đủ.
