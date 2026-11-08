# Redis DevBox

Setup Docker Compose untuk Redis Server.

## 🚀 Fitur & Peningkatan

1. **Lightweight & Stable Image**: Menggunakan `redis:7-alpine`.
2. **Data Persistence**: Menggunakan volume `redis_data` dengan Append Only File (`--appendonly yes`) agar data tidak hilang saat restart container.
3. **Restart Policy**: `restart: unless-stopped` agar otomatis berjalan saat sistem restart.
4. **Health Check**: Pengecekan otomatis kesiapan Redis via `redis-cli ping`.

---

## ⚙️ Variabel Lingkungan (`.env`)

| Variabel | Default | Keterangan |
| :--- | :--- | :--- |
| `REDIS_PASSWORD` | `password` | Password otentikasi Redis |
| `HOST_REDIS_PORT` | `6379` | Port Redis di host (ubah jika port konflik) |
| `CONT_REDIS_PORT` | `6379` | Port default di dalam container Redis |

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

---

## 💻 Akses Redis CLI

Masuk langsung ke interaktif `redis-cli`:
```bash
docker exec -it redis redis-cli -a password
```

Beberapa perintah dasar:
```bash
# Test koneksi
ping

# Set key
set nama "Adit"

# Get key
get nama

# Cek memory & info
info memory

# Monitor aktivitas realtime
monitor
```

---

## 🌐 Koneksi dari Redis Insight (Host)

Karena Redis Insight sudah terinstall di host, Anda cukup menambahkan koneksi database baru:
- **Host**: `127.0.0.1` atau `localhost`
- **Port**: `6379` (sesuai `HOST_REDIS_PORT` di `.env`)
- **Password**: `password` (sesuai `REDIS_PASSWORD` di `.env`)
- **Database Alias**: `Local Redis`
