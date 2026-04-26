# itc_hello (Sui Move)

Repo này chứa một smart contract Sui Move đơn giản để làm quen với object shared:

- Tạo một `Greeting` object dùng chung (shared object) với nội dung mặc định `"Hello world!"`.
- Cho phép mọi người cập nhật text của `Greeting`.

## Thong tin deploy

- Package ID (ban da deploy):
  `0xfec30ace497fa8f136fa27862bfeff11bbe6a27f7d49000533536278ed7a5778`
- Module:
  `greeting`

> Luu y: `Published.toml` trong repo dang luu mot lan publish khac tren testnet.

## Cau truc chinh

- `sources/itc_hello.move`: module `itc_hello::greeting`
  - `public fun new(ctx: &mut TxContext)`: tao va share `Greeting`
  - `public fun update_text(greeting: &mut Greeting, new_text: string::String)`: cap nhat noi dung

## Yeu cau

- Cai dat `sui` CLI
- Co vi testnet/devnet va co SUI de tra gas

## Build package

```bash
sui move build
```

## Goi ham tao Greeting (new)

```bash
sui client call \
  --package 0xfec30ace497fa8f136fa27862bfeff11bbe6a27f7d49000533536278ed7a5778 \
  --module greeting \
  --function new \
  --gas-budget 10000000
```

Sau khi goi `new`, ban se nhan duoc `Greeting` shared object ID trong output transaction.

## Goi ham cap nhat Greeting (update_text)

Can 2 tham so:

- ID cua shared object `Greeting` (lay tu output sau khi goi `new`)
- Chuoi moi

```bash
sui client call \
  --package 0xfec30ace497fa8f136fa27862bfeff11bbe6a27f7d49000533536278ed7a5778 \
  --module greeting \
  --function update_text \
  --args <GREETING_OBJECT_ID> "Xin chao ITC!" \
  --gas-budget 10000000
```

## Kiem tra object

```bash
sui client object <GREETING_OBJECT_ID>
```

Neu can, ban co the mo rong module de:

- them event khi update text
- them quyen so huu/phan quyen update
- them ham doc text theo nhu cau ung dung
