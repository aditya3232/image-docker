# Redpanda DevBox (Kafka-Compatible Streaming Platform)

Setup Docker Compose untuk Redpanda (alternatif Apache Kafka yang ringan dan cepat tanpa Zookeeper / JVM) beserta Redpanda Console (Web UI).

## 🚀 Fitur & Peningkatan

1. **Data Persistence**: Menggunakan named volume `redpanda_data:/var/lib/redpanda/data` sehingga topic, pesan, dan consumer offset tidak hilang saat container dihentikan/dibuat ulang.
2. **Manual Start (On-Demand)**: Restart policy dinonaktifkan secara default agar tidak memakan RAM/CPU secara otomatis saat Docker menyala.
3. **Health Check**: Pengecekan otomatis via perintah bawaan `rpk cluster health`.
4. **Console Web UI Terintegrasi**: Mengaktifkan integrasi Admin API di Redpanda Console untuk memantau cluster, topic, dan consumer groups secara visual di port `9002`.
5. **Dua Listener Jaringan (Internal & External)**:
   - **Internal (`redpanda:9092`)**: Digunakan oleh service lain di jaringan Docker.
   - **External (`localhost:19092`)**: Digunakan oleh aplikasi yang berjalan langsung di host komputer.

---

## ⚙️ Variabel Lingkungan (`.env`)

| Variabel | Default | Keterangan |
| :--- | :--- | :--- |
| `HOST_REDPANDA_KAFKA_PORT` | `19092` | Port broker Kafka untuk aplikasi di host |
| `HOST_REDPANDA_ADMIN_PORT` | `9644` | Port Redpanda Admin API |
| `HOST_REDPANDA_CONSOLE_PORT` | `9002` | Port Web UI Redpanda Console |

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

## 💻 Panduan CLI `rpk` (Redpanda Swiss-Army Knife)

Redpanda menyediakan tool CLI powerful bernama `rpk` di dalam containernya:

### 1. Cek Info & Kesehatan Cluster
```bash
docker exec -it redpanda rpk cluster info
docker exec -it redpanda rpk cluster health
```

### 2. Manajemen Topic
```bash
# Buat topic
docker exec -it redpanda rpk topic create order-events -p 3

# Lihat daftar topic
docker exec -it redpanda rpk topic list

# Cek detail topic
docker exec -it redpanda rpk topic describe order-events
```

### 3. Mengirim & Membaca Pesan
```bash
# Produce pesan interaktif (tekan Ctrl+C untuk selesai)
docker exec -it redpanda rpk topic produce order-events

# Consume pesan dari awal
docker exec -it redpanda rpk topic consume order-events --offset oldest
```

---

## 🌐 Akses Web Console

Buka di browser:
- [http://localhost:9002](http://localhost:9002)

Melalui web console Anda dapat melihat throughput cluster, melihat isi pesan di dalam topic, memantau consumer lag, dan membuat topic baru dengan mudah.

---

## 🔌 Koneksi dari Aplikasi

- **Jika aplikasi berjalan di Host:**
  - `bootstrap_servers`: `localhost:19092`
- **Jika aplikasi berjalan di Docker (Network: `redpanda_network`):**
  - `bootstrap_servers`: `redpanda:9092`

