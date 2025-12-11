# Dashboard Pasien BPJS Add Antroll

**Deskripsi singkat**
Dashboard interaktif untuk monitoring pendaftaran BPJS (Add Antroll) — analisis sukses vs gagal, tren kunjungan, top poli, dan pasien dengan kunjungan tinggi. Dibangun dengan Streamlit + Python.

## Fitur utama

- Filter rentang tanggal, poli, status.
- Visualisasi: bar chart (status), line chart (tren harian), bar chart top poli, histogram umur.
- Mode EDA: Deskriptif & Lanjutan (pasien >=10 kunjungan, peak hours).
- Ekspor CSV pasien gagal.
- Langkah wrangling otomatis untuk menormalkan kolom umum.

## File penting

- `streamlit.py` — aplikasi Streamlit.
- `requirements.txt` — dependency.
- `database/data/bpjs antrol.csv` — dataset (contoh).

## Cara menjalankan (lokal)

1. Clone repo:

   ```bash
   git clone https://github.com/Mudhya19/BPJS-Add-Antroll-Dashboard.git
   cd BPJS-Add-Antroll-Dashboard
   ```

2. Setup env & install:

   ```bash
   python -m venv venv
   source venv/bin/activate   # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Run:
   ```bash
   streamlit run streamlit.py
   ```

## Struktur data

1. `no_rawat` - `Nomor registrasi rawat`
2. `tgl_registrasi` - `Tanggal registrasi`
3. `jam_reg` - `Jam registrasi`
4. `kd_dokter` - `Kode dokter`
5. `nm_dokter` - `Nama dokter`
6. `no_rkm_medis` - `Nomor rekam medis`
7. `nm_pasien` - `Nama pasien`
8. `kd_poli` - `Kode poliklinik`
9. `nm_poli` - `Nama poliklinik`
10. `status_lanjut` - `Status lanjut (Ralan = Rawat Jalan)`
11. `kd_pj` - `Kode penjamin`
12. `png_jawab` - `Penanggung jawab`
13. `tanggal_periksa` - `Tanggal periksa`
14. `nomor_kartu` - `Nomor kartu BPJS`
15. `nomor_referensi` - `Nomor referensi`
16. `kodebooking` - `Kode booking`
17. `jenis_kunjungan` - `Jenis kunjungan`
18. `status_kirim` - `Status kirim (Sudah/Gagal/Ambil Antrian/Belum)`
19. `keterangan` - `Keterangan`
20. `USER` - `Nama user`

> Jika nama kolom berbeda, app akan mencoba otomatis merename kolom umum. Untuk variasi ekstrem, buka `streamlit.py` dan sesuaikan fungsi `unify_columns`.

## S.M.A.R.T Questions

1. **Berapa jumlah total registrasi pasien BPJS per hari?**
   - *Specific*: Mengukur jumlah registrasi harian
   - *Measurable*: Dapat dihitung dari data tanggal registrasi
   - *Achievable*: Data tersedia di dataset
   - *Relevant*: Penting untuk mengetahui volume layanan
   - *Time-bound*: Dapat dianalisis per hari, minggu, atau bulan

2. **Berapa persentase keberhasilan registrasi BPJS per poliklinik?**
   - *Specific*: Mengukur efektivitas registrasi per poliklinik
   - *Measurable*: Dihitung sebagai rasio registrasi sukses terhadap total
   - *Achievable*: Status registrasi tersedia di dataset
   - *Relevant*: Penting untuk evaluasi kinerja layanan
   - *Time-bound*: Dapat dianalisis dalam periode tertentu

3. **Apa poliklinik dengan jumlah kunjungan tertinggi dan terendah?**
   - *Specific*: Identifikasi poliklinik berdasarkan volume kunjungan
   - *Measurable*: Dihitung berdasarkan jumlah registrasi per poliklinik
   - *Achievable*: Nama poliklinik tersedia di dataset
   - *Relevant*: Penting untuk alokasi sumber daya
   - *Time-bound*: Dapat dianalisis dalam periode tertentu

4. **Apa penyebab utama kegagalan registrasi BPJS?**
   - *Specific*: Mengidentifikasi faktor-faktor yang menyebabkan kegagalan
   - *Measurable*: Dihitung berdasarkan kategori keterangan error
   - *Achievable*: Data keterangan error tersedia di dataset
   - *Relevant*: Penting untuk perbaikan sistem
   - *Time-bound*: Dapat dianalisis dalam periode tertentu

5. **Bagaimana pola distribusi waktu registrasi pasien?**
   - *Specific*: Mengidentifikasi jam-jam sibuk pendaftaran
   - *Measurable*: Dihitung berdasarkan jam registrasi
   - *Achievable*: Jam registrasi tersedia di dataset
   - *Relevant*: Penting untuk manajemen antrian
   - *Time-bound*: Dapat dianalisis harian/mingguan

## Visualisasi Data

1. **KPI header** — menampilkan total record, jumlah sukses, jumlah gagal, avg wait (jika ada).
   
   - **Penjelasan**: Gambaran cepat kesehatan operasional registrasi BPJS.

2. **Bar chart Status** — jumlah `sudah` vs `gagal`.

   - **Penjelasan**: Fokus mitigation pada kategori `gagal`.

3. **Line chart Tren Harian** — jumlah kunjungan per hari.

   - **Penjelasan**: Memantau tren & efek perubahan kebijakan/maintenance.

4. **Top Poli** — total kunjungan vs gagal per poli.

   - **Penjelasan**: Identifikasi poli yang membutuhkan intervensi.

5. **Distribusi Umur** — melihat profil pasien.
   - **Penjelasan**: Memudahkan kebijakan pelayanan (mis. poli anak).

<!-- ## Lisensi

(opsional) Sesuaikan dengan kebijakan organisasi.

## Kontak / Kontributor

Nama / email Anda. -->
