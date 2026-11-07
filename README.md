# 🌤️ Cuaca Jakarta

Aplikasi prakiraan cuaca Jakarta yang dikembangkan menggunakan **Ionic Framework, Vue.js, TypeScript, dan Axios** dengan memanfaatkan data dari **Open-Meteo API**.

## 📌 Deskripsi Proyek

Aplikasi ini dibuat untuk menampilkan informasi prakiraan suhu udara Jakarta berdasarkan data yang diperoleh dari Open-Meteo API.

Data ditampilkan dalam bentuk tabel agar mudah dibaca dan dipahami oleh pengguna.

Proyek ini merupakan pengerjaan Tugas 2 mata kuliah **Pemrograman Berbasis Piranti Bergerak**, Universitas Terbuka.

## ✨ Fitur Aplikasi

- Menampilkan prakiraan cuaca Jakarta.
- Mengambil data dari Open-Meteo API.
- Menampilkan waktu pengukuran per jam.
- Menampilkan temperatur dalam satuan Celsius (°C).
- Menampilkan seluruh data yang diterima dari API.
- Tabel dapat digulir untuk melihat data lainnya.
- Tampilan menggunakan tema pink pastel.

## 🛠️ Teknologi yang Digunakan

- Ionic Framework
- Vue.js
- TypeScript
- Axios
- HTML
- CSS
- Open-Meteo API

## 🌐 Sumber Data API

Aplikasi menggunakan Open-Meteo API dengan koordinat Jakarta:

- Latitude: -6.2
- Longitude: 106.8
- Parameter: `temperature_2m`

URL API:

https://api.open-meteo.com/v1/forecast?latitude=-6.2&longitude=106.8&hourly=temperature_2m

## 🚀 Cara Menjalankan Proyek

Pastikan Node.js, npm, dan Ionic CLI sudah terpasang.

**1. Clone repository**

```bash
git clone https://github.com/cittt114/cuaca-jakarta.git
```

**2. Masuk ke folder proyek**

```bash
cd cuaca-jakarta
```

**3. Instal dependensi**

```bash
npm install
```

**4. Jalankan aplikasi**

```bash
ionic serve
```

Aplikasi dapat dibuka melalui alamat lokal yang ditampilkan pada terminal.

## 📂 Halaman Utama

Halaman utama aplikasi berada pada:

`src/views/HomePage.vue`

File tersebut berisi tampilan aplikasi, proses pengambilan data menggunakan Axios, serta pengaturan desain menggunakan CSS.

## 👩‍💻 Pengembang

**Citra Dewi**

Program Studi Sistem Informasi  
Universitas Terbuka

## 📄 Lisensi

Proyek ini dibuat untuk keperluan pembelajaran dan tugas akademik.
