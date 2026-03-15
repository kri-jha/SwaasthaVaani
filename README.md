# 🎙️ SwaasthaVaani — Voice AI for Bharat

<div align="center">

![Track](https://img.shields.io/badge/Track%203-Indic%20Voice%20AI-02C39A?style=for-the-badge)
![Hackathon](https://img.shields.io/badge/Hackmatrix%202.0-IIT%20Patna-065A82?style=for-the-badge)
![Partner](https://img.shields.io/badge/Partner-Jilo%20Health-1C7293?style=for-the-badge)

**Multilingual Voice AI platform for automated patient engagement in Indian regional languages.**

*No smartphone. No internet. No large team. Just a voice call — and a patient who feels cared for.*

</div>

---

## 🩺 Problem

SME hospitals across India face a critical gap in post-discharge patient care:

- **No follow-up system** — hospitals lack resources to manually call every discharged patient
- **Language barrier** — patients in Tier 2/3 cities speak Hindi, Bhojpuri, and regional dialects
- **Unstructured data** — patient health reports are handwritten or unstructured PDFs with no insights
- **Bihar alone** has 38 districts with a doctor-patient ratio 40% below the national average

---

## 💡 Solution

SwaasthaVaani is a Voice AI platform that automatically calls patients post-discharge in their regional language, collects structured health responses, and displays real-time risk flags on a hospital dashboard.

```
Hospital Backend → Twilio Outbound Call → Patient's Phone
                                              ↓
                              Bhashini STT converts voice to text
                                              ↓
                          Python backend processes & risk-flags
                                              ↓
                         MongoDB stores structured JSON response
                                              ↓
                          React Dashboard alerts care team
```

---

## 📦 3 Core Deliverables

### 1. 🎙️ Voice AI Engine — Indic Language Support
- Automated outbound calls via **Twilio**
- Hindi + 10 regional languages via **Bhashini STT/TTS** (Govt of India API)
- **Hybrid input** — DTMF keypress (feature phones) + live voice (smartphones)
- Works on any basic phone — no smartphone or internet needed for patients

### 2. ⚙️ Patient Engagement Workflow Builder
- Hospital staff define call schedules, questions, and follow-up timelines
- Simple React UI — no technical knowledge required
- Supports post-discharge, chronic care, and medication reminder workflows

### 3. 📊 Structured Data Collection & Reporting Dashboard
- Every patient response stored as structured JSON
- Real-time risk flagging (LOW / MEDIUM / HIGH)
- Call history, compliance tracking, and auto-alerts for care teams

---

## 🔧 Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3.11 + FastAPI |
| Voice Calls | Twilio Voice API |
| Speech AI | Bhashini STT + TTS (Govt of India) |
| Database | MongoDB |
| Frontend | React + Vite |
| Real-time | WebSockets |

---

## 🗂️ Project Structure

```
SwaasthaVaani/
├── backend/
│   ├── main.py              # FastAPI app entry point
│   ├── routes/
│   │   ├── call.py          # Twilio call initiation & TwiML
│   │   ├── audio.py         # Bhashini STT integration
│   │   └── dashboard.py     # Patient data API
│   ├── models/
│   │   └── patient.py       # MongoDB schemas
│   └── utils/
│       ├── bhashini.py      # Bhashini API wrapper
│       └── risk.py          # Keyword-based risk flagging
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Dashboard.jsx    # Real-time patient dashboard
│   │   │   └── Workflow.jsx     # Call schedule builder
│   │   └── components/
│   │       ├── RiskCard.jsx     # Patient risk display
│   │       └── CallLog.jsx      # Call history table
│   └── package.json
├── scripts/
│   └── seed_patients.py     # Sample patient data
├── .env.example
├── requirements.txt
└── README.md
```

---

## 🚀 Setup & Installation

### Prerequisites
- Python 3.11+
- Node.js 18+
- MongoDB (local or Atlas)
- Twilio account (free trial works)
- Bhashini API key ([register here](https://bhashini.gov.in))

### Backend Setup

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/SwaasthaVaani.git
cd SwaasthaVaani

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Setup environment variables
cp .env.example .env
# Fill in your Twilio + Bhashini + MongoDB credentials

# Run the backend
uvicorn backend.main:app --reload --port 8000
```

### Frontend Setup

```bash
cd frontend
npm install
npm run dev
# Opens at http://localhost:5173
```

### Environment Variables

```env
# Twilio
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token
TWILIO_PHONE_NUMBER=+1XXXXXXXXXX

# Bhashini
BHASHINI_API_KEY=your_bhashini_key
BHASHINI_USER_ID=your_user_id

# MongoDB
MONGODB_URI=mongodb://localhost:27017/swaasthavaani

# App
BASE_URL=https://your-ngrok-url.ngrok.io
```

---

## 📞 How a Call Works

```
1. Hospital staff schedules a follow-up for "Ramesh Kumar"
2. SwaasthaVaani initiates outbound call via Twilio
3. Patient answers → AI speaks in Hindi via Bhashini TTS:
   "Namaste Ramesh ji! Kya aapne aaj dawai li? 
    Haan ke liye 1, Nahi ke liye 2 dabayein."
4. Patient presses 2 (No) → DTMF captured
5. AI asks: "Kya dard ho raha hai? Seedha bolein."
6. Patient says: "Haan, ghutne mein bahut dard hai"
7. Bhashini STT converts audio → text in ~2 seconds
8. Keyword match → HIGH RISK flagged
9. MongoDB stores structured response
10. Dashboard alerts care team instantly
Total time: ~60 seconds per patient
```

---

## 🌐 API Endpoints

```
POST  /api/call/initiate          → Start outbound call for a patient
POST  /api/call/incoming          → TwiML handler (Twilio webhook)
POST  /api/audio/transcribe       → Bhashini STT processing
GET   /api/dashboard/patients     → All patient responses
GET   /api/dashboard/risk/:level  → Filter by risk level
POST  /api/workflow/create        → Create call schedule
```

---

## ⚡ Key Differentiators

| Feature | WhatsApp Bot | IVR System | SwaasthaVaani |
|---|---|---|---|
| Feature phone support | ✗ | ✓ | ✓ |
| Regional language (10+) | ✗ | Limited | ✓ Bhashini |
| Live voice understanding | ✗ | ✗ | ✓ STT |
| Structured data output | ✗ | ✗ | ✓ JSON |
| Real-time dashboard | ✗ | ✗ | ✓ |
| Cost per call | ~₹5 | ~₹3 | ~₹2 |

---

## 📈 Scalability

- 1 server instance → **50 concurrent calls**
- **1,000 follow-ups/day** at ~₹2/call
- Bhashini API is **free** (Government of India)
- Offline fallback → pre-recorded IVR clips when internet unavailable
- Plugs into existing HMS via REST APIs — **Jilo Health partner hospitals ready**

---

## 🗺️ Roadmap

**Phase 1 — Now (Hackathon MVP)**
- Post-discharge follow-up calls
- Hindi + Bhojpuri + 3 regional languages
- DTMF + live voice hybrid input
- Risk dashboard for hospital admins

**Phase 2 — 3 Months**
- Appointment reminders & prescription refill alerts
- Multi-hospital onboarding
- WhatsApp + IVR channel parity

**Phase 3 — 6 Months**
- AI triage — pre-alert doctors based on symptoms
- All 10+ Bhashini languages live
- Full Jilo Health HMS integration
- Outcome analytics & reporting

---

## 👥 Team

| Name | Role | Institute |
|---|---|---|
| [Your Name] | Full Stack + AI | [Your Institute] |

---

## 📄 External APIs & Acknowledgements

- **[Bhashini](https://bhashini.gov.in)** — Government of India's Indic language AI platform
- **[Twilio](https://twilio.com)** — Voice call automation
- **[Jilo Health](https://jilohealth.com)** — Healthcare partner & problem statement

---

## 📬 Submission

- **Hackathon:** Hackmatrix 2.0 — IIT Patna
- **Track:** Track 3 — Indic Voice AI Patient Engagement
- **Submission Link:** [hackathon.jilohealth.com/register](https://hackathon.jilohealth.com/register)

---

<div align="center">
  <b>SwaasthaVaani — Voice AI for Bharat 🇮🇳</b><br/>
  <i>Built with ❤️ for India's healthcare gap</i>
</div>
