# BuildQuest Leaderboard — Project Bundle

Everything you need: the backend spreadsheet, the conversion script, and the
website that's ready to push to Vercel.

```
IMS_Hackathon_Leaderboard.xlsx   <- backend. Fill this in every week.
xlsx_to_json.py                  <- run this after updating the sheet
site/
  index.html
  styles.css
  script.js
  data.json                      <- auto-generated, the website reads this
```

## Weekly routine

1. Open `IMS_Hackathon_Leaderboard.xlsx`.
   - Go to the current week's `WeekN_Individual` tab → fill in each member's
     **Sessions Attended**, **Mini-Challenges Completed**, **Mini-Challenges Won**.
   - Go to the current week's `WeekN_Team` tab → fill in each team's
     **Weekly Update, Deploys, Helped Other Teams, Blog Posts, PRs Merged,
     Build Nights, Mentor Slots, Demo Day**.
   - Only type into the cream-colored cells — everything else is a formula.
   - The **Leaderboard** tab updates instantly: individual points are
     averaged per team, team points are added on top, ranks recalculate.
2. Save the file, then run:
   ```
   python3 xlsx_to_json.py
   ```
   This regenerates `site/data.json` from the Leaderboard tab — no personal
   info (emails/phone numbers) is ever included, only team name, track, and
   points.
3. Commit and push. If the repo is connected to Vercel, it redeploys
   automatically in under a minute.

## Deploying the site to Vercel (one-time setup)

1. Push the contents of this folder to a new GitHub repo (the `site/` folder
   can be the repo root, or keep the whole bundle together — either works).
2. Go to vercel.com → **Add New Project** → import that GitHub repo.
3. Framework preset: **Other** (it's plain HTML/CSS/JS, no build step).
   - Root Directory: `site` (if you kept the bundle structure above).
   - Build command: leave blank. Output directory: leave blank/`.`.
4. Click **Deploy**. You'll get a live `*.vercel.app` URL immediately.
5. From then on: edit the spreadsheet → run the script → `git push` →
   Vercel redeploys on its own.

## How points are split (matches your point-earning table)

**Individual** (tracked per member, then averaged into the team's score):
- Attending a live session — 5 pts/session
- Completing a mini-challenge — 20 pts/challenge
- Winning a mini-challenge — +30 pts bonus

**Team** (one set of numbers per team, not per member):
- Weekly progress update — 10 pts
- Deploying a working project/feature — 15 pts/deploy
- Helping another team (documented) — 10 pts/instance
- Writing a technical blog post — 20 pts/post
- Open source PR merged — 25 pts/PR
- Attending a Build Night — 15 pts
- Using a mentor hour slot — 5 pts/slot
- Demo Day presentation — 50 pts baseline

A team's weekly score = average of its members' individual points + its team
points for that week. Total = sum across all 6 weeks.

## About the demo data

Week 6 has sample numbers filled in across the board so the leaderboard and
website are easy to see working. Weeks 1–5 are at zero, exactly as a fresh
template should be. Delete Week 6's sample numbers in the spreadsheet
whenever you're ready to start logging real data — the website's "Overall"
view, podium, and per-week tabs all update automatically based on whatever
has actual numbers in it.

## Renaming the event

Open `xlsx_to_json.py` and change `EVENT_NAME = "BuildQuest Leaderboard"` to
whatever you're calling it, then re-run the script. The site reads the name
from `data.json`, so nothing in the HTML needs to change.
