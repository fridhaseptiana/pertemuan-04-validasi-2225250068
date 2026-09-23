# Pertemuan 04 Seleksi Multi-Kondisi dan Validasi Input

**Nama:** Fridha Septiana
**NIM:** 2225250068
**Kelas:** 3E

## Tujuan

Membangun program validasi dan klasifikasi dengan menggunakan rantai `if-elif-else`, kondisi majemuk, validasi tipe input, validasi rentang, serta klasifikasi berdasarkan beberapa kondisi.

## Cara Menjalankan

Program dapat dijalankan melalui terminal dengan perintah:

```bash
python3 praktik/validasi_klasifikasi_nilai.py
```

Pada Windows, jika `python3` tidak dapat digunakan, dapat menggunakan:

```bash
python praktik/validasi_klasifikasi_nilai.py
```

## Tabel Keputusan

| Kategori                         | Syarat                                    | Contoh Masukan                            |
| -------------------------------- | ----------------------------------------- | ----------------------------------------- |
| Input ditolak karena tipe        | Salah satu masukan bukan angka            | Ujian = 80, Tugas = 80, Kehadiran = `abc` |
| Input ditolak karena nilai ujian | Nilai ujian < 0 atau > 100                | Ujian = 105                               |
| Input ditolak karena nilai tugas | Nilai tugas < 0 atau > 100                | Tugas = -5                                |
| Input ditolak karena kehadiran   | Kehadiran < 0 atau > 100                  | Kehadiran = 105                           |
| Tidak memenuhi syarat kehadiran  | Kehadiran < 80%                           | Ujian = 90, Tugas = 90, Kehadiran = 75    |
| Predikat A, Lulus                | Nilai akhir ≥ 85 dan kehadiran ≥ 80%      | Ujian = 90, Tugas = 80, Kehadiran = 95    |
| Predikat B, Lulus                | 70 ≤ nilai akhir < 85 dan kehadiran ≥ 80% | Ujian = 75, Tugas = 70, Kehadiran = 85    |
| Predikat C, Lulus                | 60 ≤ nilai akhir < 70 dan kehadiran ≥ 80% | Ujian = 60, Tugas = 60, Kehadiran = 80    |
| Predikat D, Belum lulus          | 50 ≤ nilai akhir < 60 dan kehadiran ≥ 80% | Ujian = 55, Tugas = 50, Kehadiran = 90    |
| Predikat E, Belum lulus          | Nilai akhir < 50 dan kehadiran ≥ 80%      | Ujian = 40, Tugas = 30, Kehadiran = 100   |

Nilai akhir dihitung dengan rumus:

```text
Nilai akhir = (0.6 × nilai ujian) + (0.4 × nilai tugas)
```

## Hasil Pengujian

| No. | Masukan (Ujian, Tugas, Kehadiran) | Keluaran yang Diharapkan                           | Keluaran Aktual                                      | Status   |
| --- | --------------------------------- | -------------------------------------------------- | ---------------------------------------------------- | -------- |
| 1   | 90, 80, 95                        | Nilai akhir 86.00, Predikat A, Lulus               | Nilai akhir = 86.00, Predikat A, Lulus               | Berhasil |
| 2   | 75, 70, 85                        | Nilai akhir 73.00, Predikat B, Lulus               | Nilai akhir = 73.00, Predikat B, Lulus               | Berhasil |
| 3   | 60, 60, 80                        | Nilai akhir 60.00, Predikat C, Lulus               | Nilai akhir = 60.00, Predikat C, Lulus               | Berhasil |
| 4   | 55, 50, 90                        | Nilai akhir 53.00, Predikat D, Belum lulus         | Nilai akhir = 53.00, Predikat D, Belum lulus         | Berhasil |
| 5   | 40, 30, 100                       | Nilai akhir 36.00, Predikat E, Belum lulus         | Nilai akhir = 36.00, Predikat E, Belum lulus         | Berhasil |
| 6   | 90, 90, 75                        | Nilai akhir 90.00, Tidak memenuhi syarat kehadiran | Nilai akhir = 90.00, Tidak memenuhi syarat kehadiran | Berhasil |
| 7   | 105, 80, 90                       | Penolakan nilai ujian di luar rentang              | Penolakan nilai ujian di luar rentang                | Berhasil |
| 8   | 80, -5, 90                        | Penolakan nilai tugas di luar rentang              | Penolakan nilai tugas di luar rentang                | Berhasil |
| 9   | 80, 80, abc                       | Penolakan karena seluruh data harus berupa angka   | Penolakan karena seluruh data harus berupa angka     | Berhasil |

## Refleksi

Salah satu masukan tidak valid yang dapat terlewat jika program tidak menggunakan validasi tipe adalah memasukkan teks seperti `abc` pada bagian kehadiran. Jika input langsung dikonversi menggunakan `float()` tanpa penanganan kesalahan, program akan menghasilkan error dan berhenti.

Untuk menanganinya, program menggunakan `try-except` dengan `ValueError`. Ketiga masukan terlebih dahulu dibaca sebagai teks, kemudian dikonversi menjadi `float` di dalam blok `try`. Jika salah satu masukan bukan angka, program masuk ke `except` dan menampilkan pesan:

```text
Masukan ditolak: seluruh data harus berupa angka.
```

Dengan demikian, program dapat menangani masukan tidak valid dengan lebih aman sebelum melakukan perhitungan nilai akhir.
