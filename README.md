# Name That Tune

A browser-based music quiz game with 4-choice answers, hints, difficulty levels, genre filters, and a local leaderboard.

## Features
- 4 multiple-choice answers per round (song title + artist)
- 3 difficulty levels: Easy (3 attempts, 4 hints, auto-play), Medium (2 attempts, 2 hints), Hard (1 attempt, no hints)
- Genre filters: Pop, Rock, Hip-hop, Classics
- Hint system with point cost
- Score + streak tracking
- Local leaderboard (saved in browser)

## How to deploy to GitHub Pages (free, no server needed)

### Step 1 — Create a GitHub repository
1. Go to [github.com/new](https://github.com/new)
2. Name it `name-that-tune` (or anything you like)
3. Set it to **Public** (required for free GitHub Pages)
4. Click **Create repository**

### Step 2 — Upload the files
**Option A — Drag and drop (easiest):**
1. Open your new repo on GitHub
2. Click **Add file → Upload files**
3. Drag `index.html` into the upload area
4. Click **Commit changes**

**Option B — Git command line:**
```bash
cd name-that-tune
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/name-that-tune.git
git push -u origin main
```

### Step 3 — Enable GitHub Pages
1. In your repo, click **Settings**
2. Scroll to **Pages** in the left sidebar
3. Under **Source**, select **Deploy from a branch**
4. Choose **main** branch, **/ (root)** folder
5. Click **Save**

### Step 4 — Visit your live site
After about 60 seconds, your game will be live at:
```
https://YOUR_USERNAME.github.io/name-that-tune/
```

GitHub will show the URL in the Pages settings once it's ready.

---

## Adding real Spotify previews

The game currently uses placeholder preview URLs. To get real 30-second Spotify previews:

### Option A — Manual (easiest for small song lists)
1. Go to [open.spotify.com](https://open.spotify.com)
2. Search for a song
3. Right-click the song → **Share → Copy Song Link**
   - Link looks like: `https://open.spotify.com/track/4cOdK2wGLETKBW3PvgPWqT`
4. Use the Spotify API to get the preview URL for that track ID:
   ```
   https://api.spotify.com/v1/tracks/4cOdK2wGLETKBW3PvgPWqT
   ```
   (Returns a `preview_url` field — a direct MP3 link)
5. Paste the `preview_url` values into the `SONGS` array in `index.html`

### Option B — Automated (for larger song lists)
Set up a free Vercel function (see the main project README) that fetches preview URLs from Spotify's API on the fly using your Client ID and Secret.

---

## Customizing the song list

Edit the `SONGS` array in `index.html`. Each song needs:
```js
{
  title: "Song Title",
  artist: "Artist Name",
  genre: "pop",          // pop | rock | hiphop | classics
  preview: "https://...", // direct MP3 URL (30 sec)
  hints: [
    "First clue",
    "Second clue",
    "Third clue",
    "Fourth clue"
  ]
}
```

Add as many songs as you like — the game picks randomly from the filtered pool each round.

---

## Customizing difficulty

Edit these objects in the script to change how points and attempts work:
```js
const maxAttempts = { easy: 3, medium: 2, hard: 1 };
const hintCost    = { easy: 5, medium: 10, hard: 0 };
const pointsForCorrect = { easy: 50, medium: 100, hard: 200 };
```
