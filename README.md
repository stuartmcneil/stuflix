# 🎬 Stu Country for Old Men

Stu's personal film & TV grader. One HTML file, no build step, hosted on GitHub Pages, usable from PC, iPad and phone. Your grades and lists live in `data.json` in this repo and sync through the GitHub API.

Live site (once Pages is on): **https://stuartmcneil.github.io/stuflix/**
Part of [Stuart McNeil](https://stuartmcneil.github.io/window/)'s site.

## What it does

* **Films** and **TV** sections with identical tools (switch at the top right).
* **Top Ten** — front page, ranked by your own grade.
* **Catalogue** — always 100 titles awaiting judgement. Tick *Want to watch* or *Remove*; it tops itself back up (from the built-in list, or from TMDB's top-rated once you add a key).
* **Want to Watch** — the pile. Tick *Watched it* to grade.
* **Latest** — now showing in UK cinemas / coming soon / trending, and series on the air (needs a TMDB key).
* **Watched** — everything graded; click to edit.
* **Removed** — the cutting-room floor; restore anything.
* Click any poster or title for **details**: synopsis, cast, director, IMDb / Rotten Tomatoes / Metacritic / TMDB scores, and links to reviews on Letterboxd, The Guardian, NY Times, Empire, Sight & Sound and IMDb.
* **Grading**: ten stars for Overall, plus Acting, Cinematography and Story, a watched-on date and notes. If you leave Overall blank it averages the three criteria.

## One-time setup

### 1. Put it on GitHub

```bash
cd "C:\STUX\CLAUDE\Stux TV and Film"
git init
git add .
git commit -m "Stu Country for Old Men"
git branch -M main
git remote add origin https://github.com/stuartmcneil/stuflix.git
git push -u origin main
```

(Create the empty `stuflix` repo on github.com first — **public** is simplest, since GitHub Pages on a free account needs a public repo.)

Then on GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root) → Save.** A minute later the site is live at the address above.

### 2. Get the free API keys (about five minutes)

| Key | Where | What it gives you |
|---|---|---|
| **TMDB** (v3 API key) | themoviedb.org → sign up → *Settings → API* → request a key (choose *Developer*, personal use) | posters, cast, synopsis, latest releases, endless catalogue top-ups |
| **OMDb** | omdbapi.com/apikey.aspx → *Free* tier → confirm the email | IMDb, Rotten Tomatoes and Metacritic scores |

Letterboxd has no public API, and The Guardian / NYT reviews need full-text access, so those are one-tap links from each title's details page rather than embedded scores.

### 3. Make a GitHub token so the app can save

GitHub → your avatar → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.

* Name: `stuflix`
* Expiration: up to a year (you'll paste a new one when it expires)
* Repository access: **Only select repositories → stuflix**
* Permissions → Repository permissions → **Contents: Read and write**

Copy the token (starts `github_pat_…`).

### 4. On each device

Open the site → **Settings** tab → paste the token and the two API keys → **Save**. Keys are kept in that browser's local storage only; they are never written to the repo. Do this once on the PC, once on the iPad, once on the phone.

On iPad/iPhone, tap Share → **Add to Home Screen** to get it as an app icon.

## How sync works

* Every change is saved to the browser immediately, then pushed to `data.json` on GitHub about 2.5 s later (the status pill at the top says *Saved to GitHub hh:mm*).
* Opening the app pulls the latest `data.json` first, so the phone sees what the PC did.
* If two devices save at the same moment the app refetches and retries once. Avoid grading on two devices simultaneously and you'll never notice.
* Without a token the app still works read-only from the public `data.json` and saves locally on that device.
* **Settings → Export** downloads a backup; **Import** restores one.

## Files

| File | Purpose |
|---|---|
| `index.html` | the whole app |
| `data.json` | your lists and grades (committed by the app) |
| `.nojekyll` | tells GitHub Pages to serve files as-is |
| `README.md` | this |
