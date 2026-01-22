# 🤖 Chatbot Customer Service

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)

![RASA](https://img.shields.io/badge/RASA-3.x-5a17ee.svg)

![Flask](https://img.shields.io/badge/Flask-2.x-000000.svg)

![Laragon](https://img.shields.io/badge/Laragon-Compatible-0e83cd.svg)

![License](https://img.shields.io/badge/License-MIT-green.svg)

> An intelligent customer service chatbot built with RASA NLP, Flask REST API, and modern web interface. Optimized for Laragon local development environment.
> 

## 📖 Overview

This project implements an **AI-powered Customer Service Chatbot** that leverages natural language understanding to provide automated, fast, and efficient customer support. The system handles various customer interactions including greetings, service inquiries, order tracking, complaints, and more.

### ✨ Key Features

- 🧠 Natural Language Understanding with RASA
- 🔄 RESTful API backend with Flask
- 💬 Modern responsive web interface
- 📊 Intent classification and entity extraction
- 🎯 Context-aware dialogue management
- 🚀 Laragon-ready configuration
- 📝 Conversation logging (optional)

### 🎯 Supported Intents

| Intent | Description | Example Input |
| --- | --- | --- |
| `greet` | User greetings | "halo", "selamat pagi" |
| `ask_services` | Service inquiries | "layanan apa saja?" |
| `check_order` | Order status tracking | "cek pesanan saya" |
| `give_order_number` | Provide order number | "nomor order A123" |
| `complain` | Customer complaints | "barang rusak" |
| `thank` | Gratitude expressions | "terima kasih" |
| `goodbye` | Conversation endings | "sampai jumpa" |

---

## 🛠️ Technology Stack

| Component | Technology | Purpose |
| --- | --- | --- |
| **NLP Engine** | RASA 3.x | Intent recognition & dialogue management |
| **Backend API** | Flask 2.x | RESTful API server |
| **Frontend** | HTML5 / CSS3 / JavaScript | User interface |
| **Web Server** | Laragon | Local hosting & development |
| **Database** | MySQL *(optional)* | Conversation logging |
| **Language** | Python 3.8+ | Core implementation |

---

## 📁 Project Structure

```
chatbot-project/
├── rasa-bot/                 # RASA NLP configuration
│   ├── domain.yml           # Bot domain definition
│   ├── nlu.yml              # Training data for NLU
│   ├── stories.yml          # Conversation flows
│   ├── rules.yml            # Response rules
│   └── config.yml           # Pipeline configuration
├── app.py                   # Flask API backend
├── requirements.txt         # Python dependencies
├── venv/                    # Virtual environment (gitignored)
├── css/
│   └── style.css           # UI styling
├── js/
│   └── chat.js             # Frontend chat logic
├── index.html              # Main chat interface
├── .gitignore
├── LICENSE
└── README.md

```

---

## 🚀 Getting Started

### Prerequisites

- **Laragon** (Full version recommended)
- **Python 3.8+** (included in Laragon or install separately)
- **Git** (for cloning repository)
- **VSCode** or any code editor

### Installation

### 1. **Clone Repository to Laragon**

Open Laragon Terminal (Right-click Laragon > Terminal) dan jalankan:

```bash
cd C:\laragon\www
git clone https://github.com/YOUR-USERNAME/chatbot-project.git
cd chatbot-project

```

### 2. **Create Virtual Environment**

Tetap di Laragon Terminal:

```bash
python -m venv venv

```

### 3. **Activate Virtual Environment**

```bash
venv\Scripts\activate

```

Pastikan muncul `(venv)` di awal prompt terminal.

### 4. **Install Dependencies**

```bash
pip install rasa
pip install flask flask-cors
pip install mysql-connector-python

```

*Note: Proses instalasi RASA memerlukan waktu beberapa menit.*

---

## ⚙️ Configuration & Setup

### Step 1: Train RASA Model

Dari terminal dengan venv aktif:

```bash
cd rasa-bot
rasa data validate

```

Jika validasi berhasil, lanjutkan training:

```bash
rasa train

```

Output: Model akan tersimpan di folder `models/`

### Step 2: Start RASA Server

Buka **Terminal 1** (Laragon Terminal):

```bash
cd C:\laragon\www\chatbot-project\rasa-bot
venv\Scripts\activate
rasa run --enable-api --cors "*"

```

✅ RASA Server running at: `http://localhost:5005`

### Step 3: Start Flask Backend

Buka **Terminal 2** (Terminal baru):

```bash
cd C:\laragon\www\chatbot-project
venv\Scripts\activate
python app.py

```

✅ Flask API running at: `http://localhost:8000`

### Step 4: Configure Laragon Virtual Host

**Otomatis (Recommended):**

Laragon akan otomatis membuat virtual host. Akses melalui:

```
http://chatbot-project.test

```

**Manual Setup (jika diperlukan):**

1. Klik kanan Laragon > Apache > `httpd-vhosts.conf`
2. Tambahkan konfigurasi:

```
<VirtualHost *:80>
    DocumentRoot "C:/laragon/www/chatbot-project/"
    ServerName chatbot-project.test
    <Directory "C:/laragon/www/chatbot-project/">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

```

1. Klik kanan Laragon > Tools > Edit hosts file
2. Tambahkan:

```
127.0.0.1    chatbot-project.test

```

1. Restart Apache di Laragon

### Step 5: Access Application

Buka browser dan akses:

```
http://chatbot-project.test

```

atau

```
http://localhost/chatbot-project

```

🎉 **Chatbot siap digunakan!**

---

## 💡 Usage

### Web Interface

1. Buka `http://chatbot-project.test` di browser
2. Ketik pesan di input field
3. Tekan Enter atau klik tombol Send
4. Bot akan merespon secara real-time

### API Testing dengan Postman

**Endpoint:** `POST http://localhost:8000/chat`

**Headers:**

```
Content-Type: application/json

```

**Request Body:**

```json
{
  "message": "halo"
}

```

**Response Example:**

```json
{
  "reply": "Halo! Ada yang bisa saya bantu hari ini?"
}

```

---

## 🔄 System Architecture

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Flask
    participant RASA

    User->>Browser: Ketik pesan
    Browser->>Flask: POST /chat
    Flask->>RASA: Kirim message ke NLP
    RASA->>RASA: Process intent & entities
    RASA->>Flask: Return response
    Flask->>Browser: JSON response
    Browser->>User: Tampilkan balasan bot
<img width="904" height="582" alt="image" src="https://github.com/user-attachments/assets/e517a783-ed53-4c19-800d-18ea55977b71" />


```

---

## 🧰 Troubleshooting

| Issue | Possible Cause | Solution |
| --- | --- | --- |
| Bot tidak merespon | RASA server tidak berjalan | Jalankan `rasa run --enable-api --cors "*"` |
| CORS error | Missing CORS configuration | Pastikan `CORS(app)` ada di `app.py` |
| 404 Not Found | Virtual host belum dikonfigurasi | Cek `http://chatbot-project.test` atau restart Laragon |
| Training fails | Invalid YAML syntax | Jalankan `rasa data validate` untuk cek error |
| API returns empty | Flask tidak aktif | Execute `python app.py` di terminal |
| Module not found | Virtual env tidak aktif | Aktifkan dengan `venv\Scripts\activate` |
| Port sudah digunakan | Aplikasi lain menggunakan port | Ubah port di `app.py` atau matikan aplikasi lain |

### Quick Fix Commands

```bash
# Cek status port
netstat -ano | findstr :5005
netstat -ano | findstr :8000

# Restart semua service
# 1. Stop RASA (Ctrl+C di terminal RASA)
# 2. Stop Flask (Ctrl+C di terminal Flask)
# 3. Restart Laragon Apache
# 4. Start ulang RASA dan Flask

```

---

## 📚 RASA Configuration Files

| File | Purpose | Description |
| --- | --- | --- |
| `nlu.yml` | Training data | Contoh intent dengan variasi input pengguna |
| `domain.yml` | Domain definition | Daftar intent, entities, slots, dan responses |
| `stories.yml` | Conversation flows | Alur percakapan untuk training dialogue |
| `rules.yml` | Response rules | Aturan respon otomatis dan fallback |
| `config.yml` | Pipeline config | Konfigurasi NLU dan policy pipeline |

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](https://claude.ai/chat/LICENSE) file for details.

---

## 👤 Author

**[Your Name]**

- GitHub: [@](https://github.com/your-username)**steven7281**
- Email: stevengsianipar@gmail.com
- Institution: Universitas Esa Unggul Jakarta
- Year: 2026

---

## 🙏 Acknowledgments

- [RASA Open Source](https://rasa.com/) - Conversational AI framework
- [Flask](https://flask.palletsprojects.com/) - Python web framework
- [Laragon](https://laragon.org/) - Portable development environment
- Community contributors and supporters
