# system_cinema

---

# 🎬 Database Cinema – MariaDB

Project ini berisi implementasi database sederhana untuk sistem cinema menggunakan **MariaDB**, lengkap dengan relasi dan contoh penggunaan `JOIN`.

---

## 📌 Struktur Database

### 1️⃣ Membuat Database

```sql
CREATE DATABASE db_cinema;
USE db_cinema;
```

---

### 2️⃣ Membuat Tabel

#### 🧑‍🎬 Tabel `sutradara`

```sql
CREATE TABLE sutradara (
    id_sutradara INT PRIMARY KEY AUTO_INCREMENT,
    nama_sutradara VARCHAR(100),
    negara_asal VARCHAR(50),
    tahun_lahir INT
);
```

---

#### 🎭 Tabel `genre`

```sql
CREATE TABLE genre (
    id_genre INT PRIMARY KEY AUTO_INCREMENT,
    nama_genre VARCHAR(50),
    keterangan TEXT
);
```

---

#### 🎥 Tabel `film`

```sql
CREATE TABLE film (
    id_film INT PRIMARY KEY AUTO_INCREMENT,
    judul_film VARCHAR(150),
    tahun_rilis INT,
    durasi_menit INT,
    id_sutradara INT,
    id_genre INT,
    FOREIGN KEY (id_sutradara) REFERENCES sutradara(id_sutradara),
    FOREIGN KEY (id_genre) REFERENCES genre(id_genre)
);
```

---

## 📥 Insert Data

### Data Sutradara

```sql
INSERT INTO sutradara (nama_sutradara, negara_asal, tahun_lahir) VALUES
('Christopher Nolan', 'Inggris', 1970),
('Joko Anwar', 'Indonesia', 1976),
('Bong Joon-ho', 'Korea Selatan', 1969),
('Steven Spielberg', 'Amerika Serikat', 1946),
('Greta Gerwig', 'Amerika Serikat', 1983),
('Denis Villeneuve', 'Kanada', 1967),
('Martin Scorsese', 'Amerika Serikat', 1942);
```

---

### Data Genre

```sql
INSERT INTO genre (nama_genre, keterangan) VALUES
('Action', 'Adegan aksi dan ketegangan'),
('Drama', 'Cerita konflik kehidupan'),
('Thriller', 'Misteri dan ketegangan psikologis'),
('Sci-Fi', 'Fiksi ilmiah dan teknologi'),
('Horror', 'Cerita menyeramkan'),
('Comedy', 'Unsur humor'),
('Adventure', 'Petualangan dan eksplorasi');
```

---

### Data Film

```sql
INSERT INTO film (judul_film, tahun_rilis, durasi_menit, id_sutradara, id_genre) VALUES
('Inception', 2010, 148, 1, 4),
('Pengabdi Setan', 2017, 107, 2, 5),
('Parasite', 2019, 132, 3, 2),
('Jurassic Park', 1993, 127, 4, 7),
('Barbie', 2023, 114, 5, 6),
('Dune', 2021, 155, 6, 4),
('The Irishman', 2019, 209, 7, 2);
```

---

# 🔗 JOIN Queries

## ✅ INNER JOIN

Menampilkan hanya data yang memiliki relasi di semua tabel.

```sql
SELECT 
    f.judul_film,
    f.tahun_rilis,
    f.durasi_menit,
    s.nama_sutradara,
    g.nama_genre
FROM film f
INNER JOIN sutradara s 
    ON f.id_sutradara = s.id_sutradara
INNER JOIN genre g 
    ON f.id_genre = g.id_genre;
```

📌 Hasil: Semua film tampil karena seluruh data memiliki relasi yang valid.

---

## ✅ LEFT JOIN

Menampilkan semua data dari tabel kiri (`film`) meskipun tidak memiliki pasangan.

```sql
SELECT 
    f.judul_film,
    s.nama_sutradara,
    g.nama_genre
FROM film f
LEFT JOIN sutradara s 
    ON f.id_sutradara = s.id_sutradara
LEFT JOIN genre g 
    ON f.id_genre = g.id_genre;
```

📌 Jika ada film tanpa sutradara/genre, kolom tersebut akan bernilai `NULL`.

---

## ✅ RIGHT JOIN

Menampilkan semua data dari tabel kanan (`sutradara`).

```sql
SELECT 
    f.judul_film,
    s.nama_sutradara
FROM film f
RIGHT JOIN sutradara s
    ON f.id_sutradara = s.id_sutradara;
```

📌 Jika ada sutradara tanpa film, maka `judul_film` akan bernilai `NULL`.

---

# 🗂 Relasi Antar Tabel

```
sutradara (1) ────< (∞) film (∞) >──── (1) genre
```

* Satu sutradara bisa memiliki banyak film
* Satu genre bisa memiliki banyak film
* Film memiliki satu sutradara dan satu genre

---

# 🚀 Teknologi

* MariaDB
* SQL
* Relational Database Concept

---

