# Claude Code Prompt — Alice & Lucas Wedding Website

## Context
You are building a bilingual (French/English) wedding schedule website for Alice & Lucas, getting married on June 30, 2026 at Eagle's Eye Restaurant, Kicking Horse Mountain Resort, Golden, BC, Canada.

The site will be shared with ~60 guests (mix of French and English speakers) and the wedding party. It needs to be clean, elegant, mobile-friendly, and easy to navigate.

## What to build
A single HTML file (or simple folder structure) with **3 tabs**:

1. **Programme / Full Week** — 5-day calendar (June 28 – July 3) — PUBLIC
2. **Jour du Mariage / Wedding Day** — detailed June 30 timeline — PASSWORD PROTECTED
3. **Cérémonie / Ceremony** — step-by-step ceremony runsheet — PASSWORD PROTECTED

---

## Data files
All content is pre-written in JSON files in the `/content/` folder:
- `content/calendar_5days.json` — full 5-day calendar data
- `content/wedding_day.json` — wedding day timeline data
- `content/ceremony.json` — ceremony runsheet data

Read these files and use them to populate the site. Do not hardcode content.

---

## Password protection

**Tabs 2 and 3 (Wedding Day + Ceremony) are password-protected.**

- Password: `ZOZOSOCUTE1908`
- When a user clicks on Tab 2 or Tab 3, show a password modal/overlay before revealing content
- Once the correct password is entered, store it in `localStorage` so the user doesn't have to re-enter it on page reload or tab switch
- Wrong password: show a friendly error message
- The password modal should be elegant and on-brand (not a basic browser prompt)
- Tab 1 (Full Week) is always publicly accessible — no password needed

---

## WhatsApp collection banner

Show a dismissible banner at the bottom of the page (on all tabs) asking guests to share their WhatsApp number and name.

### Banner behavior
- Appears on first visit
- Contains two fields: Name (text) and WhatsApp number (tel input with +country code)
- A "Submit" button and a "Dismiss" button
- Once submitted OR dismissed, hide the banner and **never show it again** for that user (store in `localStorage`)
- Show a brief thank-you confirmation before hiding after submission

### Data storage
- Use the **Anthropic Claude API** (available via the AI-powered artifacts system — `fetch` to `https://api.anthropic.com/v1/messages`) to store submissions
- Actually, since we can't store to a database from a static site, use this approach instead:
  - On submit, format the data as: `Name: [name] | WhatsApp: [number] | Date: [timestamp]`
  - Send it to a **Google Form** POST endpoint (leave a placeholder comment `// TODO: replace with your Google Form action URL`)
  - The form should silently POST in the background — no redirect
  - Leave clear instructions in the code comments on how to set up the Google Form

### Google Form setup instructions (in code comments)
```
// HOW TO SET UP GOOGLE FORM FOR WHATSAPP COLLECTION:
// 1. Go to forms.google.com and create a new form
// 2. Add two Short Answer questions: "Name" and "WhatsApp"
// 3. Click the 3-dot menu → "Get pre-filled link"
// 4. Fill in dummy values and click "Get link"
// 5. From the URL, note the entry IDs (entry.XXXXXXXXX) for each field
// 6. Your form action URL is: https://docs.google.com/forms/d/e/YOUR_FORM_ID/formResponse
// 7. Replace GOOGLE_FORM_ACTION_URL, ENTRY_NAME_ID, and ENTRY_WHATSAPP_ID below
```

---

## Design requirements

### Visual style
- Elegant, warm, mountain-wedding aesthetic
- Color palette:
  - Gold/warm brown: `#8B6E52` (primary brand color)
  - Purple: `#7a3ea3` (mandatory/ceremony/wedding events)
  - Green: `#2e7d4f` (optional events)
  - Orange: `#c05c00` (meals/food)
  - Blue: `#3a6ea8` (photos)
  - Amber: `#c9a030` (rings/warnings/info)
  - Red: `#a33030` (closing/critical)
  - Light bg variants: `#f3eafa` (purple), `#edf7f0` (green), `#fff2e8` (orange), `#eef4fb` (blue), `#fef8ee` (amber), `#fae8e8` (red)
- Clean white/warm background, soft shadows, rounded cards
- Mobile-first — guests will view on phones

### Language toggle
- FR/EN toggle button visible at all times (top right corner or fixed in header)
- Switching language updates ALL text on the page instantly (no reload)
- Default language: French

### Header
- Always visible at top: "Alice & Lucas · 30 Juin 2026 · Golden, BC"
- Elegant, compact

### Tab navigation
- Three tabs always visible at the top
- Tab order: Full Week → Wedding Day → Ceremony
- Active tab clearly highlighted
- Tabs 2 & 3 show a small lock icon (🔒) until unlocked
- After unlocking, lock icon disappears for the session

### Event type color coding (consistent across all 3 tabs)
Use left-border + light background for all event cards:
- `mandatory` → purple `#7a3ea3`
- `optional` → green `#2e7d4f`
- `meal` / `food` → orange `#c05c00`
- `photo` → blue `#3a6ea8`
- `free` / `break` → gray
- `warn` / `info` → amber `#c9a030`
- `wedding` → purple with full border + subtle shadow (special treatment, more prominent)
- `travel` → blue (same as photo but lighter)

### Legend
Show a small color legend on each tab.

---

## Tab 1 — Full Week Calendar

- Show all 6 days as vertical cards (mobile) or a clean grid (desktop)
- June 30 is the wedding day — highlight it prominently (dark purple header)
- Each day: date header, theme subtitle, list of events in chronological order
- Events show: time, colored type badge, title, description
- If an event has a `note` field, show it in italic below the description (e.g. rehearsal note about wedding party only)
- Info box at the bottom with key practical info (from `info_box` in the JSON)

---

## Tab 2 — Wedding Day Timeline (password protected)

- Vertical timeline with time labels on the left, event cards on the right
- Section separators (Morning / Afternoon / Ceremony / Evening) from the JSON sections
- If event has a `flag` field, show it in amber italic text below the card
- Photographer's 4-hour package window (5 PM → 9 PM) should be noted visually

---

## Tab 3 — Ceremony Runsheet (password protected)

- Step-by-step numbered list
- Progress bar at the top showing time distribution across phases (data in `progress_segments` in JSON)
- Special visual treatment for the `wedding` type step (Alice's entrance, the ♡ step)
- Flag/warning notes in amber italic below relevant steps
- Total duration shown at the bottom

---

## Technical requirements

- Pure HTML/CSS/JS — no build step, no framework required
- Single `index.html` file preferred (with embedded CSS and JS)
- Loads JSON data files via `fetch()` — must be served (not opened directly as `file://`)
- Ready to deploy on **GitHub Pages**: push to repo, enable Pages on `main` branch, done
- Fully responsive: mobile, tablet, desktop

### GitHub Pages note
Since the site uses `fetch()` to load JSON files, it must be served over HTTP/HTTPS — it won't work opened directly as a local file. For local testing, use:
```
npx serve .
# or
python3 -m http.server
```

---

## Nice to haves
- Smooth fade transition when switching tabs
- Subtle entrance animations on cards
- Favicon: use a heart emoji or ring emoji as SVG favicon
- Print-friendly CSS for the ceremony runsheet tab

---

## Summary of all changes vs. previous version

The following corrections have been made in the JSON data files. The UI should reflect these:

1. **Ceremony order**: Anne-Laure speaks first (phones off, welcome) → Lucas enters (30 sec) → Wedding party 5 couples 2-by-2 (3 min) → Alice enters (2 min) → Alaina intro with early I-do exchanges → Parents speech → Vows → Rings (Zoa & Chris) → Closing
2. **June 29 rehearsal**: note that it's for wedding party and parents only
3. **June 29 dinner**: confirmed at the QG (not TBC)
4. **June 30 public view**: simplified to just show "17h00–00h30: Ceremony & Celebrations" — no detailed breakdown
5. **June 30 departure time**: 16h15 (not 16h30 or 16h45)
6. **July 1 Boo visit**: moved to 13h00; Whitetooth Brewing moved to 16h00; lunch before both
7. **July 2 last dinner**: 18h00 (not 19h00); "autres activités" note to check wedding website
8. **July 3 checkout**: all cabins by 11 AM (Bear's Den exception removed from public view)
9. **Password protection**: Tabs 2 & 3 require password `ZOZOSOCUTE1908`
10. **WhatsApp banner**: collect name + WhatsApp via Google Form POST

---

## Questions?
All content is in the JSON files in `/content/`. Use the JSON as the source of truth for all text. The tone is warm and celebratory. When in doubt, keep it elegant and simple.
