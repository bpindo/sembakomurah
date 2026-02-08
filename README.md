# 🛒 Sembako Affiliate System

Sistem affiliate sederhana dan adil untuk menampilkan produk sembako murah berdasarkan **aktivitas nyata**, bukan spam.

---

## 📌 Gambaran Umum

Project ini adalah **platform affiliate ringan** yang dirancang agar:

- produk murah & berkualitas otomatis naik,
- affiliate yang aktif mendapat keuntungan,
- akun spam dan akun mati kehilangan pengaruh secara alami.

Semua berjalan **otomatis**, tanpa kurasi manual.

---

## 👥 Peran dalam Sistem

1. **Affiliate**  
   Mengunggah produk dan membawa pengunjung.

2. **Pengunjung**  
   Melihat dan mengklik produk.

3. **Sistem**  
   Mengatur jatah upload, ranking produk, laporan, dan promosi otomatis.

---

## 🔁 Alur Besar Sistem


---

## 1️⃣ Pendaftaran Affiliate

### Dari sisi pengguna
- Cukup mengisi **username**
- Sistem memberikan **private key**
- Private key **harus disimpan** (tidak bisa dipulihkan)

### Aturan
- 1 device / IP → maksimal **1 pendaftaran per 24 jam**
- Tidak ada reset password

### Tujuan
- Mencegah akun palsu
- Setiap akun punya nilai dan tanggung jawab

---

## 2️⃣ Login Affiliate

- Login menggunakan **username + private key**
- Jika valid → bisa mengunggah produk

### Pembatasan
- **1 device hanya untuk 1 akun**
- Device yang sudah dipakai akun lain → login ditolak

**Manfaat:** mencegah peternakan akun.

---

## 3️⃣ Upload Produk & Jatah Upload

### Konsep Jatah
Anggap jatah upload seperti **kupon**:

- 1 upload = 1 kupon
- Kupon habis → tidak bisa upload

### Alur
1. Affiliate upload produk
2. Produk tampil di website
3. Jatah upload berkurang 1

**Tujuan:** mencegah spam dan upload asal-asalan.

---

## 4️⃣ Pengunjung & Klik Produk

### Dari sisi pengunjung
- Melihat daftar produk
- Klik produk → diarahkan ke marketplace

### Dari sisi sistem
- Setiap pengunjung dikenali sebagai **device unik**
- 1 device dihitung **1x per hari**

**Hasil:** klik berulang dari orang yang sama tidak dihitung.

---

## 5️⃣ Reward Jatah Upload

Jatah upload bertambah berdasarkan **traffic nyata**.

### Aturan
- 5 pengunjung unik → +0.1 jatah
- Maksimal +0.3 per hari
- Total jatah maksimal 3.0

**Prinsip:**  
> Traffic nyata → reward nyata

---

## 6️⃣ Ranking Produk

Produk tidak ditampilkan acak.

### Faktor Penilaian
1. Harga lebih murah (paling berpengaruh)
2. Rating toko
3. Jumlah terjual
4. Bonus kecil dari promotion credit

**Hasil:**
- Produk terbaik naik otomatis
- Produk mahal / jelek tenggelam sendiri

---

## 7️⃣ Sistem Laporan (Report)

Produk bisa dilaporkan oleh:
- Affiliate lain
- Pengunjung biasa

### Bobot Laporan
- Affiliate: kuat
- Pengunjung terpercaya: sedang
- Pengunjung baru: lemah

### Dampak
- Laporan sedikit → aman
- Laporan cukup → status *perlu dicek*
- Laporan berat → produk disembunyikan

Produk tidak langsung dihapus, tapi **diturunkan bertahap**.

---

## 8️⃣ Autopromo untuk Akun Tidak Aktif

Jika affiliate:
- Tidak login ≥ 30 hari
- Masih punya sisa jatah upload

### Yang terjadi
- Jatah upload dikurangi sedikit demi sedikit
- Jatah diubah menjadi **promotion credit**
- Promotion credit memberi **boost ringan** ke ranking

### Tujuan
- Akun mati tidak menyumbat sistem
- Resource tetap berputar
- Tidak ada penimbunan jatah

---

## ✅ Kesimpulan

Sistem ini dirancang agar:

- adil untuk affiliate aktif,
- tahan terhadap spam,
- berbasis aktivitas nyata,
- berjalan otomatis tanpa admin manual.

> Yang aktif berkembang.  
> Yang ditinggal, pelan-pelan kehilangan pengaruh.

---

## 📦 Cocok Digunakan Untuk

- Website affiliate niche
- Kurasi produk otomatis
- Eksperimen ekonomi sistem / game economy ringan
- Project side-hustle berbasis traffic

---

Jika diperlukan, dokumentasi ini bisa dikembangkan ke:
- diagram arsitektur,
- flowchart visual,
- pitch deck non-teknis,
- atau whitepaper konsep sistem.
