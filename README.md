# ⚠️ PhishCatch Kiosk

An interactive cybersecurity web app where users paste suspicious emails, SMS messages, or links to receive an instant AI-powered phishing threat analysis.

**Powered by:** Streamlit · NVIDIA NIM (Llama 3.1) · Firebase Firestore

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io)

---

## 🚀 Features

| Feature | Detail |
|---|---|
| ⚡ Instant AI Analysis | Uses NVIDIA Llama 3.1 8B (fast) → 70B (accurate) fallback |
| 🎯 Structured Results | Threat Level, Risk Score, Red Flags, Expert Advice |
| 🔥 Cloud Logging | Scans auto-logged to Firebase Firestore |
| 🛡️ Secure Secrets | No hardcoded keys — uses Streamlit secrets |
| 🔁 Smart Retry | Auto-retries with fallback model on failure |

---

## 🛠️ Tech Stack

- **Python 3.10+**
- **Streamlit** — UI framework
- **NVIDIA NIM API** — Llama 3.1 8B / 70B Instruct
- **Firebase Firestore** — scan logging database

---

## ⚙️ Local Development Setup

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/phishcatch-kiosk.git
cd phishcatch-kiosk
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Create local secrets file
Create the file `.streamlit/secrets.toml` (this is git-ignored):
```toml
NVIDIA_API_KEY = "nvapi-your-key-here"

FIREBASE_KEY = """{
  "type": "service_account",
  "project_id": "your-project-id",
  ...full firebase-key.json content here...
}"""
```

### 4. Run locally
```bash
streamlit run app.py
```

---

## 🚀 Streamlit Cloud Deployment (Step-by-Step)

### Step 1 — Create a GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Name it `phishcatch-kiosk`
3. Set to **Public** (required for free Streamlit Cloud)
4. Click **Create repository**

### Step 2 — Push Your Code

Run these commands in your project folder:
```bash
git init
git add app.py requirements.txt README.md .gitignore
git commit -m "Initial commit: PhishCatch Kiosk"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/phishcatch-kiosk.git
git push -u origin main
```

> ⚠️ **Do NOT add** `.streamlit/secrets.toml`, `firebase-key.json`, or `.env` — they are git-ignored for security.

### Step 3 — Deploy on Streamlit Cloud

1. Go to **[share.streamlit.io](https://share.streamlit.io)** and sign in with GitHub
2. Click **"New app"**
3. Select your repository: `YOUR_USERNAME/phishcatch-kiosk`
4. Set **Main file path**: `app.py`
5. Click **"Advanced settings"** before deploying

### Step 4 — Add Secrets in Streamlit Cloud

In the **Advanced settings → Secrets** text box, paste exactly:

```toml
NVIDIA_API_KEY = "nvapi-your-actual-nvidia-key-here"

FIREBASE_KEY = """{
  "type": "service_account",
  "project_id": "axial-reference-483416-q6",
  "private_key_id": "your-key-id",
  "private_key": "-----BEGIN PRIVATE KEY-----\nYOUR_PRIVATE_KEY_HERE\n-----END PRIVATE KEY-----\n",
  "client_email": "firebase-adminsdk-fbsvc@your-project.iam.gserviceaccount.com",
  "client_id": "your-client-id",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-fbsvc%40your-project.iam.gserviceaccount.com",
  "universe_domain": "googleapis.com"
}"""
```

> 💡 **Tip:** Copy the entire contents of your `firebase-key.json` file between the triple quotes of `FIREBASE_KEY`.

6. Click **"Deploy!"**

---

## 🐛 Common Errors & Fixes

| Error | Cause | Fix |
|---|---|---|
| `KeyError: 'NVIDIA_API_KEY'` | Secret not added in Streamlit Cloud | Add secret in App Settings → Secrets |
| `🔑 Invalid API Key` | Wrong NVIDIA key | Get fresh key from [build.nvidia.com](https://build.nvidia.com) |
| `⏱️ Request timed out` | NVIDIA API under load | Wait 30s and try again — app auto-retries |
| Firebase init error | Malformed JSON in `FIREBASE_KEY` | Ensure the JSON is valid and inside triple quotes `"""` |
| `DefaultCredentialsError` | Firebase already initialized | Handled automatically by `_apps` check |
| App crashes on deploy | `python-dotenv` missing | Already removed from requirements.txt ✅ |

---

## 📂 Project Structure

```
phishcatch-kiosk/
├── app.py                  # Main Streamlit app
├── requirements.txt        # Python dependencies
├── README.md               # This file
├── .gitignore              # Excludes secrets & cache
└── .streamlit/
    └── secrets.toml        # Local secrets (git-ignored)
```

---

## 🔐 Getting API Keys

### NVIDIA NIM API Key
1. Go to [build.nvidia.com](https://build.nvidia.com)
2. Sign in / create account
3. Go to **API Keys** → **Generate Key**
4. Key starts with `nvapi-...`

### Firebase Service Account Key
1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your project → **Project Settings** → **Service Accounts**
3. Click **Generate new private key**
4. Download the JSON file — this is your `firebase-key.json`
