---
description: Generate the full CloudQuiz app from scratch in any directory
---

Generate the complete CloudQuiz application (AWS vs Azure vs GCP comparison quiz app) from scratch. This skill creates all files needed to run the app on any machine with Node.js installed.

## Prerequisites
- Node.js 18+ installed
- npm available

## Steps

1. Create project directory structure:
```
cloud-quiz-app/
├── .claude/commands/
│   ├── start-app.md
│   └── generate-project.md
├── src/
│   ├── components/
│   │   ├── AnswerKey.jsx
│   │   ├── FlashCards.jsx
│   │   ├── MatchGame.jsx
│   │   ├── MultipleChoice.jsx
│   │   ├── ScenarioChallenge.jsx
│   │   └── ScoreBoard.jsx
│   ├── data/
│   │   ├── answerKey.json
│   │   └── scenarios.json
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── index.html
├── package.json
├── vite.config.js
├── tailwind.config.js
├── postcss.config.js
└── README.md
```

2. Create `package.json` with these exact contents:
```json
{
  "name": "cloud-quiz-app",
  "private": true,
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "lucide-react": "^0.441.0",
    "framer-motion": "^11.5.4"
  },
  "devDependencies": {
    "@types/react": "^18.3.5",
    "@types/react-dom": "^18.3.0",
    "@vitejs/plugin-react": "^4.3.1",
    "autoprefixer": "^10.4.20",
    "postcss": "^8.4.45",
    "tailwindcss": "^3.4.10",
    "vite": "^5.4.3"
  }
}
```

3. Create `vite.config.js`:
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    port: 5173,
    open: true
  }
})
```

4. Create `tailwind.config.js`:
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
    },
  },
  plugins: [],
}
```

5. Create `postcss.config.js`:
```js
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

6. Create `index.html`:
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <title>Cloud Quiz - AWS vs Azure vs GCP</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

7. Create `src/main.jsx`:
```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

8. Create `src/index.css` with the full CSS including Tailwind directives, glassmorphism `.glass` class, `.gradient-text`, `.provider-aws/.provider-azure/.provider-gcp` gradients, card flip animations, floating orb animations, shimmer effect, and custom scrollbar. Copy the exact CSS from the source file.

9. Create `src/App.jsx` — the main app with 5 mode cards: Flash Cards, Match Game, Quiz Mode, Scenario Challenge, Answer Key. Imports all components and data files. Uses `framer-motion` for transitions, `lucide-react` for icons. Has a `scores` state for quiz/match history. Grid layout uses `lg:grid-cols-3` for the 5 mode cards.

10. Create `src/components/FlashCards.jsx` — Flashcard component with category filtering, shuffle toggle, flip animation. Uses `ProviderBadge` sub-component with provider-specific gradient badges.

11. Create `src/components/MatchGame.jsx` — Match game with random provider pair selection, 5 services per round, click-to-match mechanic, wrong answer shake animation, completion screen with accuracy.

12. Create `src/components/MultipleChoice.jsx` — 10-question quiz with 3 question types (equivalent service, category identification, provider identification), streak tracking, letter-labeled options (A/B/C/D).

13. Create `src/components/ScenarioChallenge.jsx` — Scenario-based challenge with: ServiceTag multi-select, PlatformButton selector, AiSuggestionCard with recommendation/reasoning/alternatives/keyTradeoff sections, progress bar, scoring, final results screen.

14. Create `src/components/ScoreBoard.jsx` — Simple stats display showing quiz avg and match avg percentages.

15. Create `src/components/AnswerKey.jsx` — Searchable reference table with category accordion, provider-colored cells, tradeoff display (green ▲ strength / amber ▼ tradeoff per provider), sub-details section.

16. Create `src/data/answerKey.json` — Complete service comparison data with 8 categories, 39 services, each with `id`, `serviceType`, `description`, `aws`, `azure`, `gcp`, and `tradeoffs` (strength + tradeoff per provider). Metadata includes sources array. Categories: Networking (7), Compute (6), Storage (4), Database (4), Security & Identity (4), DevOps & Management (4), Data & Analytics (6), Messaging & Integration (4).

17. Create `src/data/scenarios.json` — 10 real-world project scenarios with `title`, `description`, `requirements`, `correctServices`, `recommendedPlatform`, and `aiSuggestion` (recommendation, reasoning, alternativeConsideration, keyTradeoff).

18. Run `npm install` to install dependencies.

19. Create the `start-app.md` Claude skill in `.claude/commands/`.

20. Run `npm run dev` to start the dev server on port 5173.

## Important Implementation Notes

- All component files use **exact** content from the source project — do NOT paraphrase or modify the data
- The `answerKey.json` has 585 lines — create ALL 39 services with ALL tradeoffs
- The `scenarios.json` has 10 scenarios — create ALL of them
- Use `framer-motion` for all animations (not CSS transitions)
- The `AnswerKey.jsx` tradeoff section uses `&#9650;` (▲) and `&#9660;` (▼) HTML entities
- `MultipleChoice.jsx` has an "Oracle Cloud" fallback distractor in question type 3

## Tech Stack
- React 18 + Vite 5
- TailwindCSS 3
- Framer Motion 11
- Lucide React Icons

## Data Sources
- [Google Cloud Docs - AWS/Azure/GCP Service Comparison](https://docs.cloud.google.com/docs/get-started/aws-azure-gcp-service-comparison)
- [ByteByteGo - Cloud Comparison Cheat Sheet](https://blog.bytebytego.com)
