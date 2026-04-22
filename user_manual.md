# User Manual Sistem MES (Operator & Supervisor)

Dokumen ini berisi panduan penggunaan sistem **Work Order, Produksi, OEE, dan Monitoring Mesin** untuk user di area produksi.

---

# 1. Tujuan Manual

Manual ini dibuat agar user dapat:

* Mengoperasikan sistem dengan cepat
* Menginput data produksi dengan benar
* Mengurangi kesalahan penggunaan
* Memahami alur kerja sistem

---

# 2. Tipe User

## 2.1 Operator

* Input produksi
* Input reject
* Input downtime
* Melihat status mesin

## 2.2 Supervisor

* Monitoring dashboard
* Melihat performa mesin (OEE)
* Analisa Top 5 mesin

---

# 3. Login ke Sistem

## Langkah:

1. Buka aplikasi MES
2. Masukkan:

   * Username / NIK
   * Password
3. Klik tombol **LOGIN**

```text
[ Username ]
[ Password ]
[ LOGIN ]
```

Jika berhasil, akan masuk ke halaman dashboard.

---

# 4. Dashboard Mesin

## Fungsi:

* Melihat status semua mesin
* Mengetahui mesin running / downtime / off
* Melihat OEE per mesin
* Melihat Top 5 mesin terbaik

## Warna Status:

* Hijau = Running
* Merah = Downtime
* Abu = Off
* Kuning = Warning / Changeover

## Cara Menggunakan:

1. Lihat status mesin
2. Klik mesin yang ingin dioperasikan

---

# 5. Detail Mesin (Operation Summary)

## Informasi yang Ditampilkan:

* Work Order ID
* Toy Number
* Target produksi
* Part Number
* Panel
* Output Good
* Reject
* Progress produksi
* OEE (Availability, Performance, Quality)

## Tombol Aksi:

* Input Produksi
* Reject
* Downtime
* Work Order

---

# 6. Input Produksi

## Langkah:

1. Klik tombol **Input Produksi**
2. Masukkan jumlah produksi (Good Qty)
3. Gunakan tombol cepat jika diperlukan:

   * +10
   * +50
   * +100
4. Klik **SIMPAN**

## Catatan:

* Pastikan Work Order sudah aktif
* Pastikan jumlah sesuai produksi aktual

---

# 7. Input Reject

## Langkah:

1. Klik tombol **Reject**
2. Masukkan jumlah reject
3. Pilih alasan reject
4. Klik **SIMPAN**

## Contoh Alasan:

* NG Visual
* NG Dimensi
* NG Fungsi
* Material Defect

## Catatan:

* Reject tidak boleh lebih besar dari total produksi

---

# 8. Input Downtime

## Langkah:

1. Klik tombol **Downtime**
2. Pilih alasan downtime
3. Klik **START DOWNTIME**
4. Setelah selesai, klik **END DOWNTIME**

## Daftar Reason:

* Operational Downtime
* Connectivity
* Changeover
* Plan Downtime
* Call Mechanic
* Break
* External Constraints
* Planned Maintenance
* Running
* Out of Cycle
* Machine Off / No Schedule

## Catatan:

* Pastikan downtime dihentikan setelah mesin berjalan kembali

---

# 9. Work Order

## Fungsi:

* Mengatur Work Order yang aktif pada mesin

## Langkah:

1. Klik tombol **Work Order**
2. Pilih WO dari daftar
3. Klik **SET WO**

## Catatan:

* Pastikan memilih WO yang benar
* Jangan mengganti WO tanpa izin supervisor

---

# 10. OEE (Monitoring Performa Mesin)

## Komponen:

* Availability
* Performance
* Quality
* OEE

## Penjelasan:

* Availability → waktu mesin aktif
* Performance → kecepatan produksi
* Quality → kualitas hasil produksi

## Fungsi:

* Mengetahui performa mesin
* Membantu analisa produksi

---

# 11. Top 5 Mesin

## Fungsi:

* Menampilkan 5 mesin dengan performa terbaik (berdasarkan OEE)

## Cara Membaca:

* Ranking 1 = performa terbaik
* Digunakan untuk monitoring supervisor

---

# 12. Aturan Penggunaan

* Input data secara real-time
* Jangan menunda input
* Gunakan reason yang sesuai
* Periksa kembali sebelum menyimpan

---

# 13. Kesalahan Umum

## 1. Tidak memilih Work Order

Solusi:

* Pastikan WO sudah aktif sebelum input produksi

## 2. Lupa menghentikan downtime

Solusi:

* Klik END DOWNTIME setelah mesin berjalan

## 3. Input jumlah salah

Solusi:

* Gunakan tombol increment
* Periksa sebelum simpan

---

# 14. Tips Penggunaan

* Gunakan tombol cepat (+10, +50)
* Fokus pada 1 mesin
* Gunakan dashboard untuk monitoring
* Laporkan jika sistem error

---

# 15. Penutup

Manual ini digunakan sebagai panduan dasar penggunaan sistem MES.

Gunakan sistem secara konsisten agar data produksi akurat dan dapat digunakan untuk analisa lebih lanjut.

---
