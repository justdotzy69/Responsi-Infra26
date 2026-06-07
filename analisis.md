

# Analisis

## Masalah 1
* **Gejala:** Muncul pesan *error* `yaml: line 4, column 8: mapping values are not allowed in this context` saat menjalankan *docker compose*.
* **Penyebab:** Kata kunci `services` pada file `docker-compose.yml` kurang tanda titik dua (`:`), yang menyebabkan konfigurasi tidak terdeteksi dengan baik.
* **Solusi:** Menambahkan tanda titik dua sehingga menjadi `services:` dan merapikan baris kodenya.


## Masalah 2
* **Gejala:** Gagal membuat *container* dengan pesan *error*: `unable to prepare context`
* **Penyebab:** Terdapat *typo* pada *path context* milik *service* `web3` di file `docker-compose.yml`, yaitu tertulis `/web33` yang seharusnya `./web3`. Hal ini menyebabkan *path* yang dikonfigurasi tidak terbaca.
* **Solusi:** Mengubah *context* milik *service* `web3` dari `/web33` menjadi `./web3`.

---

## Masalah 3
* **Gejala:** Proses *build* gagal dengan pesan *error*: `failed to resolve source metadata for docker.io/library/php:8.2-apach: not found.`.
* **Penyebab:** Terdapat *typo* pada nama *base image* resmi di baris pertama file `Dockerfile` milik folder `web1`, `web2`, dan `web3`. Penulisan `FROM php:8.2-apach` kurang huruf "e", sehingga Apache tidak terdeteksi.
* **Solusi:** Mengubah baris pertama di ketiga file `Dockerfile` tersebut menjadi `FROM php:8.2-apache`.

---

## Masalah 4
* **Gejala:** *Container* berhasil berjalan, namun saat diuji menggunakan perintah `8080` di port iximiuz, selalu muncul *error* `Connection refused`.
* **Penyebab:** Terdapat sisa karakter *backtick* di bagian atas dan bawah file `nginx.conf`. Selain itu, terdapat *typo* penulisan target *server* seperti `web11:80` dan `web3:8080` yang menyebabkan koneksi tidak diterima.
* **Solusi:** Menghapus karakter *backtick* pada file `nginx.conf` dan memperbaiki *typo* pada blok *upstream backend* menjadi:
```nginx
upstream backend {
    server web1:80;
    server web2:80;
    server web3:80;
}
