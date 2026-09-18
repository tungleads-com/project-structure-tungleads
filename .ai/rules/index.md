# Rules index — router glob → rule file

> Chỉ tạo thư mục `.ai/rules/` khi dự án đủ lớn/nhiều concern kỹ thuật khác nhau
> (VD backend nhiều domain, frontend riêng, migration riêng). Dự án nhỏ → gộp hết vào `AGENTS.md`, xoá thư mục này.

Trước khi sửa 1 file, đọc rule nào có glob khớp đường dẫn file đó, đọc đầy đủ trước khi code.

| Glob | Rule file | Nội dung |
| :--- | :--- | :--- |
| `<VD: app/Models/**>` | `models.md` | <VD: quy ước đặt tên, quan hệ, không SoftDeletes trừ khi...> |

Xoá dòng mẫu trên khi thêm rule thật đầu tiên.
