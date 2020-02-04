# <a name="release_notes"></a>PoS API Release Notes

The Point of Sale API V10 will be in production **Q2 2020**. It will be released in SandProd **Q1 2020**.

## Changelog

### 2020-02-04

- Specified expiration length of Refund reservations to 24 hours. [Refunds](payment_flows#refunds)

---
### 2020-01-31

- Added a description of Self-Certification to the documention under [Self Certification](self_certification)

---

### 2019-12-23

- Changed the month that news will come out regarding self-certification from December 2019 to January 2020

---

### 2019-12-10

- Added `BrandName` to the subpage **Input and Output Formats** in the Brand section

---

### 2019-12-10

- Renamed subpage **Input Formats** to **Input and Output Formats**.
- Adjusted content of subpage **Input and Output Formats**
  - **HTTP Headers**
    - Renamed from `X-MP-\*` to `X-MobilePay-\*`.
    - Removed `X-MP-IntegratorId`.
  - **Payments**
    - Added `PlannedCaptureDelay`, `CustomerToken` and `CustomerReceiptToken`.
