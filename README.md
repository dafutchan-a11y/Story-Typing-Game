# Hollowsdale Stories

A typing-driven choose-your-own-adventure storybook engine built for Lily.

Currently includes two stories:
- **Book 1: The Mystery of the Missing Card** — Otis lost a card he made for Mrs. Featherwhistle
- **Book 2: The Mystery of the Hidden Garden** — Hazel sees something through a knothole in the fence

---

## What's in this folder

```
index.html                    The game engine (single file)
story-1-missing-card.json     Book 1 content
story-2-hidden-garden.json    Book 2 content
audio/
  background-music.mp3        Looping background music
```

---

## How to deploy to GitHub Pages

1. Create a new GitHub repo (or update existing).
2. Upload these items:
   - `index.html`
   - `story-1-missing-card.json`
   - `story-2-hidden-garden.json`
   - `audio/background-music.mp3` (keep the `audio/` folder structure)
3. Settings → Pages → source = `main` branch, root folder.
4. Live at `https://<username>.github.io/<repo-name>/` after about a minute.

---

## How to test locally

The engine uses `fetch()` to load story JSON, which means **opening `index.html` directly with a double-click won't work**.

Use a local web server:

```bash
cd /path/to/this/folder
python3 -m http.server 8000
```

Then visit `http://localhost:8000` in a browser.

---

## How to add a third story later

1. Write a new JSON file using the same shape as the existing story files.
2. Drop it in the same folder as `index.html`.
3. Open `index.html` and find the line near the bottom that looks like:
   ```js
   const STORY_FILES = [
     'story-1-missing-card.json',
     'story-2-hidden-garden.json',
   ];
   ```
4. Add the new filename to the array.
5. Save, commit, push. New book appears on the bookshelf automatically.

---

## Design notes

**Two visual modes by intention:**
- **Reading mode** is a storybook page - cream parchment, rounded sans-serif body font (Quicksand) at 22px for comfortable kid-reading, centered with decorative leaf-and-vine corner ornaments. Pages flip with a soft 3D rotation.
- **Typing mode** is Hazel's notebook - lined paper with a pink margin line, casual handwritten font (Kalam) at 26px for the words being typed. The aesthetic shift is the cue that *Hazel is writing this thought now*.

**Typing engine** mirrors Typing Adventure: live character-by-character green/red feedback, must-backspace-to-fix errors, live WPM and accuracy. Smart quotes are normalized so typing a regular `'` matches a curly `'` if one ever sneaks into the JSON. On completion: a sparkle burst and soft chime.

**Save/resume** runs automatically on every page turn and choice. If Lily closes the laptop mid-story, the next time she opens the bookshelf she'll see a "Continue" banner.

**Storybook collection** appears at the bottom of the title screen. Every completed playthrough adds a tiny book to the shelf, color-coded by ending (pink = Mae, gold = Felix, green = Wilbur, purple = Window). Tapping a storybook re-reads the path she took, no typing required - it's pure read mode.

**Parent console** is hidden behind 5 quick taps on the "Hollowsdale Stories" title. From there you can:
- **Enter Test Mode** — play through the story freely without affecting any of her saved progress or storybook collection. Test-mode data is held in memory and discarded when you exit. A persistent banner at the top reminds you you're in test mode.
- Clear saves, clear the storybook collection, or reset everything.

**Music** loops in the background. The 🎵 button in the top-right toggles it. Browsers won't autoplay until the user interacts with the page, so the first click anywhere starts it.

**Sound effects** for page-flip, success-on-typing-complete, and ending celebration are synthesized on the fly via Web Audio API - no extra audio files needed. No typing-key click sound, per request.

**Decorations:** Falling autumn leaves drift gently across the background to match the story's autumn setting. Subtle pink/purple sparkles float in the foreground. A small magnifying glass icon bobs next to the title. Corner flourishes on each storybook page hint at vines and acorns.

---

## Browser support

Tested target: modern Chrome, Safari, Firefox on a laptop. Touch interactions are not designed for - laptop is the only target device.

---

## What's coming in Phase 2 (after Lily tries this)

- Refined page-flip animation (more book-like)
- "Unselect choice" mid-typing (currently only Esc to back out)
- More decorative animations on the title screen
- Possibly: typing-streak rewards, end-of-story stats, second story
