# Scansion

A browser-based poetic metre analyser. Paste or type lines of poetry on the left; the right panel scans each line in real time, marking stressed (`/`) and unstressed (`˘`) syllables, grouping them into feet (`|`), and identifying the metre.

## Features

- Real-time scansion as you type (120ms debounce)
- Syllable-level stress marking with `/ ˘` notation
- Foot grouping with `|` separators
- Metre detection: iambic, trochaic, anapestic, dactylic, spondaic, pyrrhic
- Foot count naming: dimeter through octameter
- Handles archaic/poetic elision: `languish'd`, `alter'd`, `follow'd` etc.
- Fully offline — no API calls, no dependencies
- Light/dark mode via `prefers-color-scheme`

## Usage

Open `poetry_scansion_local.html` directly in any modern browser. No server, build step, or internet connection required.

## How It Works

The scansion engine runs entirely in client-side JavaScript in four stages:

1. **Syllable counting** — vowel-nucleus detection with rules for silent final *-e*, silent *-ed*, syllabic consonants (*-tle*, *-ble*, *-ple*), plus a hand-tuned override table for irregular words
2. **Stress assignment** — function words (*the, and, that, of, to*…) are unstressed; monosyllabic content words are stressed; polysyllabic words follow suffix rules (*-tion*, *-ic*, *-ity*, *-ing*, *-ness*, prefixes *be-*, *re-*, *con-*…)
3. **Metre detection** — the stress pattern is scored against candidate templates; the best-fitting name and foot size are reported per line
4. **Foot grouping** — syllables are divided into feet based on the detected metre and rendered with `|` bars

## Files

```
scansion/
├── poetry_scansion_local.html   # The entire application (single file)
└── README.md
```

## Limitations

Computational scansion of English is hard without a full phonetic dictionary. The engine uses heuristics and will occasionally mis-stress a word — especially proper nouns, foreign borrowings, and highly irregular stress patterns. It works well on most classical English verse.

## Licence

MIT
