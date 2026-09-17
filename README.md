# AffWorth Skill — hỏi một câu, biết dự án affiliate có chạy ads được không

Skill cho Claude Code / agent bất kỳ: đưa vào một tên miền shop, trả về **hoa hồng mỗi đơn**,
**trần giá thầu hoà vốn**, **biên lợi nhuận**, và cảnh báo **shop cấm chạy quảng cáo trả tiền**.

Số liệu lấy từ [AffWorth](https://affworth.com?ref=gh-skill) — kho gần 48.000 chương trình affiliate
đã chấm sẵn, tra trực tiếp được cả tên miền chưa có trong kho.

## Cài đặt

```bash
git clone https://github.com/phamlinh1010/affworth-skill
cp -r affworth-skill/skills/affworth-check ~/.claude/skills/
```

Rồi trong Claude Code gõ: `/affworth-check bellroy.com`

## Nó trả về gì

| Trường | Nghĩa |
|---|---|
| `price` | giá đơn hàng trung bình của shop |
| `pct` | phần trăm hoa hồng |
| `hh` | tiền hoa hồng thực nhận mỗi đơn |
| `be` | trần giá thầu hoà vốn — trả hơn mức này là lỗ |
| `bien` | biên lợi nhuận ở giá thầu rẻ |
| `tos_ppc` | `banned` = điều khoản cấm chạy quảng cáo trả tiền |
| `cac_buoc` | từng bước máy đã làm và nguồn của mỗi số |

## Vì sao cần

Chạy Google Ads cho affiliate mà không biết trần giá thầu hoà vốn thì mỗi click là một lần đoán.
Tệ hơn: nhiều shop cấm chạy quảng cáo trả tiền trong điều khoản — chạy là mất tài khoản.

Xem bảng đầy đủ tại **[affworth.com](https://affworth.com?ref=gh-skill)** (miễn phí 100 dòng mỗi ngày, không cần tài khoản).

## Giấy phép
MIT
