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
- `streamlit_app.py` — aplikasi Streamlit.
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
   streamlit run streamlit_app.py
   ```

## Struktur data (kolom yang disarankan)
* `no_rkm_medis` / `no_rawat`
* `nm_pasien` / `nama_pasien`
* `tgl_kunjungan` / `tanggal` / `created_at`
* `poli` / `nama_poli`
* `status` (nilai: 'sudah' / 'gagal')
* `umur` (opsional)
* `jk` / `jenis_kelamin` (opsional)
* `waktu_antrol` / `waktu` (opsional)

> Jika nama kolom berbeda, app akan mencoba otomatis merename kolom umum. Untuk variasi ekstrem, buka `streamlit_app.py` dan sesuaikan fungsi `unify_columns`.

## Visual & Penjelasan (untuk presentasi)

1. **KPI header** — menampilkan total record, jumlah sukses, jumlah gagal, avg wait (jika ada).
   * **Penjelasan**: Gambaran cepat kesehatan operasional registrasi BPJS.

2. **Bar chart Status** — jumlah `sudah` vs `gagal`.
   * **Penjelasan**: Fokus mitigation pada kategori `gagal`.

3. **Line chart Tren Harian** — jumlah kunjungan per hari.
   * **Penjelasan**: Memantau tren & efek perubahan kebijakan/maintenance.

4. **Top Poli** — total kunjungan vs gagal per poli.
   * **Penjelasan**: Identifikasi poli yang membutuhkan intervensi.

5. **Distribusi Umur** — melihat profil pasien.
   * **Penjelasan**: Memudahkan kebijakan pelayanan (mis. poli anak).

## S.M.A.R.T Questions (contoh)

* Spesifik: Berapa persentase kegagalan BPJS di Poli X bulan ini?
* Terukur: Berapa rata-rata waktu tunggu pendaftaran (detik/min)?
* Dapat dicapai: Dapatkah mengurangi rate gagal 30% dalam 3 bulan?
* Relevan: Apakah kegagalan terkait jam tertentu?
* Batas waktu: Laporan mingguan untuk tindakan perbaikan.

## Lisensi

(opsional) Sesuaikan dengan kebijakan organisasi.

## Kontak / Kontributor

Nama / email Anda.
