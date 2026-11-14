# Gig Lyrics Screen

One page, two modes. Open it on a laptop or TV for the **Screen** (lyrics, chords, capo, up next) and on a phone for the **Remote** (set lists, song picker, scroll, transpose, text size).

Add `#screen` or `#remote` to the address to force a mode.

## Setup (about 10 minutes, all free)

### 1. Firebase (this is what keeps the phone and the screen in sync)
1. Go to https://console.firebase.google.com and create a project (Analytics not needed).
2. Build > **Realtime Database** > Create database > start in **locked mode**.
3. Open the database's **Rules** tab, paste this and publish:
   ```json
   { "rules": { "rooms": { "$room": { ".read": true, ".write": true } } } }
   ```
4. Project settings (gear icon) > Your apps > **Web app** (`</>`) > register. Copy the `firebaseConfig` values.
5. Paste them into `config.js`. Make sure `databaseURL` is filled in (it is shown on the Realtime Database page).
6. Change `room` in `config.js` to a name only your band knows.

### 2. GitHub
Create a new repository and upload every file in this folder (`index.html`, `config.js`, `seed.js`, `README.md`).

### 3. Vercel
1. https://vercel.com > Add New > Project > import the GitHub repo.
2. Framework preset: **Other**. No build command. Deploy.
3. Open the Vercel address on the laptop and on your phone.

## Good to know
- With the rules above, anyone who has your database address and room name can read and change your songs. The room name is your only lock, so keep it private. For a real lock, add Firebase Authentication later.
- The Firebase values in `config.js` are meant to be public; they identify the project and are not passwords.
- Auto scroll runs on the phone, so keep the phone awake while it is on.
- First run: the Songs tab offers "Load Set 1 starter" (chords and cues, no lyrics). Paste lyrics in with Songs > Edit.
