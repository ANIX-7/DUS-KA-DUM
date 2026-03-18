# Dus Ka Dum

A browser-based game show powered by 10 trained ML models predicting social media behaviour.

## Structure

```
dus-ka-dum/
├── frontend/
│   ├── index.html        ← Open this in a browser to play
│   ├── css/
│   │   └── style.css     ← All styles
│   └── js/
│       ├── data.js        ← Prize ladder + 10 survey questions
│       ├── game.js        ← Game logic (timer, lifelines, scoring)
│       └── main.js        ← Profile form + game boot
├── ai/
│   └── ai.js             ← Anthropic Claude API integration
├── backend/
│   └── backend.js         ← Fallback rule-based predictions + model metadata
├── models/
│   ├── README.md          ← Model documentation
│   └── *.pkl             ← 18 trained model + feature files
└── README.md
```

## Running

```bash
# Serve from the project root (required for relative JS paths to work)
python3 -m http.server 8080
# Then open: http://localhost:8080/frontend/
```

Or use VS Code Live Server pointed at `frontend/index.html`.

## How It Works

1. Player fills in their social media profile (age, platform, screen time, emotion).
2. The profile is sent to the **Anthropic Claude API** (`ai/ai.js`), which simulates
   all 10 trained ML models and returns a Yes/No prediction + the percentage of similar
   users who said YES + a key factor for each model.
3. If the API is unavailable, `backend/backend.js` provides rule-based fallback predictions.
4. The game asks 10 questions, one per model. The player guesses which percentage band
   matches the model's result. Correct answers climb the prize ladder up to ₹1 Crore.
5. Lifelines: **50:50** (removes 2 wrong options), **Skip**, **Double Dip**.
