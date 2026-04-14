# Turing Machine Simulator

**Theory of Automata & Formal Languages — TAFL Project**

An interactive, fully visual Turing Machine simulator built as a single-page web application. Supports custom machine design, step-by-step execution, live transition diagrams, and 11 built-in examples — deployable instantly via GitHub Pages.

🔗 **Live Demo:** [your-username.github.io/turing-machine-simulator](https://your-username.github.io/turing-machine-simulator)

---

## Preview

| Dashboard | Simulator | Transition Diagram |
|-----------|-----------|-------------------|
| Hero section with stats | Step-by-step tape execution | Draggable SVG state diagram |

---

## Features

### Simulator Core
- **Infinite tape** with visual read/write head movement
- **Step forward** — execute one transition at a time
- **Step backward** — full undo/history support
- **Run / Pause / Stop** — continuous execution at adjustable speed (10 ms – 800 ms)
- **Reset** — reload input and restart from initial state
- Execution step counter and state/head/symbol display pills

### Transition Diagram
- Draggable state nodes (mouse + touch)
- Zoom in/out via mouse scroll and buttons
- Pan by dragging the canvas background
- Auto-layout and Reset View buttons
- Active state and edge highlighted during execution
- Double-ring for accept state, self-loops, curved bidirectional edges
- Grid background with SVG rendering

### Transition Table
- Fully editable — add, delete, or modify any rule live
- Highlighted row tracks the current transition during execution
- Apply button syncs table → machine → diagram

### Custom Machine Builder
- Paste transition rules in plain text format
- Format: `state, read → next_state, write, L|R|S`
- Comment lines starting with `//`
- Auto-fills formal machine components (Q, Σ, Γ, δ, q₀, B, F)
- Validates machine structure (unreachable states, missing transitions)
- Export current machine rules as plain text
- Stay (`S`) move direction supported

### Execution Log
- Step-by-step trace: `(state, read) → (state, write, move)`
- Color-coded accept / reject / running entries
- Scrollable, clearable

### Input & Validation
- Symbol palette — click to insert symbols into input field
- Regex pattern validation against current input
- Dynamic symbol detection from loaded transitions

### Examples (11 built-in)
| # | Name | Type | Input |
|---|------|------|-------|
| 01 | Binary Increment | Arithmetic | `1011` |
| 02 | Binary Decrement | Arithmetic | `1100` |
| 03 | aⁿbⁿ Checker | Context-Free | `aaabbb` |
| 04 | Equal Strings (w#w) | Comparison | `abb#abb` |
| 05 | Palindrome Check | Recognition | `abba` |
| 06 | Even Number of Zeros | DFA-style | `10100` |
| 07 | Unary Addition | Arithmetic | `111+11` |
| 08 | String Copier | Transform | `abc` |
| 09 | Bit Flipper | Transform | `10110010` |
| 10 | 3-State Busy Beaver | Classic TM | *(blank)* |
| 11 | Binary to Unary | Conversion | `1011` |

### UI / UX
- **Light mode & Dark mode** toggle (persisted in `localStorage`)
- Fully responsive — desktop, tablet, mobile
- Smooth tape cell animations on write
- Sticky navigation with active-section tracking
- Mobile hamburger menu

---

## Formal Model

A Turing Machine is a 7-tuple **M = (Q, Σ, Γ, δ, q₀, q_acc, q_rej)** where:

| Symbol | Meaning |
|--------|---------|
| Q | Finite, non-empty set of states |
| Σ | Input alphabet (blank ∉ Σ) |
| Γ | Tape alphabet (Σ ⊂ Γ, blank ∈ Γ) |
| δ | Transition function: Q × Γ → Q × Γ × {L, R} |
| q₀ | Initial state |
| q_acc | Accept state |
| q_rej | Reject state (q_acc ≠ q_rej) |

---

## Deployment — GitHub Pages

### Step 1 — Create Repository
1. Go to [github.com/new](https://github.com/new)
2. Repository name: `turing-machine-simulator`
3. Set to **Public**
4. Click **Create repository**

### Step 2 — Upload Files
```bash
# Clone your new empty repo
git clone https://github.com/YOUR-USERNAME/turing-machine-simulator.git
cd turing-machine-simulator

# Copy the project files in, then:
git add .
git commit -m "Initial commit: Turing Machine Simulator"
git push origin main
```

### Step 3 — Enable GitHub Pages
1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select branch: `main`, folder: `/ (root)`
3. Click **Save**
4. Your site will be live at:  
   `https://YOUR-USERNAME.github.io/turing-machine-simulator`

> ⏱ GitHub Pages typically takes 1–3 minutes to go live after the first push.

---

## File Structure

```
turing-machine-simulator/
├── index.html          ← Complete single-page application (HTML + CSS + JS)
├── README.md           ← This file
├── LICENSE             ← MIT License
├── .gitignore          ← Standard web .gitignore
└── _config.yml         ← GitHub Pages config (optional theme)
```

The entire application is **self-contained in `index.html`** — no build step, no npm, no dependencies to install. It loads two external resources:

- Google Fonts (Inter, Playfair Display, JetBrains Mono) — CDN
- Nothing else

---

## Custom Machine Builder — Format Reference

```
// Rule format:  state, read → write, move, next_state
// MOVE: R = move right, L = move left, S = stay
// Use B for the blank symbol
// Lines starting with // are comments

q0, a → X, R, q1        // Mark 'a', move right
q1, a → a, R, q1        // Scan past a's
q1, b → Y, L, q2        // Mark 'b', move left
q2, a → a, L, q2        // Scan left past a's
q2, X → X, R, q0        // Found X, restart
q0, Y → Y, R, q3        // Only Y's left, scan
q3, Y → Y, R, q3
q3, B → B, R, qaccept   // Blank means balanced → accept
```

---

## Technical Details

| Property | Value |
|----------|-------|
| Language | Vanilla JavaScript (ES6+) |
| Rendering | SVG (diagram), DOM (tape) |
| Fonts | Google Fonts CDN |
| Framework | None |
| Build step | None |
| File count | 1 (index.html) |
| Lines of code | ~1,800 |
| Max tape steps | 50,000 |
| Tape window | 22 visible cells (centered on head) |

---

## Reference & Acknowledgements

- [aepsilon/turing-machine-viz](https://github.com/aepsilon/turing-machine-viz) — original inspiration
- [turingmachine.io](http://turingmachine.io) — reference implementation
- Sipser, M. — *Introduction to the Theory of Computation*, 3rd ed.
- Hopcroft, Motwani, Ullman — *Introduction to Automata Theory, Languages, and Computation*

---

## License

MIT — see [LICENSE](LICENSE) for details.

---

*Built for the Theory of Automata & Formal Languages (TAFL) course.*
