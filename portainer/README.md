# Portainer CE DevBox

Setup Docker Compose untuk Portainer Community Edition (Container Management Web UI).

## 🚀 Fitur

1. **Host Docker Socket**: Terhubung ke `/var/run/docker.sock` untuk mengelola seluruh container Docker di host.
2. **Data Persistence**: Menggunakan named volume `portainer_database` untuk menyimpan pengaturan akun, template, dan konfigurasi.
3. **Restart Policy**: `restart: unless-stopped` agar otomatis berjalan saat reboot.

---

## ⚙️ Variabel Lingkungan (`.env`)

| Variabel | Default | Keterangan |
| :--- | :--- | :--- |
| `HOST_PORTAINER_HTTP_PORT` | `9003` | Port HTTP di host (diteruskan ke port 9000 container) |
| `HOST_PORTAINER_HTTPS_PORT` | `9443` | Port HTTPS di host (diteruskan ke port 9443 container) |

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

### 3. Restart Service (jika timeout inisialisasi)
```bash
docker compose restart portainer
```

---

## 🌐 Akses Web UI

Buka di browser:
- **HTTP**: [http://localhost:9003](http://localhost:9003)
- **HTTPS**: [https://localhost:9443](https://localhost:9443) *(Jika muncul peringatan SSL certificate, klik Advanced -> Proceed)*

> **⚠️ PENTING**: Portainer mewajibkan pembuatan password admin dalam waktu **5 menit** pertama sejak pertama kali dijalankan. Jika terlewat, Portainer akan otomatis shutdown demi keamanan. Cukup restart container untuk mereset timer:
> ```bash
> docker compose restart portainer
> ```

