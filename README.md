# MEDWATCH — Drug Quality Verification Platform

## 🚀 Quick Start (with Docker)

### Prerequisites
- Docker Desktop installed and running

### 1. Clone / navigate to project
```bash
cd medwatch
```

### 2. Start everything here
```bash
docker-compose up --build
```

### 3. Run migrations (first time only)
```bash
docker-compose exec backend python manage.py migrate
docker-compose exec backend python manage.py createsuperuser
```

### 4. Access
| Service | URL |
|---|---|
| **API** | http://localhost:8000/api/v1/ |
| **Admin Panel** | http://localhost:8000/admin/ |

---

## 🔑 Key API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/v1/search/` | Search drug by batch + name |
| `POST` | `/api/v1/auth/otp/request/` | Send OTP |
| `POST` | `/api/v1/auth/otp/verify/` | Verify OTP, get JWT |
| `GET` | `/api/v1/auth/profile/` | User profile |
| `GET` | `/api/v1/regulations/` | List regulations |
| `GET` | `/api/v1/notifications/` | Notifications |

### Example Search Request
```json
POST /api/v1/search/
{
    "batch_no": "BN123456",
    "drug_name": "Paracetamol"
}
```

---

## 🏗️ Project Structure
```
medwatch/
├── backend/
│   ├── config/          # Django settings, URLs, Celery
│   ├── apps/
│   │   ├── drugs/       # Drug, Manufacturer, LabResult models
│   │   ├── labs/        # Lab model
│   │   ├── users/       # User, OTP, AdminUser
│   │   ├── search/      # Core search logic + SearchLog
│   │   ├── regulations/ # Regulations/circulars
│   │   └── notifications/ # Push notifications
│   ├── manage.py
│   ├── requirements.txt
│   └── Dockerfile
└── docker-compose.yml
```

---

## ⚙️ Environment Variables
Copy `.env.example` to `.env` and fill in:
- `MSG91_AUTH_KEY` — for OTP SMS
- `FIREBASE_SERVER_KEY` — for push notifications

---

## 📋 Tech Stack
- **Backend**: Django 4.2 + Django REST Framework
- **Database**: PostgreSQL 16 with pg_trgm fuzzy search
- **Cache/Queue**: Redis + Celery
- **Auth**: OTP-based JWT (no passwords)
- **Notifications**: Firebase FCM
