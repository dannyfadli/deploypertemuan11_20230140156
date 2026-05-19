# 🚀 Student Management System - Project Pertemuan 11

[![Docker](https://img.shields.io/badge/Docker-Containerized-blue?logo=docker&logoColor=white)](https://www.docker.com/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14-blue?logo=postgresql&logoColor=white)](https://www.postgresql.org/)

Projek ini merupakan implementasi sistem manajemen mahasiswa yang dikembangkan menggunakan **Spring Boot** dengan basis data **PostgreSQL**. Seluruh komponen aplikasi telah dikontainerisasi menggunakan **Docker Compose** untuk memastikan lingkungan pengembangan dan produksi yang konsisten dan mudah di-*deploy*.

---

## 🏗️ Arsitektur Sistem

Sistem ini terdiri dari dua layanan utama yang berjalan dalam jaringan virtual Docker yang terisolasi:

* **App Service (`pertemuan11`)**: Aplikasi backend berbasis Java Spring Boot.
* **Database Service (`db_mahasiswa`)**: Menggunakan PostgreSQL 14 untuk persistensi data.

### Konfigurasi Teknis
* **Networking**: Layanan berkomunikasi melalui nama *host* `db` di jaringan internal Docker.
* **Data Persistence**: Menggunakan Docker Volume (`db_data`) untuk memastikan data tetap aman meskipun kontainer dihentikan atau dihapus.
* **Port Mapping**:
    * App: `localhost:8000` -> `8080` (Container)
    * DB: `localhost:5434` -> `5432` (Container)

---

## 🛠️ Persyaratan Sistem

Pastikan *tools* berikut telah terinstal di komputer Anda:
1.  **Docker Desktop** (dengan dukungan WSL2 jika menggunakan Windows).
2.  **Git**.
3.  **Postman** atau browser untuk pengujian API.

---

## 🚀 Panduan Deployment

Ikuti langkah berikut untuk menjalankan aplikasi di lingkungan lokal Anda:

1.  **Clone Repositori**:
    ```bash
    git clone [URL-Repositori-Anda]
    cd [Nama-Folder-Projek]
    ```

2.  **Jalankan dengan Docker Compose**:
    Pastikan Docker Desktop sudah berjalan, kemudian eksekusi perintah:
    ```bash
    docker compose up -d
    ```

3.  **Verifikasi Kontainer**:
    Pastikan kedua kontainer berjalan dengan perintah:
    ```bash
    docker compose ps
    ```

---

## 🔍 Database & Dokumentasi

### Akses ke Database
Jika Anda perlu melakukan pemeriksaan data secara langsung di dalam kontainer:
```bash
docker exec -it db_mahasiswa psql -U praktikum_user -d praktikum_db
<img width="1892" height="1066" alt="image" src="https://github.com/user-attachments/assets/66a4b4ee-ee7d-4227-a5bf-a680b852b226" />
