# HTML & JS Reference Architecture for `/build`

When executing `/build`, construct the single-file HTML handbook following these exact structural and functional patterns.

## 1. Document Head & Tailwind Configuration

Include Google Fonts (`Cairo`, `Inter`, `JetBrains Mono`), Tailwind CDN, and the custom O'Reilly theme configuration:

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sprint X: [Title] — O'Reilly Interactive Edition</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700;800;900&family=Inter:wght@400;500;600;700&family=JetBrains+Mono:ital,wght@0,400;0,500;0,600;0,700;1,400&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Cairo', 'Inter', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    },
                    colors: {
                        oreilly: {
                            red: '#D3002D',
                            redDark: '#A80024',
                            crimson: '#B10026',
                            paper: '#FAF8F5',
                            paperDark: '#0F141C',
                            ink: '#1A1A1A',
                            teal: '#006677',
                            amber: '#D97706',
                        }
                    }
                }
            }
        }
    </script>
</head>
```

## 2. Core CSS Rules (O'Reilly Print-Meets-Interactive Aesthetic + Mobile Guardrails)

Always include:
- `.oreilly-stripe`: `background: linear-gradient(90deg, #D3002D 0%, #B10026 50%, #7A001A 100%);`
- `.ltr-code`: `direction: ltr; text-align: left; unicode-bidi: embed; font-family: 'JetBrains Mono', monospace;`
- Callout boxes: `.callout-tip` (Teal border `#006677`), `.callout-warn` (Red border `#D3002D`), `.callout-note` (Amber border `#D97706`).
- Mobile safety rules (`@media (max-width: 1023px)`):
  - `html, body { overflow-x: hidden; max-width: 100vw; }`
  - Off-canvas `#sidebarNav` (`position: fixed; top: 3.5rem; right: 0; bottom: 0; width: min(85vw, 320px); transform: translateX(105%); transition: transform 0.28s cubic-bezier(0.4, 0, 0.2, 1); z-index: 60;`) toggled via `.mobile-open` (`transform: translateX(0);`).

## 3. Top Brand Bar & Cookbook Modal

- **Top Header (`<header>`)**:
  - Mobile menu button (`toggleMobileSidebar()`).
  - O'Reilly Red Badge + Sprint Title.
  - Global Progress Bar (`#globalProgressBar` and `#globalProgressText`).
  - Cookbook / Practical Scenarios Modal trigger button (`toggleCookbookModal()`).
  - Reset Progress button (`resetSprintProgress()`, optional/subtle) and Dark Mode toggle button (`toggleDarkMode()`).
- **Cookbook Drawer/Modal (`#cookbookModal`)**:
  - Contains 4 to 6 copy-pasteable production recipes, troubleshooting runbooks, or architectural cheat sheets relevant to the Sprint.

## 4. Chapter Structure (Chapters 0 to 7)

- **Chapter 0 (`#chapter-0`)**:
  - O'Reilly Book Cover Hero Card featuring a custom lightweight inline `<svg>` woodcut-style animal illustration (use intricate strokes and hatching lines in SVG, no bloated Base64 images).
  - Sprint Curriculum Roadmap cards (clickable to jump to chapters).
  - **Diagnostic Pre-Assessment (6 Questions)**: Dynamically rendered from a `preQuizData` array with instant feedback and architectural explanations.
- **Chapters 1 to 7 (`#chapter-1` .. `#chapter-7`)**:
  - Chapter Header with Chapter Number badge, Arabic/English title, and "تم الإنجاز" completion toggle button (`toggleChapterComplete(n)`).
  - Deep engineering explanation structured into numbered parts (`1.1`, `1.2`, `1.3`), comparison tables, LTR syntax-highlighted code blocks with copy buttons, and O'Reilly Callouts.
  - **Interactive Lab / Simulator**: Each chapter has a dedicated interactive simulator powered by Vanilla JS (e.g., terminal simulator, interactive packet/memory visualizer, live config builder, architectural comparator).
  - **Chapter Checkpoint Quiz (4 Questions)**: Rendered from `chapterQuizzes[n]` with score counter and detailed explanations.
  - **Capstone Project Checklist (in Final Chapter)**: Interactive checkboxes (`toggleProjectTask(idx)`) with a live completion progress bar.
  - Bottom chapter navigation bar (Previous / Next Chapter buttons).

## 5. `localStorage` Persistence Engine (Mandatory Enhancement)

Every generated HTML file must persist user state in `localStorage` using a unique key per Sprint so refreshing or closing the browser on mobile or desktop never loses progress:

```javascript
const SPRINT_STORAGE_KEY = 'oreilly_sprint_state_v1_[UNIQUE_SPRINT_SLUG]';

let completedChapters = new Set();
let completedTasks = new Set();
let savedQuizAnswers = {}; // { 'pre-0': 1, 'ch1-2': 0, ... }
let chapterQuizScores = { 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0 };

function loadPersistedState() {
    try {
        const raw = localStorage.getItem(SPRINT_STORAGE_KEY);
        if (!raw) return;
        const data = JSON.parse(raw);
        if (Array.isArray(data.completedChapters)) completedChapters = new Set(data.completedChapters);
        if (Array.isArray(data.completedTasks)) completedTasks = new Set(data.completedTasks);
        if (data.savedQuizAnswers) savedQuizAnswers = data.savedQuizAnswers;
        if (data.chapterQuizScores) chapterQuizScores = data.chapterQuizScores;
        if (data.darkMode === true) document.documentElement.classList.add('dark');
        else if (data.darkMode === false) document.documentElement.classList.remove('dark');
    } catch (e) {
        console.warn('State load skipped:', e);
    }
}

function savePersistedState() {
    try {
        const payload = {
            completedChapters: Array.from(completedChapters),
            completedTasks: Array.from(completedTasks),
            savedQuizAnswers,
            chapterQuizScores,
            darkMode: document.documentElement.classList.contains('dark'),
            lastActiveChapter: currentChapter
        };
        localStorage.setItem(SPRINT_STORAGE_KEY, JSON.stringify(payload));
    } catch (e) {
        console.warn('State save skipped:', e);
    }
}
```

Ensure `savePersistedState()` is called inside:
- `switchChapter(n)`
- `toggleChapterComplete(n)`
- `answerPreQuiz(qIdx, optIdx)`
- `answerChQuiz(ch, qIdx, optIdx)`
- `toggleProjectTask(idx)`
- `toggleDarkMode()`

And on `DOMContentLoaded`, call `loadPersistedState()`, restore answered quizzes, restore completed chapter badges and capstone checkboxes, and jump to `lastActiveChapter || 0`.
