# Brief Perhitungan OEE di Backend (ASP.NET)

## Sistem MES – Work Order, Produksi, dan Monitoring Mesin

Dokumen ini menjelaskan **cara menghitung OEE (Overall Equipment Effectiveness)** dari data produksi yang dikumpulkan secara manual (operator input) maupun semi-otomatis.

Fokus dokumen:

* konsep perhitungan
* struktur data
* flow backend
* mapping ke ASP.NET (service logic)

---

# 1. Konsep Dasar OEE

OEE terdiri dari 3 komponen utama:

1. **Availability**
2. **Performance**
3. **Quality**

Rumus utama:

```text
OEE = Availability × Performance × Quality
```

---

# 2. Struktur Data yang Digunakan

## 2.1 Data Produksi

```text
production_logs
- machine_id
- wo_id
- qty_good
- qty_reject
- timestamp
```

## 2.2 Data Downtime

```text
downtime_logs
- machine_id
- wo_id
- reason
- start_time
- end_time
```

## 2.3 Data Work Order

```text
work_orders
- id
- qty_target
- standard_cycle_time (detik)
```

---

# 3. Flow Perhitungan OEE (Backend)

```text
Ambil data produksi
        ↓
Ambil data downtime
        ↓
Hitung Planned Time
        ↓
Hitung Runtime
        ↓
Hitung Availability
        ↓
Hitung Performance
        ↓
Hitung Quality
        ↓
Hitung OEE
```

---

# 4. Availability (Ketersediaan)

## 4.1 Definisi

Availability menunjukkan berapa persen waktu mesin benar-benar berjalan dibanding waktu yang direncanakan.

## 4.2 Rumus

```text
Availability = Runtime / Planned Production Time
```

## 4.3 Komponen

* Planned Production Time = total waktu shift
* Downtime = total downtime dari log
* Runtime = Planned Time - Downtime

```text
Runtime = Planned Time - Downtime
```

## 4.4 Visual

```text
Shift Time:      |---------------------------|
Downtime:        |-----|     |---|
Runtime:         |-----RUNNING---------|
```

---

# 5. Performance (Kinerja)

## 5.1 Definisi

Performance mengukur apakah mesin berjalan sesuai kecepatan ideal.

## 5.2 Rumus

```text
Performance = (Ideal Cycle Time × Total Output) / Runtime
```

## 5.3 Komponen

* Ideal Cycle Time = dari master data
* Total Output = good + reject
* Runtime = dari availability

---

# 6. Quality (Kualitas)

## 6.1 Definisi

Quality mengukur rasio produk baik dibanding total produksi.

## 6.2 Rumus

```text
Quality = Good Output / Total Output
```

## 6.3 Komponen

* Good Output = qty_good
* Total Output = qty_good + qty_reject

---

# 7. OEE Final

## 7.1 Rumus

```text
OEE = Availability × Performance × Quality
```

## 7.2 Contoh

```text
Availability = 0.90
Performance  = 0.85
Quality      = 0.98

OEE = 0.90 × 0.85 × 0.98 = 0.7497 (74.97%)
```

---

# 8. Perhitungan Waktu (Time Handling)

## 8.1 Planned Time

Bisa diambil dari:

* shift (misal 8 jam)
* atau dari schedule WO

```text
Planned Time = Shift End - Shift Start
```

## 8.2 Downtime

```text
Downtime = SUM(end_time - start_time)
```

## 8.3 Runtime

```text
Runtime = Planned Time - Downtime
```

---

# 9. Mapping ke Backend ASP.NET

## 9.1 Service Layer

Disarankan buat service:

```text
OeeService
```

## 9.2 Method Utama

```text
CalculateOee(machineId, startDate, endDate)
```

## 9.3 Flow Method

```text
1. Ambil production_logs
2. Ambil downtime_logs
3. Hitung total_good
4. Hitung total_reject
5. Hitung downtime
6. Hitung planned_time
7. Hitung runtime
8. Hitung availability
9. Hitung performance
10. Hitung quality
11. Hitung oee
12. Return result
```

---

# 10. Struktur Output OEE

```json
{
  "machineId": 1,
  "availability": 0.89,
  "performance": 0.84,
  "quality": 0.99,
  "oee": 0.74,
  "runtime": "08:12:00",
  "downtime": "00:48:00",
  "totalGood": 5000,
  "totalReject": 50
}
```

---

# 11. Perhitungan Tambahan (Optional)

## 11.1 Average Cycle

```text
Average Cycle = Runtime / Total Output
```

## 11.2 Last Cycle

* diambil dari data terakhir produksi

## 11.3 Uptime

```text
Uptime = Runtime - Minor Stops
```

---

# 12. Validasi Data

Backend harus melakukan validasi:

* jika total output = 0 → hindari division by zero
* jika runtime = 0 → set performance = 0
* jika planned time = 0 → availability = 0

---

# 13. Penyimpanan Data OEE

Disarankan simpan hasil OEE ke tabel:

```text
oee_snapshots
- machine_id
- date
- availability
- performance
- quality
- oee
```

Tujuan:

* mempercepat dashboard
* histori performa
* reporting

---

# 14. Flow Dashboard OEE

```text
User buka dashboard
        ↓
API ambil oee_snapshots
        ↓
Tampilkan:
- OEE
- Availability
- Performance
- Quality
        ↓
Update real-time (optional)
```

---

# 15. Kesimpulan

Perhitungan OEE di backend ASP.NET harus:

* berbasis data produksi & downtime
* menggunakan service layer
* memiliki validasi kuat
* bisa di-cache atau disimpan sebagai snapshot

Dengan pendekatan ini, sistem tetap bisa menghasilkan OEE yang akurat meskipun belum terintegrasi langsung ke mesin.

---

# 16. Rekomendasi Lanjutan

Setelah ini, kamu bisa lanjut ke:

1. implementasi OeeService di ASP.NET
2. integrasi ke API endpoint
3. tampilkan di dashboard
4. optimasi dengan caching / snapshot

---
