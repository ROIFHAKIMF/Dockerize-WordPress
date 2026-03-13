# Dockerize WordPress with MySQL and Redis

## 📌 Deskripsi

Project ini merupakan implementasi **WordPress CMS menggunakan Docker Compose** dengan tiga container utama:

* **WordPress** sebagai CMS
* **MySQL** sebagai database
* **Redis** sebagai object cache

Tujuan dari project ini adalah untuk mempelajari konsep **multi-container orchestration**, **service dependency**, **Docker networking**, serta **data persistence menggunakan volume**.

---

# 🐳 Arsitektur Container

Project ini menggunakan 3 container:

* **wordpress** → aplikasi web
* **mysql** → database
* **redis** → caching

Alur komunikasi container:

User → WordPress → MySQL
User → WordPress → Redis

Semua container berjalan dalam satu network Docker sehingga dapat saling berkomunikasi menggunakan nama service.

---

# ⚙️ Cara Menjalankan Project

### 1. Clone repository

```
git clone https://github.com/ROIFHAKIMF/Dockerize-WordPress.git
cd docker-wordpress
```

### 2. Jalankan Docker Compose

```
docker compose up -d
```

Docker akan otomatis:

* menarik image WordPress
* menarik image MySQL
* menarik image Redis
* menjalankan 3 container sekaligus

---

### 3. Akses WordPress

Buka browser dan akses:

```
http://localhost:8000
```

Kemudian lakukan instalasi WordPress melalui web installer.

---

# 🧪 Testing

### 1. Cek Container Running

```
docker ps
```

Harus muncul 3 container:

* wordpress
* mysql
* redis

---

### 2. Test Redis

Masuk ke container Redis:

```
docker exec -it docker-wordpress-redis-1 redis-cli
```

Lalu jalankan:

```
ping
```

Output yang diharapkan:

```
PONG
```

---

### 3. Test Data Persistence

Jalankan:

```
docker compose down
docker compose up -d
```

Jika WordPress masih memiliki data sebelumnya, berarti volume berhasil menyimpan data database.

---

# 📂 Struktur Project

```
docker-wordpress
│
├── docker-compose.yml
├── README.md
└── screenshots
```

---

# 📸 Screenshot

Berikut screenshot hasil implementasi:

* WordPress Installation Page
* WordPress Dashboard
* Docker Containers Running
* Redis CLI Ping Test

---

# ❓ Jawaban Pertanyaan

### 1. Kenapa perlu volume untuk MySQL?

Volume digunakan agar data database tidak hilang ketika container dihentikan atau dihapus. Data akan tetap tersimpan di host machine.

---

### 2. Apa fungsi `depends_on`?

`depends_on` digunakan untuk memastikan urutan startup container. Dalam project ini WordPress harus menunggu MySQL dan Redis berjalan terlebih dahulu sebelum dijalankan.

---

### 3. Bagaimana WordPress container connect ke MySQL?

WordPress terhubung ke MySQL menggunakan environment variable:

```
WORDPRESS_DB_HOST=mysql
```

Docker Compose secara otomatis membuat network sehingga container dapat saling berkomunikasi menggunakan nama service.

---

### 4. Apa keuntungan menggunakan Redis untuk WordPress?

Redis digunakan sebagai **object cache** yang menyimpan hasil query database di memory sehingga:

* mengurangi beban database
* mempercepat response website
* meningkatkan performa WordPress

---

# 📚 Teknologi yang Digunakan

* Docker
* Docker Compose
* WordPress
* MySQL
* Redis

---

# 👨‍💻 Author

Nama: **Roif**
Program Studi: **Teknik Informatika**
