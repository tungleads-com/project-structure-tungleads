# Chuẩn cấu trúc tài liệu dự án — áp dụng cho mọi dự án mới

> Đúc kết từ 2 dự án thật: `TLA Theme` (tungleads-theme-cp — 2 model claude/deepseek chạy tuần tự,
> đã tối ưu CLAUDE.md 131KB → 6.9KB) và `web-video-learning` (Laravel Boost — bằng chứng sống cho
> việc KHÔNG rotate WORKLOG sẽ phình tới 214KB/1.586 dòng không kiểm soát được).
> **Version: v1.4** (chốt 2026-10-16) · **Lịch sử sửa: `CHANGELOG.md`** (cùng thư mục) — mỗi lần sửa file này:
> bump version (**PATCH** = sửa câu chữ · **MINOR** = thêm/sửa quy tắc, đổi hạn mức · **MAJOR** = đổi nguyên tắc nền)
> rồi ghi **1 dòng** vào CHANGELOG. Dự án áp chuẩn thì ghi `**Chuẩn áp dụng:** … — vX.Y` trong `AGENTS.md`,
> và mọi chỗ **lệch chuẩn** phải khai báo kèm **số đo + lý do + trigger xem lại**.
> File này được `~/.claude/CLAUDE.md` trỏ tới — không lặp lại nội dung ở đó.
> ⚠️ Chỗ trỏ đó phải là **TRỎ** (nhắc đường dẫn), **KHÔNG `@import`** — kẻo nạp thêm ~2,9KB mỗi phiên cho MỌI dự án.

## Cây thư mục

```
<project-root>/
├── CLAUDE.md        ≤8KB PHẦN VIẾT TAY  — CHỈ MỤC (auto-nạp mọi phiên) — 1 dòng/số P-index → FEATURE_MAP.
│                          Dự án dùng tool tự sinh guideline (Laravel Boost…): GIỮ NGUYÊN khối tool ghi,
│                          KHÔNG di dời (xem mục "Khối tool tự sinh guideline" bên dưới). Hạn mức 8KB chỉ tính
│                          PHẦN VIẾT TAY; khối tool ĐO RIÊNG và GHI số token vào AGENTS.md (> ~3.000 token ⇒
│                          phải xử lý bằng config/tắt/ghi ngoại lệ — xem mục dưới).
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
| **Tag code → số + tầng** | `// [Px.y][FE]` · `[BE]` · `[DB]` (CSS/JS: `/* [Px.y][FE] */`) ở entry point: route, controller/handler, model chính, page/component gốc. Tra 1 tầng: `grep -rn "\[Px.y\]\[BE\]"`; tra cả chức năng: `grep -rn "\[Px.y\]"`. **Định dạng DUY NHẤT cho dự án mới** (chủ dự án chốt 2026-10-12; `CLAUDE.md`/`AGENTS.md` mẫu đã khớp). Dự án đang chạy giữ tag riêng (VD TLA Theme `// CPx.y`, `TTHNx.y`), KHÔNG retrofit, khai báo định dạng trong `CLAUDE.md` dự án. |
| **Tối ưu token/phiên** | Chỉ `CLAUDE.md` tự nạp mỗi phiên (≤8KB phần viết tay); mọi file còn lại đọc theo yêu cầu bằng `grep -n` + `sed -n`, không `cat` cả file. |
| **Multi-model an toàn** | Chạy TUẦN TỰ, không song song. Nhãn commit kèm model: `feat(P3.5)[claude]: ...`. §1 đang ghi việc dang dở của model khác → không tự sửa tiếp file đó, hỏi người dùng trước. |
| **LOCK đa model (soft lock)** | Trường `LOCK:` ở đầu §1 WORKLOG ghi rõ model nào đang giữ / trống — nhìn phát biết ngay, không phải đọc văn xuôi để suy luận. ⚠️ Đây là **khoá quy ước**, KHÔNG phải khoá hệ thống file thật — không chặn ghi song song bằng cơ chế OS, chỉ giúp agent tự giác tuân theo. |
| **Sửa 1 số đã có** | PHẢI `grep` mục `FEATURE_MAP.md` tương ứng trước khi code — nhiều quyết định đã chốt sau khi đo (kích thước, màu, hành vi cụ thể) không được tự ý revert chỉ vì không thấy ghi ở `CLAUDE.md`. |
| **Ngân sách token/phiên** | **Phần do dự án VIẾT**: mục tiêu ≤ **~6.000 token** = `CLAUDE.md` (phần viết tay) + `AGENTS.md` + `WORKLOG §1` + 2–3 dòng §2 cuối (đo thật trên TLA sau tối ưu: ~5.980). **Khối tool tự sinh đo RIÊNG** và ghi số vào `AGENTS.md` (mục “Khối tool tự sinh”: > ~3.000 token ⇒ bắt buộc xử lý hoặc ghi ngoại lệ). Thực tế 6–8k vẫn chấp nhận được — **nhưng phải GHI số đo**, cấm vượt mà không ghi. Kiểm 1 lệnh: `wc -c CLAUDE.md AGENTS.md .ai/WORKLOG.md .ai/FEATURE_MAP.md`. Nghi trùng lặp ⇒ quét cụm 8 từ giữa các file (≥5% là có mùi). |
| **Không nhân bản skill/lệnh** | 1 skill / 1 lệnh chỉ có **1 bản thật**; tool khác cần chỗ khác ⇒ **symlink** (`ln -s ../.claude/skills .agents/skills`), **cấm copy**. Bằng chứng đã dính: `web-video-learning` có `.claude/skills` 176KB **và** `.agents/skills` 176KB là 2 bản copy thật. |

## Khối tool tự sinh guideline (Laravel Boost, Cursor rules sync, Copilot instructions sync…)

Cơ chế chung của loại tool này: tìm **marker cố định** (`<!-- boost:start -->…`, `<laravel-boost-guidelines>`…)
rồi **ghi đè đúng khối đó** mỗi lần sync (cập nhật package, chạy lại lệnh cài).

**Luật:** **KHÔNG tay sửa · KHÔNG tay di dời · KHÔNG copy** khối này sang file khác. Làm vậy thì lần sync sau tool
sinh lại một bản mới tại chỗ cũ, còn bản đã dời thành **bản chết** ⇒ lệch dữ liệu âm thầm, vi phạm “1 sự thật 1 nhà”.

**Hạn mức 8KB của `CLAUDE.md` chỉ tính PHẦN VIẾT TAY** bên dưới khối tool — **khối tool KHÔNG tính vào hạn mức này**
(quyết định của chủ dự án: không đánh nhau với tool). Nhưng khối tool **không được “vô hình” về token**:

- **Đo riêng và ghi con số vào bảng hạn mức của `AGENTS.md`** (byte + ~token). Ví dụ thật: `khối Laravel Boost =
  11.686 B ≈ 3.892 token` (đo 2026-09-18 trên `web-video-learning`; phần viết tay của file đó = 7.236 B ≈ 2.029 token).
- **Ngưỡng hành động: khối tool > ~3.000 token (~9 KB)** ⇒ phải làm **1 trong 3**, không được im lặng:
  (a) đổi config để tách/loại bớt, (b) tắt hẳn tính năng guideline, (c) ghi **ngoại lệ có lý do + số đo** ngay trong
  `AGENTS.md` (coi như một khoản ngân sách đã được duyệt, không phải thứ bỏ quên).

**Muốn giảm token do khối tool ⇒ làm bằng CONFIG, không bằng tay:**

1. Kiểm tool có khoá config không: `grep -rn "guidelines_path\|guidelines\|exclude\|rules" vendor/<tool>/config/*.php`
   (đã kiểm Laravel Boost: `boost.agents.claude_code.guidelines_path` ⇒ **đích ghi là CONFIG**, `CLAUDE.md` chỉ là
   *giá trị mặc định*; thêm `BOOST_RULES_SCOPED_GUIDELINES=true` ⇒ tool **tự tách guideline theo path ra `.ai/rules/boost/`**;
   `boost.guidelines.exclude` ⇒ bỏ pack không dùng).
2. Tool **không** có khoá nào ⇒ chọn: (a) **đo rồi chấp nhận** + ghi số token vào bảng hạn mức của `AGENTS.md`, hoặc
   (b) tắt hẳn tính năng guideline nếu model không cần nữa.
3. **Chứng minh bằng test, không bằng suy luận:** `shasum <file>` → chạy sync → `shasum` lại → `diff`; **chạy 2 lần**
   để chắc tool không sinh bản thứ hai ở nơi khác.

## Cấu hình Claude Code theo dự án (skills · hook · plugin · MCP)

**Nguyên tắc:** tạo khi dự án THẬT SỰ cần, không tạo thư mục rỗng. Mỗi thứ chỉ có **1 nhà**, nằm trong repo dự án dùng nó.

| Loại | Vị trí trong repo dự án | Luật |
| :--- | :--- | :--- |
| Permission · hook · plugin bật cho dự án | `.claude/settings.json` (commit) | Template có sẵn bản tối thiểu chặn đọc `.env*`/`secrets/`. Cá nhân từng máy → `.claude/settings.local.json` (gitignore). |
| Skill riêng dự án | `.claude/skills/<tên>/SKILL.md` | 1 bản thật; tool khác cần thì symlink (xem "Không nhân bản skill"). Không dùng chung skill giữa dự án khách hàng. |
| MCP riêng dự án | `.mcp.json` ở root | **Cấm secret** trong file — chỉ dùng biến môi trường `${VAR}`, khai tên biến trong `.env.example`. |
| Subagent · slash command | `.claude/agents/` · `.claude/commands/` | Tạo khi cần. |
| Script hook | `.claude/hooks/*.sh` (gọi bằng `${CLAUDE_PROJECT_DIR}/.claude/hooks/…`) | Hook chạy lệnh thật trên máy: clone repo lạ thì đọc hook trước khi mở trust. |

- Thêm plugin/MCP/hook vào dự án ⇒ ghi **1 dòng lý do** vào `AGENTS.md` (hoặc `.ai/rules/`), để biết vì sao có và khi nào gỡ.
- `enabledPlugins` trong `settings.json` chỉ *khai báo*, không cài hộ — người clone vẫn phải tự cài plugin.
- Thứ dùng chung mọi dự án (kỹ năng cá nhân, MCP cá nhân) ở `~/.claude/`, không chép vào repo dự án.

## Một repo hay nhiều repo

- Mặc định **1 dự án = 1 repo** và **có remote** (⇒ backup, PR, review). Chỉ tách khi vận hành buộc
  (WordPress parent/child/plugin, monorepo nhiều service…).
- Khi tách: (1) ghi **map repo** trong `README.md` của repo gốc (repo nào giữ gì); (2) **mỗi repo có
  `AGENTS.md` + `CLAUDE.md` riêng** và sự thật của repo nào nằm ở repo đó — **không** để “sự thật ở root, code ở con”;
  (3) kết thúc phiên phải kiểm `git status` **cả nhóm repo**; (4) `AGENTS.md` của repo con ghi rõ **thứ tự commit
  khi deploy** (VD plugin → parent → child → root).

## Áp chuẩn cho dự án có sẵn `CLAUDE.md`/`AGENTS.md` riêng

Dự án mới từ template không xung đột (chỉ có placeholder). Mục này cho dự án **đã chạy** (hoặc có file tool sinh) muốn áp chuẩn. Làm **một lần**, trên **branch riêng** (`chore/ap-chuan-vX.Y`), không xoá thẳng — git history là bản sao lưu.

1. **Kiểm kê:** liệt kê từng luật trong `CLAUDE.md`/`AGENTS.md`/tài liệu hiện có, xếp vào 1 trong 3 nhóm:

   | Nhóm | Xử lý |
   | :--- | :--- |
   | Trùng với chuẩn (làn A/B/C, đính chính, hạn mức…) | Bỏ bản của dự án, giữ bản của chuẩn |
   | Riêng dự án | Chuyển về đúng nhà: nghiệp vụ → `PRODUCT.md`/`FEATURE_MAP`; luật làm việc → mục "Luật bất biến" của `AGENTS.md`; lệnh → "Môi trường & lệnh chạy" |
   | Mâu thuẫn với chuẩn | Giữ, khai báo **lệch chuẩn** ngay cạnh dòng `Chuẩn áp dụng` kèm số đo + lý do + trigger xem lại |

2. **Ưu tiên:** luật riêng dự án chỉ thắng chuẩn khi đã khai báo lệch chuẩn. **Luật an toàn không dự án nào được nới lỏng** (không commit secret, hỏi trước khi xoá/migration, không deploy khi chưa được yêu cầu).
3. **Khối tool tự sinh** (Laravel Boost…): giữ nguyên tại chỗ, theo mục "Khối tool tự sinh guideline".
4. **Gắn tag + ghi version:** thêm `**Chuẩn áp dụng:** … — vX.Y` vào `AGENTS.md`; seed `FEATURE_MAP` cho các tính năng đã có (tag `[Px.y]` vào code theo quy tắc chuẩn, không retrofit đồng loạt).
5. **Kiểm sau gộp:** `wc -c CLAUDE.md AGENTS.md` đối chiếu hạn mức; quét trùng cụm 8 từ giữa các file (≥5% là có mùi); đối chiếu danh sách kiểm kê — không luật riêng nào mất.
6. **Duyệt:** chủ dự án xem diff trước khi merge (việc đụng nhiều file, có thể xoá nhầm luật trông giống luật chuẩn).

Chưa dùng marker `<!-- standard:start -->` để tự thay phần chuẩn khi nâng version: thêm khi số dự án tăng và việc nâng version thành thường xuyên.

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
