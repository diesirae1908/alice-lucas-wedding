# Claude Code Prompt — Alice & Lucas Wedding Website

## Context
You are building a bilingual (French/English) wedding schedule website for Alice & Lucas, getting married on June 30, 2026 at Eagle's Eye Restaurant, Kicking Horse Mountain Resort, Golden, BC, Canada.

The site will be shared with ~60 guests (mix of French and English speakers) and the wedding party. It needs to be clean, elegant, mobile-friendly, and easy to navigate.

## What to build
A single-page website (or multi-page if you prefer) with **3 tabs**:

1. **Programme de la Semaine / Full Week** — 5-day calendar (June 28 – July 3)
2. **Jour du Mariage / Wedding Day** — detailed timeline for June 30
3. **Cérémonie / Ceremony** — step-by-step ceremony runsheet

## Data files
All content is pre-written in JSON files in the `/content/` folder:
- `content/calendar_5days.json` — full 5-day calendar data
- `content/wedding_day.json` — wedding day timeline data
- `content/ceremony.json` — ceremony runsheet data

Read these files and use them to populate the site. Do not hardcode content — read from the JSON files.

## Design requirements

### Visual style
- Elegant, warm, mountain-wedding aesthetic
- Color palette:
  - Gold/warm brown: #8B6E52 (primary brand color)
  - Purple: #7a3ea3 (mandatory/ceremony events)
  - Green: #2e7d4f (optional events)
  - Orange: #c05c00 (meals/food)
  - Blue: #3a6ea8 (photos)
  - Gold accent: #c9a030 (rings/info)
  - Light backgrounds for each type (e.g. #f3eafa for purple)
- Clean white background, soft shadows
- Mobile-first — guests will view on phones

### Language toggle
- FR/EN toggle button visible at all times (top right corner or in the header)
- Switching language updates ALL text on the page instantly
- Default language: French

### Tab navigation
- Three tabs always visible at the top
- Tab order: Full Week → Wedding Day → Ceremony
- Active tab clearly highlighted
- Smooth transition between tabs

### Event type color coding (consistent across all 3 tabs)
- **Mandatory / Incontournable**: purple (#7a3ea3) — left border + light purple bg
- **Optional / Optionnel**: green (#2e7d4f) — left border + light green bg
- **Meal / Repas**: orange (#c05c00) — left border + light orange bg
- **Photo**: blue (#3a6ea8) — left border + light blue bg
- **Free / Break / Pause**: gray — left border + light gray bg
- **Wedding moment**: purple with border on all sides + subtle shadow (special treatment)
- **Warning / Info flag**: gold/amber — italic text below the event description

### Legend
Show a small color legend on each tab so guests understand the color coding.

### Tab 1 — Full Week Calendar
- Show all 6 days as a scrollable vertical list (mobile) or horizontal cards (desktop)
- Each day has a header with the date, day name (FR/EN), and a theme/subtitle
- June 30 should be visually highlighted (it's the wedding day)
- Events listed chronologically within each day
- Info box at the bottom with key practical info (from `info_box` in the JSON)

### Tab 2 — Wedding Day Timeline
- Vertical timeline with time labels on the left, event cards on the right
- Section separators (Morning / Afternoon / Ceremony / Evening)
- Photographer 4-hour package (5 PM → 9 PM) should be visually noted
- Flag/warning notes shown in italic below relevant events

### Tab 3 — Ceremony Runsheet
- Step-by-step numbered list
- Progress bar at the top showing the distribution of time across ceremony phases
- Special visual treatment for Alice's entrance (the ♡ step)
- Total duration shown at the bottom: ~30 min

## Technical requirements
- Pure HTML/CSS/JS — no frameworks required (or use a lightweight one if you prefer)
- All in one HTML file if possible, or a simple folder structure
- No build step required — should work by opening index.html directly in a browser
- Ready to deploy on GitHub Pages (just push to a repo, enable Pages)
- Responsive — works on mobile, tablet, desktop
- All JSON data loaded and rendered client-side

## Deployment
Once built, the site will be pushed to a GitHub repository and hosted via GitHub Pages. The final URL will be shared with guests via WhatsApp and the wedding website (The Knot).

## Nice to haves (if time allows)
- Smooth scroll animations when switching tabs
- A small header with "Alice & Lucas · 30 Juin 2026 · Golden, BC" always visible
- Favicon (simple heart or ring emoji)
- Print-friendly CSS for the ceremony runsheet

## Questions?
All content details are in the JSON files. If something is unclear, use the JSON data as the source of truth. The tone should be warm and celebratory — this is a wedding!
