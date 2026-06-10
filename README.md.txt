# UTS Communication Protocol - Case A: REST API JSON
### Program Studi Sains Data - Kelas Reguler (Kelompok 03)

Repositori ini dibuat untuk memenuhi tugas UTS kelompok pada mata kuliah Communication Protocol. Praktikum ini berfokus pada pengujian REST API berbasis JSON, analisis penanganan metode HTTP (GET dan POST), serta pembuktian dan troubleshooting transaksi paket data jaringan menggunakan Wireshark.

---

## 1. Anggota Kelompok & Pembagian Role
Setiap anggota kelompok bertanggung jawab penuh atas pemenuhan teknis dan penjelasan *evidence* sesuai dengan pembagian peran berikut:

* **Abda** — Project Manager & Data Analyst (Role 4 & Kontributor Analisis)
* **Muflih Fuadi** — API Tester (Role 1: Postman Specialist)
* **Afniana (Afni)** — Wireshark Packet Capture & Network Specialist (Role 2)
* **Tasyel Triajanisya** — Github Administrator (Role 4: Repository Management & Version Control)

---

## 2. Ringkasan Kasus & Arsitektur Sistem
Kelompok kami memilih **Case A - REST API JSON**. Skenario praktikum dijalankan menggunakan dua skema arsitektur server pengujian sebagai pembanding:
1. **Server Lokal:** Berjalan pada alamat lokal `http://127.0.0.1:8088` menggunakan *Communication Protocols Demo App*.
2. **Mock Server Jaringan:** Berjalan secara online memanfaatkan *Beeceptor Mock API* endpoint untuk simulasi publik.

---

## 🚀 3. Alur Pengujian API & Endpoint (Evidence Role 1)
Pengujian dilakukan melalui kombinasi request GET dan POST untuk memastikan bahwa data terkirim dan terbaca dengan sempurna oleh server. Urutan ini digunakan karena GET pertama berfungsi untuk mengecek data awal, POST digunakan untuk mengirim data JSON, dan GET terakhir digunakan untuk membaca kembali evidence yang sudah dikirim.

Berikut adalah urutan eksekusi pengujian:

| No | Method | Endpoint / URI | Tujuan Pengujian | Target Status Code |
|:--:|:------:|:---------------|:-----------------|:------------------:|
| 1  | `GET`  | `/api/uts/orders` | Mengambil data orders awal pada sistem | `200 OK` |
| 2  | `POST` | `/api/uts/evidence` | Mengirim payload JSON Struktur Peran Kelompok | `201 Created` |
| 3  | `POST` | `/api/uts/evidence` | Mengirim payload JSON Persentase Angka Kontribusi | `201 Created` |
| 4  | `GET`  | `/api/webhook/inbox` | Membaca dan memvalidasi kembali seluruh berkas masuk | `200 OK` |

### Struktur Payload JSON yang Ditransmisikan

#### A. Payload Struktur Internal Kelompok (`src/payload_struktur.json`):
```json
{
  "struktur_kelompok": "role_internal",
  "project_manager": "abda",
  "api_tester": "muflih",
  "wireshark_packet_capture": ["muflih", "abda", "afni"],
  "data_analyst": "abda",
  "github_administrator": ["tasyel", "afni"]
}

{
  "nama_data": "kontribusi",
  "project_manager": 10,
  "api_tester": 10,
  "wireshark_packet_capture": 10,
  "data_analyst": 10,
  "github_administrator": 10
}