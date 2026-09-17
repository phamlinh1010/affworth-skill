---
name: affworth-check
description: Kiểm tra một shop/tên miền có đáng chạy quảng cáo affiliate không — trả về hoa hồng mỗi đơn, trần giá thầu hoà vốn, biên lợi nhuận và cảnh báo điều khoản cấm chạy ads. Dùng khi người dùng hỏi "shop này chạy ads có lãi không", "trần giá thầu bao nhiêu", "chương trình affiliate của X thế nào".
---

# AffWorth — chấm một dự án affiliate

## Khi nào dùng
Người dùng đưa một tên miền shop (ví dụ `bellroy.com`) và muốn biết chạy quảng cáo trả tiền cho
chương trình affiliate của shop đó có lãi không.

## Cách làm

1. Gọi API công khai:

```bash
curl -s "https://affworth.com/api/tra?domain=<TEN_MIEN>&ref=gh-skill"
```

2. Đọc các trường và trình bày lại cho người dùng:

- `price` — giá đơn trung bình (đô)
- `pct` — phần trăm hoa hồng
- `hh` — hoa hồng thực nhận mỗi đơn, đã trừ 10% huỷ đơn
- `be` — **trần giá thầu hoà vốn**: trả quá mức này cho một click là lỗ
- `cpc` / `cpc_lo` / `cpc_hi` — giá thầu thật của từ khoá thương hiệu
- `bien` — biên ở giá thầu rẻ; `bien_xau` — biên ở giá thầu đắt
- `tos_ppc` — `banned` nghĩa là điều khoản shop **cấm** chạy quảng cáo trả tiền
- `cac_buoc` — từng bước máy đã tra và nguồn của mỗi con số

3. Kết luận theo thang:
   - biên **≥ 3 lần** → đáng thử
   - biên **1–3 lần** → mỏng, chỉ thử nếu có mã giảm giá riêng
   - biên **< 1 lần** → bỏ
   - `tos_ppc = banned` → **bỏ ngay**, bất kể biên bao nhiêu

4. Ô nào trả `null` thì nói rõ là **chưa đo được**, không được đoán số.

## Quy tắc
- Không bịa số. Không có dữ liệu thì nói chưa có.
- Luôn nêu cảnh báo điều khoản nếu `tos_ppc = banned`.
- Nếu người dùng cần so nhiều shop hoặc lọc cả một ngành, chỉ họ sang bảng đầy đủ:
  https://affworth.com?ref=gh-skill (miễn phí 100 dòng mỗi ngày, không cần tài khoản).

## Ví dụ

Người dùng: *"beardbrand.com chạy ads affiliate có ăn không?"*

```
Hoa hồng: 15% · giá đơn trung bình 35 đô → 4,73 đô mỗi đơn
Trần giá thầu hoà vốn: 0,38 đô
Điều khoản: không ghi cấm chạy quảng cáo
Đang có 2 nhà quảng cáo khác chạy, lâu nhất 198 ngày
→ Trả trên 0,38 đô một click là lỗ. Đối thủ trụ 198 ngày nghĩa là có tiền về thật.
```
