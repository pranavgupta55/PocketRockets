# Pocket Rockets

A browser-based poker instinct trainer for beginners. Each hand deals you a real situation — your hole cards, a random street (preflop / flop / turn / river), a table of 2–9 players — and asks one question: **how strong is this hand, really?** You answer with one of four moves (Fold, Check/Call, Bet, Bet Big), and the game grades you against the hand's *measured* win probability.

No solver charts, no memorized ranges, no theory prerequisites. Every number is produced by dealing the exact situation thousands of times in your browser and counting what happens.

**[Try it live](https://pranavgupta55.github.io/PocketRockets/)** *(once GitHub Pages is enabled)*

Sibling project: [Deck Patterns](https://github.com/pranavgupta55/DeckPatterns), a Monte Carlo lab for shuffle-pattern probability questions.

## The core teaching idea: fair share

With P players at the table, an average hand wins **1/P** of the time — that's the "fair share" line. The whole game is one visual: a gauge showing where your hand's actual win chance sits relative to that line.

- Well below your share → every chip you put in is a losing chip → **Fold**
- Around your share → not a money-maker or a money-loser → **Check / Call**
- Comfortably above → chips come back with friends, on average → **Bet**
- More than ~double your share → build the pot → **Bet Big**

The zone boundaries are 0.8×, 1.35×, and 2.1× fair share. Spots within ~9% of a boundary accept either neighboring answer at full credit — real players size those either way, and near-misses shouldn't feel like failures.

This deliberately sidesteps bet sizing, pot odds arithmetic, and range theory. The goal is the *instinct* that precedes all of that: an honest read of raw hand strength for the current player count. (It also means the trainer models opponents as random hands — real opponents who've chosen to bet have stronger-than-random ranges, which is the natural next concept once this one is internalized.)

## How the math works

- A 7-card hand evaluator (best 5 of 7, standard poker rankings including wheel straights and chopped pots) scores every hand as a single comparable integer.
- Each dealt spot runs a chunked Monte Carlo simulation (1.5k / 4k / 10k trials, configurable): complete the board, deal every opponent two random cards, evaluate everyone, and record whether you won (ties credited as split equity).
- The same simulation feeds the **"where this hand could land"** panel — the live probability of your final hand being a pair, straight, flush, etc.
- Validated against published preflop equities: AA heads-up ≈ 85%, 72o heads-up ≈ 34.5%, AA at a 9-handed table ≈ 34.9%.

## Features

- **Stylized top-down table** — opponents arced around the felt, dealer at top, you at the bottom; cards deal and flip with staggered animations.
- **Four-move answer dock** with keyboard shortcuts (1–4, Enter for next hand).
- **Equity gauge** with colored move zones and the fair-share line; the win % is hidden until you answer (or tap 👁 peek — no judgment).
- **Run it out** — after answering, deal the rest of the hand and reveal everyone's cards, with a nudge that one runout proves nothing.
- **Streaks with forgiveness** — an adjacent-zone miss takes half credit but doesn't break your streak; only being two or more zones off resets it.
- **XP, session accuracy ring, and best-streak** persistence.
- **Session setup sheet** (slides up from the bottom): player count (fixed or random), which streets appear, simulation depth, practice mode (live numbers visible before answering), auto run-out, stat reset.
- **Three original themes** — Noir & Gold, Autumn Ember, Nebula — applied across the table, cards, and card backs.

## Running it

No build step, no dependencies: open `index.html`, or serve via GitHub Pages (Settings → Pages → Deploy from branch → `main` / root).

Stats and settings persist in `localStorage`; inside sandboxed previews (e.g. an artifact viewer) storage may be unavailable, in which case the app runs fine but doesn't remember between sessions.

## Project structure

```
PocketRockets/
├── index.html   # everything — markup, styles, evaluator, simulation, game logic
├── README.md
└── LICENSE
```

## License

MIT — see [LICENSE](LICENSE). Card designs and themes are original.
