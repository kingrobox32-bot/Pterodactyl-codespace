# Pterodactyl Panel - Private Server

Panel buat ngatur game server sendiri, contohnya Minecraft, FiveM, Rust, dll.
Jalannya pake Docker, jadi nggak perlu install ribet-ribet di laptop.
Dibuat buat main private bareng temen, bukan buat dijual.

## Apa Isinya?

- Panel Pterodactyl (website buat ngatur server)
- Database MariaDB (buat nyimpen data user & server)
- Redis Cache (biar panelnya ngebut)
- Dev Container (biar langsung jalan di GitHub Codespaces)

## Struktur File

- README.md = Penjelasan cara install
- docker-compose.yml = Mesin panelnya (database + panel + cache)
- .devcontainer/devcontainer.json = Setting biar bisa jalan di Codespaces

## Cara Install di Codespaces

1. Buka repo ini di GitHub
2. Klik tombol Code -> Codespaces -> Create codespace
3. Tunggu sampe Codespace kebuka
4. Buka Terminal, ketik ini satu-satu:

docker compose down -v
docker compose up -d
docker compose ps

5. Kalau udah 3-3nya Up, lanjut bikin database:

docker compose exec panel php artisan migrate --seed --force

6. Bikin akun admin:

docker compose exec panel php artisan p:user:make

Isi datanya:
- Email: bebas, contoh admin@admin.com
- Username: admin
- Password: bebas, yang gampang diinget
- Pilih Yes buat jadi admin

## Cara Buka Panel

Buka di browser:
http://localhost:8080

Login pake email + password yang tadi dibikin di p:user:make.
Kalau di Codespaces, klik tab PORTS -> cari port 8080 -> klik Open in Browser.

## Perintah Penting

docker compose up -d = Buat nyalain panel
docker compose down = Buat matiin panel
docker compose ps = Buat ngecek panel jalan atau nggak
docker compose logs -f panel = Buat liat log kalau ada error
docker compose down -v = Buat reset total dari nol, semua data kehapus

## Kalau Error

1. Panel nggak kebuka? Cek dulu: docker compose ps
Kalau ada yang Exit, restart: docker compose restart
2. Database belum siap? Tunggu 30 detik, terus: docker compose up -d
3. Mau mulai dari nol lagi? docker compose down -v lalu docker compose up -d

## Info Server

- Panel Port: 8080
- Database: MariaDB 10.11
- Cache: Redis Alpine
- Timezone: Asia/Jakarta
- URL: http://localhost:8080
