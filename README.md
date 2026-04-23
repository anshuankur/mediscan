# MediScan — Drug Interaction Analyzer

A frontend web application that analyzes potential interactions between multiple medications using graph-based algorithms and a structured risk scoring system. Built as a portfolio project to demonstrate data structures, API integration, and UI design skills.

---

## 🔗 Live Demo

> **[Add your live demo link here]** — e.g., deployed on GitHub Pages or Vercel  
> `https://anshuankur.github.io/mediscan`

---

## ✨ Features

- **Multi-drug interaction detection** — Add 2 or more medications and detect all known interaction pairs simultaneously
- **Graph-based analysis engine** — Uses BFS, DFS, and a modified A* algorithm to find direct and cascading interaction pathways
- **Risk scoring (1–10)** — Weighted algorithm combining maximum severity, average severity, and interaction density
- **Four severity levels** — Mild, Moderate, Severe, and Critical — each with distinct visual indicators
- **Severity filter** — Filter detected interactions by severity level after analysis
- **SVG interaction map** — Visual graph showing drugs as nodes and interactions as color-coded edges
- **Risk breakdown panel** — Per-drug risk contribution bars and interaction severity chart
- **RxNorm API autocomplete** — Live drug name suggestions sourced from the US National Library of Medicine (no API key required)
- **RxNorm drug validation** — Debounced validation badge (✓ Verified / ⚠ Unknown) on drug name input
- **Analysis history** — Last 5 analyses saved to `localStorage` and accessible for one-click replay
- **Downloadable report** — Export results as a structured `.txt` file
- **Dark mode** — Full dark theme with `localStorage` persistence
- **Responsive layout** — Works on desktop and mobile screens

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 (semantic) |
| Styling | CSS3 (custom properties, grid, flexbox, animations) |
| Logic | Vanilla JavaScript (ES6+) — no frameworks |
| API | [RxNorm REST API](https://rxnav.nlm.nih.gov/) — free, no key required |
| Storage | Browser `localStorage` |
| Fonts | Google Fonts — DM Sans, DM Serif Display |
| Deployment | Static file — no build step required |

---

## ⚙️ How It Works

### Drug Database
The app includes a curated local database of 28 common medications with known interaction pairs. Each interaction has a severity score (1–10), a type (mild / moderate / severe / critical), and a clinical description.

### Graph Construction
Drugs are represented as **nodes** in an undirected graph. Known interactions are **edges** with a severity weight. The graph is built once on page load using an adjacency map.

### Analysis Algorithms

| Algorithm | Purpose |
|---|---|
| **DFS** | Discovers all interaction pairs among the selected drugs |
| **BFS** | Finds the shortest interaction path between any two drugs (used in insights text) |
| **Modified A\*** | Finds the highest-risk cumulative pathway across the full drug selection |

### Risk Scoring
The overall risk score is a weighted blend:
```
score = (max_severity × 0.55) + (avg_severity × 0.30) + (interaction_density × 0.15)
```
Clamped to 1–10 and mapped to a risk level: Low / Medium / High / Critical.

### RxNorm API
When a user types a drug name, the app:
1. First searches the local database for immediate suggestions
2. If results are sparse, calls the RxNorm `/spellingsuggestions` endpoint for live completions
3. After the user stops typing (600ms debounce), calls `/rxcui` to validate the drug and shows a verification badge

If the API is unreachable, the app falls back to local data silently — no errors shown to the user.

---

## 🚀 Running Locally

No build tools, no dependencies, no server required.

**Option 1 — Open directly**
```bash
# Clone the repository
git clone https://github.com/yourusername/mediscan.git

# Open in browser
open index.html
# or just double-click index.html in your file explorer
```

**Option 2 — Local dev server (recommended for API calls)**
```bash
# Using Python
python -m http.server 8000

# Using Node.js (npx)
npx serve .

# Then open
http://localhost:8000
```

> **Note:** The RxNorm API requires a network connection. The app works fully offline using only the local drug database.

---

## 🗂 Project Structure

```
mediscan/
├── index.html        # All HTML, CSS, and JS in one file
├── README.md
└── screenshots/      # (add your own)
```

---

## 🔮 Future Improvements

- **Expand the drug database** — integrate a more comprehensive interaction dataset (e.g., DrugBank or OpenFDA)
- **PDF report export** — replace the current `.txt` download with a formatted PDF using jsPDF
- **Dosage-aware analysis** — factor in drug dosages when calculating interaction risk
- **Patient profile** — allow users to save their medication list between sessions
- **Search by condition** — let users find common medications for a diagnosis, then check interactions
- **Unit tests** — add tests for the graph algorithms and scoring logic using Jest

---

## ⚠️ Disclaimer

**MediScan is intended for educational and portfolio demonstration purposes only.**

- All interaction data in the local database is based on publicly available clinical information but has not been reviewed by a licensed medical professional.
- This tool does **not** constitute medical advice and should **never** be used to make real clinical decisions.
- Always consult a qualified pharmacist or physician before starting, stopping, or changing any medication.
- The RxNorm API is provided by the US National Library of Medicine. MediScan is not affiliated with or endorsed by the NLM or any healthcare institution.

---

## 👤 Author

**[Anshu Ankur]**  
2nd-year Computer Science Student  
[GitHub](https://github.com/anshuankur) · [LinkedIn](https://www.linkedin.com/in/anshu-ankur-b22746313/)

---

## 📄 License

This project is open source under the [MIT License](LICENSE).
