# fitkar
FitKar is an AI-powered virtual try-on web app that lets users upload photos and see realistic outfit previews using advanced models like Replicate and Hugging Face. It offers smart outfit suggestions, a fashion chatbot, inspiration trends, and cloud saving—delivering a complete, modern styling experience across all devices.
<br>
# FitKar — AI Virtual Try-On

A full-stack AI fashion try-on app using **IDM-VTON** via Replicate.

---

## 🚀 Quick Start

### 1. Get a Replicate API Token
Sign up at https://replicate.com → Account → API Tokens → Create token (starts with `r8_`)

### 2. Install backend dependencies
```bash
npm install
```

### 3. Start the backend
```bash
REPLICATE_API_TOKEN=r8_your_token_here node server.js
```

### 4. Open the frontend
Open `index.html` in your browser (or serve via any static server).

---

## 📁 File Structure

```
fitkar/
├── index.html     ← Frontend (HTML/CSS/JS)
├── server.js      ← Backend (Node.js + Express)
├── package.json   ← npm config
└── README.md
```

---

## 🎯 Features

| Feature | Details |
|---------|---------|
| 🔐 Login/Register | localStorage-based, auto-login |
| 📸 Upload or Camera | Both person & garment photos |
| 🤖 Real AI Try-On | IDM-VTON via Replicate API |
| 💾 History | Save results to localStorage |
| 🆚 Compare | Side-by-side image comparison |
| 💬 Chatbot | Claude-powered fashion advice |
| ⬇️ Download | Save result to device |

---

## ⚙️ Architecture

```
Browser (index.html)
    ↓  POST /tryon { personImage, clothImage }
Express (server.js :3000)
    ↓  POST https://api.replicate.com/v1/predictions
Replicate (IDM-VTON model)
    ↓  polls until complete
    ↑  returns output URL
Browser displays result image
```

---

## 🔑 Client-Side Key (No Backend)

You can also enter your Replicate API key directly in the frontend input field. The app will call Replicate directly from the browser — **only recommended for local testing**, not production (exposes your key).

---

## 🧠 AI Model

**IDM-VTON** — State-of-the-art virtual try-on model
- Model: `yisol/idm-vton`
- Input: full-body person photo + garment photo
- Output: realistic image of person wearing garment

Alternative: **OOTDiffusion** (`levihsu/ootdiffusion`) — see commented code in `server.js`

---

## 🛠 Troubleshooting

| Issue | Fix |
|-------|-----|
| `CORS error` | Make sure `server.js` is running on port 3000 |
| `missing REPLICATE_API_TOKEN` | Set env variable before starting server |
| `Prediction failed` | Check Replicate dashboard for error details |
| `Camera denied` | Allow camera in browser permissions |
| AI takes long | Normal — IDM-VTON takes 30–90 seconds |
