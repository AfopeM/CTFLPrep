# CTFLPrep

An ISTQB Certified Tester Foundation Level (CTFL) exam prep platform built for real learners. The app serves 100+ monthly active users and covers all six syllabus chapters through timed quizzes, a full practice exam, and a personalised review system.

**Live site → [ctflprep.vercel.app](https://ctflprep.vercel.app)**

---

## What it does

**Chapter quizzes** — Each of the five available chapters has a pool of 40–50+ questions. Before starting, you choose a session length: Quick (10 questions), Standard (20), or Intensive (40). Questions are served in a smart order — unseen questions are always prioritised over ones you've already answered, so every session pushes you into new territory before revisiting old ground.

**Practice exam** — A timed 40-question exam modelled on the real CTFL format, with a 60-minute countdown. On submission, failed questions are automatically added to your MindVault for targeted review.

**MindVault** — A persistent review bank. Every question you answer incorrectly during a quiz is saved here, organised by chapter and exam source. You can quiz yourself exclusively on your saved questions and review them with full explanations. Questions answered correctly are automatically removed from the vault.

**Performance summary** — After every quiz or exam, you get a score gauge, a pass/fail result, a personalised improvement suggestion, and a count of questions currently in your MindVault.

**Review mode** — After any session, step through every question with correct answer highlighted, the full explanation displayed, and a navigation bar showing which questions you got right or wrong at a glance. You can add or remove questions from MindVault directly from the review screen.

---

## Chapters

| Chapter | Title | Status |
|---------|-------|--------|
| 1 | Fundamentals of Testing | Available |
| 2 | Testing Throughout the SDLC | Available |
| 3 | Static Testing | Available |
| 4 | Test Analysis and Design | Available |
| 5 | Managing the Test Activities | Available |
| 6 | Test Tools | Coming soon |

---

## Tech stack

| Layer | Technology |
|-------|-----------|
| Framework | React 19 + Vite |
| Language | TypeScript |
| Styling | Tailwind CSS v4 |
| Routing | React Router v7 |
| Animation | Framer Motion |
| State | React hooks + localStorage |
| Notifications | Sonner |
| Deployment | Vercel |

---

## Project structure

```
src/
├── components/         # Shared UI components
│   ├── exam/           # Exam-specific components (timer, navigation, question display)
│   ├── home/           # Landing page sections
│   ├── mindvault/      # MindVault card and question list
│   ├── quiz/           # Quiz question card and session selector
│   ├── review/         # Post-session review page and card
│   └── ui/             # Base UI primitives (Button, BackButton, ProgressBar, etc.)
├── data/               # JSON question banks and chapter/exam metadata
├── features/           # Feature-level components (Questionnaire, Loading)
├── hooks/              # Custom hooks (useQuestionState, useQuestions, useLocalStorage)
├── pages/              # Route-level page components
├── types/              # Shared TypeScript types
└── utils/              # Pure utility functions (exam scoring, formatting)
```

## Key implementation decisions

**Smart question ordering** — The quiz engine reads previously answered question IDs from localStorage and sorts the shuffled pool so unseen questions always surface first. This prevents the app from feeling repetitive while still allowing a full revisit cycle once all questions have been seen.

**MindVault persistence and migration** — MindVault items are stored in localStorage with a typed union structure distinguishing chapter and exam sources. On load, the app validates and migrates any legacy items from the old flat format, deduplicates, and logs invalid entries rather than silently dropping them.

**Atomic question state** — Quiz progress (current index, selected answer, results array) is optionally persisted to localStorage per chapter via `useQuestionState`, so refreshing mid-session resumes exactly where you left off. MindVault sessions deliberately skip persistence to keep review rounds clean.

**Exam auto-save to MindVault** — When an exam is submitted (or the timer expires), failed questions are diffed against existing MindVault entries and only new items are appended. Duplicate filtering runs before any write to prevent stale state from double-adding questions.

---

## Roadmap

- Chapter 6 (Test Tools) question bank
- Spaced repetition scheduling for MindVault items
- Progress tracking dashboard across sessions
- Bookmark individual questions mid-quiz
