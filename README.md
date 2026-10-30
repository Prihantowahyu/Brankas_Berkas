# Brankas Berkas

Aplikasi web satu berkas untuk **mengunci berkas**, **mengecek keaslian berkas**, dan **menandatangani dokumen secara digital**. Semua proses berjalan di peramban (Web Crypto API). Tidak ada server, tidak ada data yang dikirim keluar, dan tidak butuh instalasi.

## Tiga konsep keamanan yang diterapkan

| Konsep | Fitur | Teknik |
|---|---|---|
| Enkripsi simetris | Kunci berkas / pesan dengan kata sandi, hasil `.brnk` | AES-256-GCM, kunci dari kata sandi lewat PBKDF2-SHA256 (310.000 iterasi), salt dan IV acak |
| Fungsi hash (integritas) | Hitung dan bandingkan sidik jari berkas | SHA-256 dan SHA-512 |
| Tanda tangan digital (asimetris) | Buat kunci, tanda tangani, verifikasi | ECDSA kurva P-256 + SHA-256 |

AES-GCM juga memberi autentikasi: jika berkas `.brnk` diubah satu byte saja, proses buka akan gagal.

## Contoh pemakaian sehari-hari

- Mengunci berkas nilai, rapor, atau data siswa sebelum dikirim lewat WhatsApp atau email.
- Memastikan file instalasi yang diunduh sama dengan hash resmi dari penyedianya.
- Memastikan salinan di flashdisk atau hasil backup identik dengan aslinya.
- Menandatangani surat, laporan, atau soal ujian agar penerima bisa memeriksa bahwa isinya asli dan tidak diubah.

## Cara memakai

1. **Kunci berkas**: pilih berkas atau tulis pesan, isi kata sandi, unduh hasil `.brnk`. Untuk membuka, pilih `.brnk` dan masukkan kata sandi yang sama.
2. **Cek keaslian**: pilih berkas, lalu tempel hash resmi atau pilih berkas pembanding. Akan muncul tanda *Cocok* atau *Berbeda*.
3. **Tanda tangan**:
   1. Buat pasangan kunci (kunci privat boleh diberi kata sandi).
   2. Tanda tangani berkas dengan kunci privat, unduh `nama-berkas.sig.json`.
   3. Penerima memverifikasi dengan berkas asli, `.sig.json`, dan kunci publik Anda.

Bagikan **kunci publik** saja. **Kunci privat** jangan pernah dikirim ke siapa pun.

## Menjalankan

Buka `index.html` langsung di peramban modern (Chrome, Edge, Firefox, Safari), atau pakai GitHub Pages.

## Menaruh di GitHub dan online lewat GitHub Pages

```bash
git init
git add index.html README.md
git commit -m "Brankas Berkas: enkripsi, hash, tanda tangan digital"
git branch -M main
git remote add origin https://github.com/Prihantowahyu/brankas-berkas.git
git push -u origin main
```

Lalu di GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**. Beberapa menit kemudian aplikasi bisa dibuka di `https://prihantowahyu.github.io/brankas-berkas/`.

## Batasan

- Berkas diproses di memori peramban, jadi berkas yang sangat besar (ratusan MB) bisa lambat.
- Tidak ada pemulihan kata sandi. Lupa kata sandi berarti berkas tidak bisa dibuka.
- Tanda tangan hanya terpercaya jika kunci publik didapat lewat jalur yang tepercaya. Cocokkan sidik jari kunci dengan pemiliknya.
- Proyek ini untuk belajar dan pemakaian sehari-hari, belum diaudit untuk kebutuhan yang sangat sensitif.

## Lisensi

MIT. Silakan dipakai dan dikembangkan.
