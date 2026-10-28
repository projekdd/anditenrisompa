# Panduan Mengaktifkan Editor Admin

Editor tersedia di `https://anditenrisompa.com/admin/`. Editor memakai Decap CMS dan menyimpan perubahan langsung ke repositori GitHub. Dengan demikian, GitHub Pages akan menerbitkan perubahan otomatis.

## Yang sudah tersedia

- Form untuk mengubah profil, kartu informasi, berita, kontak, media sosial, dan foto.
- Penyimpanan konten di `content/site.json`.
- Folder unggahan gambar di `images/uploads`.
- Pesan commit otomatis setiap kali editor menyimpan perubahan.

## Konfigurasi sekali saja

Halaman admin belum dapat dipakai sebelum login GitHub disambungkan dengan aman. Ikuti langkah ini menggunakan akun pemilik repositori.

1. Buat akun Cloudflare gratis bila belum ada.
2. Buat dan terbitkan OAuth proxy Cloudflare Worker mengikuti template Decap: `https://github.com/sterlingwes/decap-proxy`.
3. Pada GitHub, buat OAuth App di **Settings → Developer settings → OAuth Apps**.
   - **Homepage URL:** URL Worker Cloudflare, misalnya `https://anditenrisompa-admin.nama-anda.workers.dev`.
   - **Authorization callback URL:** URL Worker yang sama ditambah `/callback`.
4. Simpan `Client ID` dan `Client secret` hanya sebagai **secret** di Cloudflare Worker. Jangan memasukkannya ke file website atau halaman publik.
5. Salin URL Worker yang sudah diterbitkan, lalu ubah baris `base_url` pada `admin/config.yml`. Ganti nilai contoh `https://GANTI-DENGAN-URL-WORKER.workers.dev` dengan URL tersebut.
6. Commit perubahan konfigurasi itu ke GitHub, kemudian buka `https://anditenrisompa.com/admin/` dan pilih **Login with GitHub**.

## Cara mengedit setelah aktif

1. Buka `https://anditenrisompa.com/admin/` dan login dengan akun GitHub yang memiliki akses tulis pada repositori.
2. Pilih **Konten Website → Profil, Berita, dan Kontak**.
3. Ubah isi yang diperlukan atau unggah foto.
4. Pilih **Publish**. Editor membuat commit di GitHub.
5. Tunggu GitHub Pages menerbitkan perubahan, biasanya beberapa menit.

## Catatan keamanan

- Hanya akun GitHub dengan akses tulis ke `projekdd/anditenrisompa` yang dapat menyimpan perubahan.
- Jangan pernah menyimpan GitHub token, Client ID rahasia, atau Client secret di `index.html`, `config.yml`, atau berkas publik lain.
- Periksa hasil di website setelah menerbitkan perubahan. Riwayat perubahan dan pemulihan versi tetap tersedia melalui riwayat commit GitHub.
