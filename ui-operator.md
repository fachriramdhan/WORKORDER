# Brief UI/UX Operator Dashboard

## Sistem Work Order, OEE, dan Tracking Produksi

Dokumen ini berfokus pada **desain visual dan navigasi** untuk user operator di area produksi. Tujuan utama UI adalah:

* cepat dipahami
* cepat dipakai
* minim salah input
* cocok untuk layar TV, PC produksi, dan penggunaan saat kerja shift

---

# 1. Prinsip Desain UI Operator

## 1.1 Target Utama

UI operator harus mendukung aktivitas berikut:

* melihat status mesin secara cepat
* memilih work order aktif
* input produksi dengan langkah sesedikit mungkin
* input reject dan downtime dengan pilihan yang jelas
* mengurangi ketergantungan pada ketikan manual

## 1.2 Prinsip Desain

* **Tombol besar** agar mudah diklik saat kondisi kerja cepat
* **Pilihan terbatas** agar operator tidak bingung
* **Informasi penting di atas** agar status mesin langsung terlihat
* **Warna konsisten** untuk status mesin dan status proses
* **Minim teks panjang**
* **Form pendek** dan hanya menampilkan field yang memang dibutuhkan
* **Validasi otomatis** untuk mencegah input salah

---

# 2. Struktur Navigasi Utama

## 2.1 Navigasi Level 1

Aplikasi operator sebaiknya hanya punya beberapa menu inti:

1. **Dashboard Mesin**
2. **Work Order Aktif**
3. **Input Produksi**
4. **Downtime**
5. **Reject**
6. **Material Tracking**
7. **Riwayat / Log**

## 2.2 Navigasi yang Disarankan

```text
[Dashboard Mesin]
   ├── Klik mesin → [Detail Mesin]
   │                    ├── Work Order
   │                    ├── Input Produksi
   │                    ├── Reject
   │                    └── Downtime
   └── Top 5 Mesin
```

## 2.3 Pola Navigasi

Pola yang paling aman untuk operator:

* **Dashboard awal**
* klik kartu mesin
* masuk ke **halaman detail mesin**
* lakukan aksi dari tombol besar
* kembali ke dashboard

Dengan pola ini, operator tidak perlu membuka banyak halaman dan tidak tersesat di menu.

---

# 3. User Flow Operator

## 3.1 Flow Utama

```text
Login
  ↓
Dashboard Mesin
  ↓ klik mesin
Detail Mesin / Operation Summary
  ↓
Pilih aksi:
- Work Order
- Input Produksi
- Reject
- Downtime
  ↓
Simpan
  ↓
Dashboard update
```

## 3.2 Flow Saat Produksi Normal

```text
Operator login
  ↓
Lihat mesin running
  ↓
Klik mesin
  ↓
Lihat WO aktif
  ↓
Tambah output good
  ↓
Sistem simpan log
```

## 3.3 Flow Saat Ada Masalah

```text
Operator login
  ↓
Mesin status downtime
  ↓
Klik mesin
  ↓
Pilih reason downtime
  ↓
Start downtime
  ↓
Saat selesai: Stop downtime
```

---

# 4. Wireframe Halaman Utama

## 4.1 Login Page

Tujuan: cepat masuk, tidak banyak elemen.

```text
+------------------------------------------------------+
|                    COMPANY LOGO                      |
|                                                      |
|               Sistem Produksi / MES                  |
|                                                      |
|  [ Username / NIK                          ]         |
|  [ Password                                ]         |
|                                                      |
|  ( ) Operator   ( ) Supervisor   ( ) Admin           |
|                                                      |
|              [   LOGIN   ]                           |
|                                                      |
+------------------------------------------------------+
```

### Catatan UX

* form hanya 2 field utama
* role bisa otomatis berdasarkan akun, lebih baik tidak perlu dipilih jika memungkinkan
* tombol login dibuat besar dan jelas

---

## 4.2 Dashboard Mesin

Halaman ini untuk TV atau monitor utama.

```text
+-----------------------------------------------------------------------------------+
| LOGO | Dashboard Produksi | Shift: A | Tanggal | Jam | User Login                 |
+-----------------------------------------------------------------------------------+
| [ Running 12 ] [ Downtime 3 ] [ Off 5 ] [ Top 5 Mesin ] [ Total WO Aktif 18 ]     |
+-----------------------------------------------------------------------------------+
|                                                                                   |
|  [ Mesin 01 ]   [ Mesin 02 ]   [ Mesin 03 ]   [ Mesin 04 ]   [ Mesin 05 ]        |
|  Running        Downtime       Off           Running       Running                |
|  WO: 13423      WO: 12991      -             WO: 14520     WO: 15880             |
|  68% OEE        42% OEE        -             81% OEE       75% OEE                |
|                                                                                   |
|  [ Mesin 06 ]   [ Mesin 07 ]   [ Mesin 08 ]   [ Mesin 09 ]   [ Mesin 10 ]        |
|                                                                                   |
+-----------------------------------------------------------------------------------+
| Panel kanan / bawah: Top 5 Mesin                                                  |
| 1. Mesin 04 - 81%                                                                  |
| 2. Mesin 05 - 75%                                                                  |
| 3. Mesin 01 - 68%                                                                  |
| 4. Mesin 08 - 66%                                                                  |
| 5. Mesin 02 - 61%                                                                  |
+-----------------------------------------------------------------------------------+
```

### Catatan UX

* kartu mesin harus besar dan mudah dibaca dari jauh
* status memakai warna konsisten:

  * hijau = running
  * merah = downtime
  * abu = off
  * kuning = warning / changeover
* bagian **Top 5 Mesin** harus terlihat jelas karena membantu supervisor memantau performa

---

## 4.3 Detail Mesin / Operation Summary

Halaman ini adalah inti untuk operator.

```text
+-----------------------------------------------------------------------------------+
| < Back | Mesin 01 | Status: RUNNING | OEE: 68%                                   |
+-----------------------------------------------------------------------------------+
| WORK ORDER AKTIF                                                                  |
| WO ID        : 13423                                                              |
| Toy No       : JKY78                                                              |
| Target       : 837549 pcs                                                         |
| Part Number  : 83457983745                                                        |
| Panel        : Front-Rear SS                                                      |
| Actual Good  : 521000 pcs                                                         |
| Reject       : 1200 pcs                                                           |
| Progress     : [███████████-------] 62%                                           |
+-----------------------------------------------------------------------------------+
| [ Input Produksi ]   [ Reject ]   [ Downtime ]   [ Work Order ]                   |
+-----------------------------------------------------------------------------------+
| OEE SUMMARY                                                                       |
| Availability  : 89%                                                               |
| Runtime       : 08:12:20                                                          |
| Uptime        : 07:55:10                                                          |
| Downtime      : 00:17:10                                                          |
| Performance   : 84%                                                               |
| Standard Cycle: 12.5 sec                                                          |
| Average Cycle : 14.1 sec                                                          |
| Last Cycle    : 13.9 sec                                                          |
| Quality       : 99.7%                                                             |
+-----------------------------------------------------------------------------------+
```

### Catatan UX

* informasi utama ditaruh di atas
* tombol aksi ada di tengah dan ukurannya besar
* metrik OEE ditaruh di bawah sebagai informasi pendukung
* operator tidak perlu scroll terlalu jauh

---

# 5. Wireframe Halaman Input

## 5.1 Input Produksi

```text
+-------------------------------------------------------------+
| Input Produksi - Mesin 01                                   |
+-------------------------------------------------------------+
| WO Aktif  : 13423                                           |
| Target    : 837549 pcs                                      |
| Good Qty  : [      100      ]  [-10] [+10] [+50] [+100]     |
| Shift     : [ A ▼ ]                                         |
| Operator  : [ Nama operator auto ]                          |
| Catatan   : [ optional................................ ]    |
|                                                             |
|                 [ BATAL ]   [ SIMPAN ]                      |
+-------------------------------------------------------------+
```

### Catatan UX

* input quantity bisa pakai tombol increment agar cepat
* field jumlah harus tetap bisa diketik manual
* data operator sebaiknya auto dari login
* tombol simpan besar dan jelas

---

## 5.2 Reject Input

```text
+-------------------------------------------------------------+
| Input Reject - Mesin 01                                     |
+-------------------------------------------------------------+
| WO Aktif  : 13423                                           |
| Reject Qty: [      5       ]  [-1] [+1] [+5] [+10]          |
| Reason    : [ Pilih reason ▼ ]                              |
|             - NG Visual                                     |
|             - NG Dimensi                                    |
|             - NG Fungsi                                     |
|             - Material Defect                                |
| Catatan   : [ optional................................ ]    |
|                                                             |
|                 [ BATAL ]   [ SIMPAN ]                      |
+-------------------------------------------------------------+
```

### Catatan UX

* reason reject harus berupa dropdown
* opsi reason sebaiknya singkat dan sering dipakai
* validasi wajib agar jumlah reject tidak melebihi output

---

## 5.3 Downtime Input

```text
+------------------------------------------------------------------+
| Downtime - Mesin 01                                              |
+------------------------------------------------------------------+
| WO Aktif  : 13423                                                |
| Status    : RUNNING / DOWNTIME                                   |
| Reason    : [ Pilih reason downtime ▼ ]                          |
|             - Operational Downtime                               |
|             - Connectivity                                       |
|             - Changeover                                          |
|             - Plan Downtime                                       |
|             - Call Mechanic                                       |
|             - Break                                               |
|             - External Constraints                                |
|             - Planned Maintenance                                |
|             - Running                                             |
|             - Out of Cycle                                        |
|             - Machine Off / No Schedule                           |
|                                                                  |
| Action    : [ START DOWNTIME ] [ END DOWNTIME ]                  |
| Note      : [ optional....................................... ] |
|                                                                  |
|                    [ BATAL ]   [ SIMPAN ]                        |
+------------------------------------------------------------------+
```

### Catatan UX

* reason downtime wajib dipilih
* tombol start/end dibuat jelas dan dibedakan warna
* jika downtime aktif, tampilan harus langsung berubah supaya operator tahu statusnya

---

## 5.4 Work Order Selection

```text
+-------------------------------------------------------------+
| Work Order                                                  |
+-------------------------------------------------------------+
| Mesin      : Mesin 01                                       |
| WO Aktif   : 13423                                          |
| WO Baru    : [ pilih WO ▼ ]                                 |
| Filter     : [ Today ] [ Open ] [ Planned ] [ Running ]     |
|                                                             |
| Daftar WO                                                    |
| - 13423 | JKY78 | Running                                   |
| - 13424 | JKY79 | Planned                                   |
| - 13425 | JKY80 | Open                                       |
|                                                             |
|                 [ BATAL ]   [ SET WO ]                      |
+-------------------------------------------------------------+
```

### Catatan UX

* daftar WO harus bisa difilter
* WO aktif harus terlihat jelas
* perubahan WO harus ada konfirmasi agar tidak salah pilih

---

# 6. Komponen UI yang Disarankan

## 6.1 Komponen Utama

* machine card
* status badge
* action button besar
* modal konfirmasi
* progress bar
* summary panel
* top 5 ranking panel

## 6.2 Komponen Tambahan

* toast sukses / error
* notifikasi suara untuk status tertentu
* skeleton loading
* empty state
* badge warna untuk status WO

---

# 7. Struktur Navigasi yang Disarankan

## 7.1 Untuk TV / Dashboard

Navigasi dibuat sangat minimal:

* Dashboard
* Detail Mesin
* Top 5 Mesin
* Logout

## 7.2 Untuk PC Operator

Navigasi utama:

* Dashboard
* Work Order
* Produksi
* Reject
* Downtime
* Material
* Riwayat

## 7.3 Struktur Menu Samping

```text
[ Dashboard ]
[ Work Order ]
[ Produksi ]
[ Reject ]
[ Downtime ]
[ Material ]
[ Riwayat ]
[ Logout ]
```

### Catatan UX

* menu jangan terlalu banyak level
* item yang sering dipakai harus paling atas
* untuk operator, sidebar harus ringkas dan konsisten

---

# 8. Aturan Visual / UI Style

## 8.1 Warna Status

* **Hijau** = Running
* **Merah** = Downtime
* **Abu** = Off
* **Kuning** = Warning / Changeover
* **Biru** = Informasi / detail

## 8.2 Ukuran Layout

* kartu mesin minimal lebar besar agar mudah dilihat di TV
* tombol aksi minimal tinggi 48px untuk kenyamanan klik
* font harus tegas dan mudah dibaca

## 8.3 Hierarki Informasi

Urutan tampilan:

1. Status mesin
2. Work order aktif
3. Output / reject
4. OEE summary
5. Riwayat / detail tambahan

---

# 9. Mekanisme Pencegahan Error

UI ini harus mengurangi kesalahan input dengan cara:

* dropdown untuk reason
* default value auto dari data sebelumnya
* validasi range angka
* konfirmasi sebelum simpan
* tombol start/end yang jelas
* disable tombol jika status tidak sesuai
* tampilkan pesan error yang singkat dan mudah dipahami

Contoh:

* jika mesin belum punya WO aktif, tombol input produksi tidak aktif
* jika downtime sedang aktif, tombol start downtime nonaktif
* jika reject melebihi output, tampilkan error

---

# 10. Wireframe Dashboard Top 5 Mesin

```text
+----------------------------------------------+
| TOP 5 MESIN TERBAIK                           |
+----------------------------------------------+
| 1. Mesin 04 | OEE 81% | Running              |
| 2. Mesin 05 | OEE 75% | Running              |
| 3. Mesin 01 | OEE 68% | Running              |
| 4. Mesin 08 | OEE 66% | Running              |
| 5. Mesin 02 | OEE 61% | Downtime            |
+----------------------------------------------+
```

### Catatan UX

* top 5 sebaiknya berdasarkan OEE tertinggi
* dapat juga diberi indikator naik/turun dibanding shift sebelumnya
* tampilan harus sederhana dan langsung terbaca

---

# 11. Rekomendasi Alur Penggunaan Harian

## Awal Shift

* login
* buka dashboard
* lihat mesin yang aktif
* pilih mesin yang akan dipantau

## Saat Produksi

* cek WO aktif
* input output good
* input reject jika ada
* pantau status mesin

## Saat Ada Gangguan

* buka downtime
* pilih reason
* start downtime
* setelah selesai, stop downtime

## Akhir Shift

* review summary
* cek total produksi
* cek reject
* cek downtime
* logout

---

# 12. Kesimpulan UI/UX

Desain operator yang baik untuk sistem ini harus:

* cepat dioperasikan
* minim salah input
* sangat jelas secara visual
* mudah dipakai di area produksi
* mendukung kerja shift dan monitor TV

Prinsip utamanya adalah **sedikit klik, sedikit ketik, banyak otomatisasi visual**.

---

# 13. Rekomendasi Lanjutan

Setelah wireframe ini disetujui, tahap berikutnya bisa dibuat:

1. desain layout Bootstrap
2. komponen React / Razor View
3. alur modal input
4. validasi form
5. style guide warna dan status
6. versi prototype HTML

---

## Lampiran: Ringkasan Navigasi

```text
Dashboard
  └── Detail Mesin
        ├── Work Order
        ├── Produksi
        ├── Reject
        └── Downtime

Dashboard
  └── Top 5 Mesin
```
