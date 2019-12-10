# <a name="release_notes"></a>PoS API Release Notes

The Point of Sale API V10 will be in production **Q2 2020**. It will be released in SandProd **Q1 2020**.

# Changelog
## 2019-12-10
---
- Renamed subpage **Input Formats** to **Input and Output Formats**.
- Adjusted content of subpage **Input and Output Formats**
  - **HTTP Headers**
    - Renamed from `X-MP-\*` to `X-MobilePay-\*`.
    - Removed `X-MP-IntegratorId`.
  - **Payments**
    - Added `PlannedCaptureDelay`, `CustomerToken` and `CustomerReceiptToken`.
