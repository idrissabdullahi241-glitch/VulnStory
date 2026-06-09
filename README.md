 VulnStory

> "Learn cybersecurity by living the attack."

VulnStory is an AI-powered interactive cybersecurity training application that transforms OWASP Top 10 vulnerabilities into immersive, story-driven scenarios. Users step into the role of attacker or defender inside realistic company environments precisely fintech platforms, hospital systems, e-commerce backends and make real incident response decisions with immediate AI-generated feedback.

Built on the Anthropic Claude API, every scenario is dynamically generated, ensuring no two sessions are identical.

---

 Features

- Story mode — AI-generated vulnerability scenarios with role-play (attacker or defender), difficulty levels (beginner / intermediate / advanced), and decision-based outcomes
- Quiz mode — Situational multiple-choice questions per OWASP Top 10 vulnerability with AI-generated explanations
- OWASP reference — Built-in cheat sheet for all OWASP Top 10:2021 entries with severity ratings
- Score tracker — Tracks correct decisions and accuracy across scenarios
- 10 vulnerabilities supported — SQL Injection, XSS, Broken Auth, IDOR, SSRF, XXE, CSRF, RCE, Open Redirect, JWT Misconfiguration

---

 Project Structure

```
vulnstory/
│
├── index.html              ← Main app (all UI + logic in one file)
├── README.md               ← This file
├── .env.example            ← API key placeholder
├── .gitignore              ← Prevents secrets being pushed to GitHub
│
├── src/
│   ├── app.js              ← Core app logic and Anthropic API calls
│   ├── scenarios.js        ← Pre-built scenario data (SQLi, XSS, etc.)
│   ├── owasp.js            ← OWASP Top 10 reference data
│   └── styles.css          ← All app styling
│
├── prompts/
│   ├── story_prompt.txt    ← System prompt for story mode generation
│   ├── quiz_prompt.txt     ← System prompt for quiz mode generation
│   └── README.md           ← Explains prompt engineering decisions
│
└── docs/
    ├── submission.md       ← Competition submission write-up
    └── screenshots/        ← App screenshots for judges
```

---

 Prerequisites

Before running VulnStory, make sure you have the following installed:

| Tool | Version | Purpose |
|------|---------|---------|
| A modern web browser | Chrome / Firefox / Edge | Running the app |
| A code editor | VS Code (recommended) | Editing files |
| Git | Any | Cloning the repo |
| An Anthropic API key | — | Powering the AI scenarios |

You do **not** need Node.js, Python, or any backend server. VulnStory runs entirely in the browser.

---

## Getting Your Anthropic API Key

1. Go to [https://console.anthropic.com](https://console.anthropic.com)
2. Sign up or log in
3. Click **API Keys** in the left sidebar
4. Click **Create Key** and copy your key — it starts with `sk-ant-...`
5. Keep it safe — you will paste it into the app

---

## Setup and Execution Guide

### Step 1 — Clone the repository

Open your terminal (Command Prompt on Windows, Terminal on Mac/Linux) and run:

```bash
git clone https://github.com/idrissabdullahi241-glitch/vulnstory.git
cd vulnstory
```


### Step 2 — Set up your environment file

Copy the example environment file:

```bash
# On Mac/Linux
cp .env.example .env

# On Windows
copy .env.example .env
```

Open `.env` in your code editor and add your API key:

```
ANTHROPIC_API_KEY=sk-ant-your-actual-key-here
```

> **Important:** The `.env` file is listed in `.gitignore` and will never be pushed to GitHub. Never paste your real API key directly into `index.html` or any file that goes into your repo.

### Step 3 — Open the app

Since VulnStory is a pure front-end app, you just open the file in your browser:

**Option A — Direct open (simplest):**
```bash
# Mac
open index.html

# Windows — double-click index.html in File Explorer
# OR right-click → Open with → Chrome/Firefox
```

**Option B — Using VS Code Live Server (recommended for development):**
1. Install the **Live Server** extension in VS Code
2. Right-click `index.html` in the file explorer
3. Select **Open with Live Server**
4. The app opens at `http://127.0.0.1:5500`

**Option C — Using Python's built-in server:**
```bash
# Python 3
python -m http.server 8000

# Then open your browser at:
# http://localhost:8000
```



## How the Anthropic API Integration Works

VulnStory calls the Anthropic Claude API directly from the browser using the `/v1/messages` endpoint:

```javascript
const response = await fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "x-api-key": YOUR_API_KEY,
    "anthropic-version": "2023-06-01"
  },
  body: JSON.stringify({
    model: "claude-sonnet-4-20250514",
    max_tokens: 1000,
    system: SYSTEM_PROMPT,
    messages: [{ role: "user", content: USER_PROMPT }]
  })
});
```

The model is instructed to return structured JSON only, which the app parses and renders into the scenario cards, choice buttons, and feedback panels.

---

## Keywords

`SQL Injection` · `OWASP Top 10` · `Cybersecurity Training` · `AI-Powered Learning` · `Interactive Scenarios` · `Defender Simulation` · `Web Security` · `Ethical Hacking` · `Anthropic Claude API` · `Security Awareness` · `CTF Training` · `Incident Response`

---

## Security Notes

- Your API key is never stored in any file committed to GitHub
- All API calls go directly from your browser to Anthropic — no backend server involved
- The app does not collect, store, or transmit any user data
- All scenarios are fictional and for educational purposes only

---

## Built With

- HTML5 / CSS3 / Vanilla JavaScript
- [Anthropic Claude API](https://docs.anthropic.com) — `claude-sonnet-4-20250514`
- [Tabler Icons](https://tabler.io/icons)
- OWASP Top 10:2021 framework

---

## License

MIT License — free to use, modify, and distribute for educational purposes.
