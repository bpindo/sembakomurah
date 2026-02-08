Siap. Di bawah ini aku kirim **README versi FINAL yang SUDAH DIBETULKAN**,
**lengkap, detil, production-minded**, dan **aman dari bug sistem** berdasarkan audit & manajemen ulang helper yang kita bahas.

Ini **siap langsung kamu taruh sebagai `README.md` di GitHub**.

---

```md
# 🛒 Sembako Affiliate System

**Production-Ready Affiliate Platform with Ledger-Based Economy**

---

## 1. Overview

Sembako Affiliate System adalah platform affiliate berbasis **traffic nyata** dengan ekonomi internal yang dicatat menggunakan **ledger**.

Sistem ini dirancang untuk:
- menghargai affiliate yang aktif & jujur,
- mencegah spam dan multi-akun,
- menghilangkan ketergantungan moderasi manual,
- menjaga stabilitas ekonomi sistem dalam jangka panjang.

---

## 2. Core Principles

### 2.1 Ledger-Based Economy

Semua nilai ekonomi **WAJIB** dicatat di tabel:

```

point_ledger

```

Tidak ada saldo statis yang dipercaya.

Ledger digunakan untuk:
- upload quota
- reward traffic
- promotion credit
- banner cost (CPC)
- system tax & burn

**Ledger bersifat immutable**  
Tidak ada update, hanya insert delta (+ / -).

---

### 2.2 Device-Centric Anti Spam

Sistem menggunakan **device_id (cookie)** sebagai fondasi:

- 1 device = 1 visit / post / hari
- 1 device = 1 akun affiliate
- Klik ganda dari device yang sama diabaikan

Device tracking digunakan untuk:
- anti multi-account
- traffic validation
- report trust
- referral ringan

---

### 2.3 One System, One Truth

- Tidak ada sistem user biasa
- Tidak ada auth ganda
- Tidak ada quota statis
- Tidak ada ranking manual

**Affiliate System adalah satu-satunya sistem aktif.**

---

## 3. Actors

| Actor | Description |
|-----|------------|
| Affiliate | Upload produk & menerima reward |
| Viewer | Mengunjungi & mengklik produk |
| Investor | Membeli banner & membayar per click |
| Admin | Penerima pajak & takeover |
| Cron System | Otomasi ekonomi & resource sink |

---

## 4. Final Folder Structure (Production Clean)

```

/
├── api/                # HTTP endpoints (controller layer)
│   ├── register.php
│   ├── login.php
│   ├── upload_product.php
│   ├── visit.php
│   ├── report.php
│   └── quota.php
│
├── services/           # Business rules (NO side-effects)
│   ├── LedgerService.php
│   ├── QuotaService.php
│   ├── RankingService.php
│   ├── ReportService.php
│   └── AuthService.php
│
├── repositories/       # Database access only
│   ├── LedgerRepo.php
│   ├── DeviceRepo.php
│   ├── AffiliateRepo.php
│   ├── PostRepo.php
│   └── VisitRepo.php
│
├── helpers/            # Utility only (pure functions)
│   ├── uuid.php
│   ├── date.php
│   └── hash.php
│
├── includes/
│   ├── db.php
│   └── bootstrap.php
│
├── cron/
│   └── autopromo.php
│
├── public/
│   ├── index.php
│   ├── dashboard.php
│   └── assets/main.js
│
└── README.md

```

---

## 5. Helper & Service Rules (ANTI BUG CONTRACT)

### ❗ Mandatory Rules

1. Helper **TIDAK BOLEH**:
   - start session
   - set cookie
   - echo / header
   - akses `$_POST` / `$_SESSION`

2. Service **HANYA**:
   - validasi
   - kalkulasi
   - orchestration logic

3. Repository **HANYA**:
   - query database
   - tidak boleh logika bisnis

4. Semua operasi ekonomi **HARUS TRANSACTIONAL**

5. Cron ≠ API ≠ Frontend  
   (tidak boleh berbagi implicit context)

Melanggar aturan ini = **bug sistem**.

---

## 6. Core Modules

### 6.1 Device Management

**Tujuan:** Anti spam & identifikasi visitor.

Aturan:
- device dibuat jika belum ada
- cookie bersifat long-lived
- tidak ada IP-based logic

Mode penggunaan:
- `visitor`
- `affiliate_auth`
- `affiliate_action`
- `cron` (tidak pakai device)

---

### 6.2 Authentication (Affiliate Only)

Login menggunakan:
- username
- private key (random, unrecoverable)
- device lock

Aturan:
- 1 akun = 1 device
- 1 device = 1 akun
- tidak ada reset password

Security model: **API-key style auth**

---

### 6.3 Ledger Service

**Jantung ekonomi sistem**

Fungsi utama:
- `getBalance(affiliate_id)`
- `requireBalance(affiliate_id, cost)`
- `addEntry(affiliate_id, delta, type, meta)`

Semua pemakaian quota:
- upload produk
- banner click
- autopromo burn  
➡️ **HARUS lewat ledger**

---

### 6.4 Upload Product Flow

Atomic transaction:

1. Begin transaction
2. Cek saldo ledger ≥ 1
3. Insert produk
4. Ledger add: `-1 upload_product`
5. Commit

➡️ Tidak ada double spend.

---

### 6.5 Visit & Reward Flow

Aturan:
- 1 device / post / hari
- Insert IGNORE

Reward:
- setiap 5 visit unik → +0.1
- max 0.3 per hari
- masuk via ledger

---

### 6.6 Ranking System

Ranking **tidak live-read ledger**.

Menggunakan:
- snapshot via cron
- data stabil & konsisten

Faktor ranking:
1. harga (paling berat)
2. rating toko
3. jumlah terjual
4. promotion credit
5. penalti status report

---

### 6.7 Report System

- report ganda dicegah
- bobot report:
  - affiliate: kuat
  - viewer trusted: sedang
  - viewer baru: lemah

Produk tidak langsung dihapus.
Status berubah bertahap:
- normal
- disputed
- hidden

---

## 7. Cron Jobs

### 7.1 Autopromo (Resource Sink)

Trigger:
- affiliate tidak login ≥ 30 hari
- saldo ledger masih ada

Action:
- burn quota (max 0.1)
- convert ke promotion credit

Tujuan:
- akun mati tidak menimbun resource
- ranking tetap dinamis

Cron **TIDAK**:
- pakai session
- pakai cookie
- pakai auth helper

---

## 8. Frontend Philosophy

- frontend tipis
- SEO-friendly
- tidak ada logika bisnis
- semua validasi di backend

JS hanya untuk:
- tracking visit
- async UX

---

## 9. Database Characteristics

- Ledger immutable
- Composite unique key untuk anti duplicate
- DECIMAL untuk ekonomi
- Foreign key untuk konsistensi

Tabel inti:
- affiliates
- posts
- devices
- post_visits
- point_ledger
- reports
- promotion_logs

---

## 10. System Guarantees

Dengan desain ini:
- tidak ada quota bocor
- tidak ada double reward
- tidak ada spam click efektif
- ranking stabil & fair
- siap dimigrasikan ke Node.js / Next.js

---

## 11. Summary

Sembako Affiliate System adalah:
- **ledger-driven**
- **device-secured**
- **economically stable**
- **production-minded**

> Yang aktif berkembang.  
> Yang ditinggal, pengaruhnya menyusut otomatis.  
> Tanpa admin manual. Tanpa spam.

---

## 12. Roadmap (Optional)

- migrate to Node.js + Prisma
- Redis snapshot ranking
- investor dashboard
- fraud scoring device
- analytics panel

```


