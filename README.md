# Student Management System - Project Pertemuan 11

[![Docker](https://img.shields.io/badge/Docker-Containerized-blue?logo=docker&logoColor=white)](https://www.docker.com/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14-blue?logo=postgresql&logoColor=white)](https://www.postgresql.org/)

Projek ini merupakan implementasi sistem manajemen mahasiswa dan autentikasi berbasis akun yang dikembangkan menggunakan **Spring Boot** dengan persistensi data **PostgreSQL**. Seluruh komponen aplikasi telah dikontainerisasi menggunakan **Docker Compose** guna memastikan konsistensi lingkungan pengembangan (*development*) di dalam WSL (Windows Subsystem for Linux) hingga siap di-*deploy*.

---

## Arsitektur Sistem & Alur Kerja

Sistem ini berjalan di atas arsitektur multi-kontainer yang terisolasi dalam satu jaringan virtual Docker:

* **App Service (`pertemuan11`)**: Backend Java Spring Boot yang mengurus enkripsi password (BCrypt), logika bisnis, dan penyajian antarmuka web.
* **Database Service (`db_mahasiswa`)**: Engine PostgreSQL 14 sebagai media penyimpanan tabel user dan profil mahasiswa.

### 🔌 Konfigurasi Teknis Jaringan & Port
* **Networking**: Komunikasi internal antar-kontainer menggunakan *hostname* `db`.
* **Data Persistence**: Menggunakan Docker Volume (`db_data`) agar data di PostgreSQL tidak hilang saat kontainer dimatikan.
* **Port Mapping**:
    * **Aplikasi Web**: Dapat diakses via browser lokal di `http://localhost:8000`
    * **Database PostgreSQL**: Terekspos ke *host* pada port `5434`

---

## Persyaratan Sistem

Pastikan perangkat Anda telah terpasang kakas (*tools*) berikut:
1.  **Docker Desktop** (yang terintegrasi aktif dengan backend WSL2).
2.  **Git** (untuk manajemen repositori).
3.  Browser modern (Chrome / Edge / Firefox) untuk mengakses aplikasi.

---

## 🚀 Panduan Deployment & Verifikasi Server

1.  **Clone Repositori**:
    ```bash
    git clone [URL-Repositori-Anda]
    cd [Nama-Folder-Projek]
    ```

2.  **Jalankan Docker Compose**:
    Nyalakan layanan di latar belakang menggunakan perintah:
    ```bash
    docker compose up -d
    ```

3.  **Pemeriksaan Log Runtime Aplikasi**:
    Berikut adalah bukti bahwa aplikasi Spring Boot berhasil melakukan inisialisasi *Entity Manager Factory* (JPA/Hibernate) dan server Tomcat berjalan sukses di port internal `8080` (di-mapping ke `8000` pada host):

    ![Spring Boot App Running Logs]<img width="1511" height="646" alt="Cuplikan layar 2026-05-19 140054" src="https://github.com/user-attachments/assets/dc64f74b-4f83-4e0e-83ec-07128ced0bf7" />


---

## Dokumentasi Antarmuka Web (UI)

Sistem ini menyediakan alur manajemen akun penuh, mulai dari pendaftaran data baru hingga masuk ke dalam dasbor profil terproteksi.

### 1. Halaman Pendaftaran Akun (`/register`)
Formulir untuk mendaftarkan akun baru yang mencakup Username, Password, Nama Lengkap, dan Alamat Domisili.

![Halaman Register](<img width="1917" height="873" alt="Cuplikan layar 2026-05-19 135730" src="https://github.com/user-attachments/assets/6129f764-96ff-4785-ac2c-48755462f0eb" />
)

### 2. Halaman Autentikasi (`/login`)
Gerbang masuk aman menggunakan kredensial akun yang telah didaftarkan sebelumnya.

![Halaman Login](<img width="1901" height="1006" alt="Cuplikan layar 2026-05-19 135700" src="https://github.com/user-attachments/assets/3f082b98-3c30-4121-9c84-fd7799308b07" />
)

### 3. Halaman Dasbor / Informasi Akun & Profil (`/home`)
Setelah sukses login, pengguna akan diarahkan ke halaman profil yang menampilkan informasi personal secara dinamis dari database.

![Halaman Home Dashboard](<img width="1915" height="953" alt="Cuplikan layar 2026-05-19 125148" src="https://github.com/user-attachments/assets/e2b87ea2-8458-4668-9197-5dbd31d9693c" />
)

---

## Validasi Data Persistence (PostgreSQL via WSL)

Untuk memastikan data terisi dengan benar di database relasional, kita dapat masuk ke dalam kontainer database melalui terminal WSL dengan perintah berikut:

```bash
docker exec -it db_mahasiswa psql -U praktikum_user -d praktikum_db

<img width="1436" height="662" alt="Cuplikan layar 2026-05-19 125104" src="https://github.com/user-attachments/assets/4487566b-794b-41ec-ac76-ad17cc223410" />
