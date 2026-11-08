# PostgreSQL DevBox

Setup Docker Compose untuk PostgreSQL Database Server.

## 🚀 Fitur & Peningkatan

1. **Volume Path yang Benar**: Menggunakan `pgdata:/var/lib/postgresql/data` (direktori standar resmi PostgreSQL) agar data tersimpan aman dan tidak rusak.
2. **Pinned Version**: Menggunakan `postgres:16-alpine` (ringan ~140 MB vs ~450 MB versi standar) dan mencegah resiko *breaking change* versi baru yang sering terjadi jika menggunakan tag `:latest`.
3. **Environment Fleksibel**: Kredensial dan port dikonfigurasi melalui file `.env`.
4. **Health Check**: Dilengkapi pengecekan berkala kesiapan database dengan `pg_isready`.
5. **Manual On-Demand**: Restart policy dinonaktifkan secara default agar hemat RAM/CPU di mesin lokal dan hanya berjalan saat Anda menyalakannya secara manual.

---

## ⚙️ Variabel Lingkungan (`.env`)

| Variabel | Default | Keterangan |
| :--- | :--- | :--- |
| `POSTGRES_USER` | `postgres` | Username superuser database |
| `POSTGRES_PASSWORD` | `password` | Password user database |
| `POSTGRES_DB` | `appdb` | Nama database awal yang otomatis dibuat |
| `HOST_POSTGRES_PORT` | `5432` | Port di host komputer Anda |
| `CONT_POSTGRES_PORT` | `5432` | Port internal container |

---

## 🛠️ Cara Menjalankan

### 1. Menjalankan Service di Background
```bash
docker compose up -d
```

### 2. Menghentikan Service
```bash
docker compose down
```

### 3. Melihat Log Realtime
```bash
docker compose logs -f
```

---

## 💻 Akses Database & CLI

### 1. Masuk ke Interactive CLI (`psql`)
```bash
docker exec -it postgres psql -U postgres -d appdb
```

Perintah umum di dalam `psql`:
- `\l` : Melihat daftar database
- `\dt` : Melihat daftar tabel
- `\d <nama_tabel>` : Melihat struktur tabel
- `\q` : Keluar dari psql

### 2. Backup Database (Dump)
```bash
docker exec -t postgres pg_dump -U postgres appdb > backup.sql
```

### 3. Restore Database
```bash
cat backup.sql | docker exec -i postgres psql -U postgres -d appdb
```

---

## 🌐 Koneksi dari Host GUI Client (DBeaver / DataGrip / TablePlus)

- **Host:** `localhost` atau `127.0.0.1`
- **Port:** `5432` (sesuai `HOST_POSTGRES_PORT`)
- **Database:** `appdb` (sesuai `POSTGRES_DB`)
- **Username:** `postgres` (sesuai `POSTGRES_USER`)
- **Password:** `password` (sesuai `POSTGRES_PASSWORD`)

