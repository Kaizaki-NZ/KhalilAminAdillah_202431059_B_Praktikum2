# Praktikum 2 — Web Scraping

Latihan mengambil data tabel langsung dari halaman web menggunakan `requests` untuk mengunduh HTML dan `pandas.read_html` untuk mengubahnya menjadi DataFrame. Pekerjaan dilakukan di notebook `Web Scraping.ipynb` dengan dua situs latihan yang berbeda.

| | |
|---|---|
| **Mata Kuliah** | Machine Learning / Pembelajaran Mesin |
| **Nama** | Khalil Amin Adillah |
| **NIM** | 202431059 |

## Isi Folder

```
Web Scraping.ipynb   # Notebook scraping dua situs
```

## Sumber Data

### 1. Worldometer — Populasi Negara

`https://www.worldometers.info/world-population/population-by-country/`

Menghasilkan **234 baris × 12 kolom** tanpa nilai kosong.

| Kolom | Keterangan |
|---|---|
| `#` | Peringkat populasi |
| `Country (or dependency)` | Nama negara/wilayah |
| `Population 2026` | Jumlah populasi |
| `Yearly Change` | Perubahan populasi per tahun |
| `Net Change` | Perubahan absolut per tahun |
| `Density (P/Km²)` | Kepadatan penduduk |
| `Land Area (Km²)` | Luas daratan |
| `Migrants (net)` | Migrasi bersih |
| `Fert. Rate` | Tingkat kesuburan |
| `Median Age` | Usia median |
| `Urban Pop %` | Persentase penduduk urban |
| `World Share` | Porsi terhadap populasi dunia |

### 2. ScrapeThisSite — Statistik Tim Hockey

`https://www.scrapethissite.com/pages/forms/`

Menghasilkan **25 baris × 9 kolom** dari halaman pertama (musim 1990–1991, 21 tim berbeda).

| Kolom | Keterangan |
|---|---|
| `Team Name` | Nama tim |
| `Year` | Musim |
| `Wins` | Menang |
| `Losses` | Kalah |
| `OT Losses` | Kalah di overtime |
| `Win %` | Persentase kemenangan |
| `Goals For (GF)` | Gol dicetak |
| `Goals Against (GA)` | Gol kebobolan |
| `+ / -` | Selisih gol |

## Cara Kerja

1. **Menyiapkan library** — `requests`, `pandas`, dan `StringIO` dari modul `io`.
2. **Memasang header** — `User-Agent: Mozilla/5.0` agar request diterima seperti browser biasa.
3. **Mengunduh halaman** — `requests.get()` mengambil HTML mentah dari tiap URL.
4. **Mengubah HTML menjadi DataFrame** — `pd.read_html()` mengembalikan daftar tabel; yang dipakai adalah tabel pertama (`[0]`).
5. **Menampilkan hasil** — `df.head()` untuk memeriksa lima baris pertama tiap tabel.

## Menjalankan Notebook

Kebutuhan: Python 3.10 atau lebih baru.

```bash
pip install requests pandas lxml
jupyter notebook "Web Scraping.ipynb"
```

`lxml` dibutuhkan `pandas.read_html` sebagai parser HTML. Jalankan cell dari atas ke bawah; notebook memerlukan koneksi internet karena data diambil langsung dari kedua situs.

## Catatan

- Angka pada kolom seperti `Yearly Change`, `Net Change`, dan `Migrants (net)` memakai karakter minus unicode (`−`) serta pemisah ribuan (`,`), sehingga masih bertipe teks. Perlu dibersihkan dulu sebelum dihitung sebagai angka.
- Situs ScrapeThisSite memakai paginasi. Notebook hanya mengambil halaman pertama; untuk seluruh data perlu iterasi `?page=1`, `?page=2`, dan seterusnya.
- `pd.read_html()[0]` bergantung pada urutan tabel di halaman. Kalau struktur situs berubah, indeks tabelnya perlu disesuaikan.

Dibuat untuk memenuhi tugas Praktikum 2 mata kuliah Machine Learning / Pembelajaran Mesin.
