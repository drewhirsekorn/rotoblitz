# RotoBlitz — Fantasy League App

## What this is
A single-file multiplayer fantasy sports web app. Friends join via a shared league code, draft real athletes, and compete on a season-long leaderboard. No backend server — Firebase Realtime Database handles all shared state.

## File structure
- `fantasy-league.html` — the entire app (HTML + CSS + JS in one file)

## Tech stack
- **Firebase Realtime Database** (compat SDK v9.23.0) for live sync across all players
- **Vanilla JS** — no frameworks, no build step
- **Fonts**: Syne (headings) + DM Sans (body) from Google Fonts
- Firebase project: `rotoblitz` (rotoblitz-default-rtdb.firebaseio.com)

## Deployment
- Hosted on Netlify (drag-and-drop or GitHub auto-deploy)
- To deploy: push to `main` branch on GitHub → Netlify auto-deploys
- Live URL: check Netlify dashboard

## Key data structure (Firebase)
```
leagues/
  {leagueCode}/
    name: string
    week: number
    members/
      {playerName}/
        name, score, color, roster: { {playerName}: {name, sport, pos} }
    pool/
      {playerName}/
        name, sport, pos, team
    chat/
      {pushId}/
        from, text, ts
    log/
      {pushId}/
        to, pts, desc, ts
```

## League features
- Multi-sport: NFL, NBA, MLB, NHL, MLS, PGA, Tennis
- Unlimited roster size per player
- Season-long leaderboard (no weekly matchups)
- Commissioner awards bonus points manually via Admin tab
- Scoring rules visible in Scoring tab (NFL, NBA, MLB, NHL, Soccer)
- Real-time chat / trash talk
- Auto-login via localStorage

## Scoring rules (for reference)
### NFL
- Passing TD: +4, Passing yard per 25: +1
- Rushing/Receiving TD: +6, yards per 10: +1
- Reception: +0.5, INT thrown: -2, Fumble lost: -2
- FG <40: +3, 40-49: +4, 50+: +5

### NBA
- Point: +1, Rebound: +1.2, Assist: +1.5
- Block/Steal: +2, Turnover: -1, Triple-double bonus: +5

### MLB
- Single +1, Double +2, Triple +3, HR +4
- RBI +1, Run +1, SB +2, Walk +0.5
- Pitcher K +1, Win +5, ERA -1 per run

### NHL
- Goal +3, Assist +2, Shot +0.5, Block +0.5
- Hat trick bonus +3, Goalie win +5, Shutout +3, GA -1

### Soccer
- Goal +4, Assist +3, Shot on target +1
- Clean sheet +4, Save +1, Yellow -1, Red -3

## Common tasks for Claude Code
- "Add a feature to X" → edit fantasy-league.html, test in browser, commit
- "Fix bug where Y" → locate the relevant function, patch it, commit
- "Deploy latest changes" → `git add . && git commit -m "..." && git push`

## Coding conventions
- Keep everything in the single HTML file
- Use the existing CSS variable system (--bg, --surface, --accent, etc.)
- Firebase calls use the compat SDK: `db.ref(...).once('value')` / `.set()` / `.push()`
- All functions are global (plain `<script>` tag, not modules)
- Commit messages should be short and descriptive
