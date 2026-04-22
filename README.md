<div align="center">

# 🩺 Electronic Medical Record (EMR)

### A secure, lightweight EMR for clinics — patient records, appointments, prescriptions, and reports  
**Fast | Audit-ready | Easy to deploy**

[![Stars](https://img.shields.io/github/stars/DhanushGroot/Electronic-Medical-Record?style=for-the-badge&logo=github)](https://github.com/DhanushGroot/Electronic-Medical-Record/stargazers)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![Build](https://img.shields.io/badge/build-passing-brightgreen?style=for-the-badge)](https://github.com/DhanushGroot/Electronic-Medical-Record/actions)
[![Version](https://img.shields.io/badge/version-1.0.0-blue?style=for-the-badge)](./)

</div>

---

## ✨ Live Demo / Preview

<div align="center">

**Preview animation**

![EMR Preview](/assets/demo.gif)

</div>

---

## 🚀 What it does

Electronic Medical Record is a focused, clinician-first web app that lets small clinics manage patient data, appointments, prescriptions, and billing with privacy and traceability in mind.

- Centralized patient profiles with visit history
- Appointment scheduling and reminders
- Prescription generation and printable RX
- Basic billing & invoice generation
- Role-based access (Admin / Clinician / Reception)

---

## 🔑 Key Features

- 🔒 Secure session-based authentication and role permissions  
- 🧾 Patient-centric records with chronological visit log  
- 📅 Appointment calendar & availability checks  
- 💊 Prescription templates + PDF export/print  
- 💳 Billing summary & printable invoices  
- 📈 Simple reports (visits per period, revenue)  
- ⚙️ Lightweight PHP codebase — easy to self-host

---

## 🛠 Tech Stack

| Layer | Technology |
|------:|:-----------|
| Backend | PHP (Core) |
| Database | MySQL / MariaDB |
| Frontend | HTML, CSS (responsive), minimal JavaScript |
| Styling | Custom CSS — optionally Bootstrap compatible |
| Email | PHP mail() / SMTP (configurable) |
| Deployment | Apache / Nginx or Docker |

---

## ⚙️ Architecture

```
Electronic-Medical-Record

├── public/                  → Document root (index.php, assets)
│   ├── index.php
│   ├── assets/
│   │   ├── css/
│   │   └── demo.gif
│   └── uploads/             → user uploads (scans, attachments)
│
├── src/                     → Application source (MVC-style)
│   ├── controllers/
│   ├── models/
│   └── views/
│
├── routes/                  → Simple routing / API endpoints
│   └── api.php
│
├── config/
│   └── config.php           → DB credentials, SMTP, app settings
│
├── scripts/                 → utilities (migrations, seeders)
├── sql/
│   └── schema.sql
└── server/                   → optional Express / workers (if used)
```

### Data flow

User Browser → public/index.php → Router → Controller → Model → MySQL → Controller → View → Browser

<details>
<summary>🔎 Advanced: Core endpoints & roles</summary>

- POST /auth/login — session-based login (roles: admin, clinician, receptionist)  
- GET /patients — list & search (clinician/receptionist)  
- GET /patient/{id} — full record & visits (clinician)  
- POST /appointments — schedule / check conflicts (receptionist/clinician)  
- POST /prescriptions — create & export (clinician)  
- POST /billing/invoice — generate invoice (receptionist/admin)

</details>

---

## 📦 Installation (Quick)

Choose one: Local PHP stack or Docker.

### Prerequisites
- PHP 7.4+ with PDO MySQL
- MySQL / MariaDB
- Composer (optional)
- Web server (Apache/Nginx) or Docker

### Option A — Local (PHP + MySQL)

```bash
# clone
git clone https://github.com/DhanushGroot/Electronic-Medical-Record.git
cd Electronic-Medical-Record

# copy sample config
cp config/config.sample.php config/config.php

# edit config/config.php with DB & SMTP details

# import database schema
mysql -u root -p emr_db < sql/schema.sql

# serve (Apache or PHP built-in for testing)
php -S 0.0.0.0:8000 -t public
# visit http://localhost:8000
```

### Option B — Docker (recommended for reproducible env)

Create a docker-compose.yml (example) and run:

```bash
# start services
docker-compose up -d

# run migrations (if provided)
docker exec -it emr_app php scripts/migrate.php
```

---

## 💻 Usage Examples

### Example: create a patient (curl)
```bash
curl -X POST http://localhost:8000/api/patients \
  -H "Content-Type: application/json" \
  -d '{"first_name":"Asha","last_name":"Kumar","dob":"1988-05-10","phone":"9876543210"}'
```

### Example: login (PHP)
```php
// simple client-side fetch
$ch = curl_init('http://localhost:8000/auth/login');
curl_setopt($ch, CURLOPT_POSTFIELDS, ['username'=>'reception','password'=>'secret']);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);
```

---

## 🔧 Configuration

Edit config/config.php (example keys):

```php
return [
  'db' => [
    'host' => '127.0.0.1',
    'name' => 'emr_db',
    'user' => 'emr_user',
    'pass' => 'secret'
  ],
  'smtp' => [
    'host' => 'smtp.example.com',
    'port' => 587,
    'user' => 'noreply@example.com',
    'pass' => 'smtp-password'
  ],
  'app' => [
    'base_url' => 'http://localhost:8000'
  ]
];
```

<details>
<summary>📁 Database: sample schema (expand)</summary>

- patients (id, first_name, last_name, dob, phone, created_at)  
- visits (id, patient_id, clinician_id, notes, diagnosis, created_at)  
- appointments (id, patient_id, clinician_id, start_at, end_at, status)  
- prescriptions (id, visit_id, medication, dosage, instructions)  
- invoices (id, visit_id, amount, status, created_at)  
- users (id, username, password_hash, role)

</details>

---

## 🗺 Roadmap

- [x] Core patient records CRUD  
- [x] Appointments & basic calendar  
- [x] Prescriptions & printable RX  
- [x] Billing & invoice PDF export  
- [ ] Audit trails & activity logs (HIPAA-conscious)  
- [ ] Role-based access control refinement  
- [ ] Two-factor auth & SSO options  
- [ ] Data export / backup tools  
- [ ] Mobile-friendly UI improvements

---

## 🤝 Contributing

We welcome improvements, bug fixes, and integrations.

1. Fork the repo  
2. Create branch: git checkout -b feat/your-feature  
3. Run tests / validate locally  
4. Commit with clear message and open a PR

Please include migration scripts and a short description of data changes with PRs.

---

## 📈 Metrics & Badges

<div align="center">

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=DhanushGroot&repo=Electronic-Medical-Record&show_icons=true&theme=dark&hide_border=true)
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=DhanushGroot&repo=Electronic-Medical-Record&layout=compact&theme=dark&hide_border=true)

<br />

![GitHub Streak](https://github-readme-streak-stats.herokuapp.com/?user=DhanushGroot&theme=dark&hide_border=true)
![Profile Views](https://komarev.com/ghpvc/?username=DhanushGroot&color=49c5b6)

</div>

---

## 📝 License

MIT — see the LICENSE file for details.

---

## ✉️ Contact

If you want to test, audit, or integrate this EMR, open an issue or reach out via GitHub: [DhanushGroot](https://github.com/DhanushGroot)

---

Made with care — lightweight & clinic-ready.
