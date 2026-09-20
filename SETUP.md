# Bag of Holding — setup guide

Everything here is already wired to your Firebase project `bag-of-holding-c4ff9`.
Work through the steps in order. Budget about 30 minutes.

## 1. Firebase console

**Authentication**
1. Build → Authentication → Get started.
2. Sign-in method → Google → Enable. Pick your email as the support contact. Save.
3. Settings → Authorized domains → Add domain: `yourname.github.io` (your GitHub Pages
   domain, step 2). `localhost` is already allowed for testing.

**Firestore**
1. Build → Firestore Database → Create database → **Production mode**.
2. Region: `us-east4` or `us-central1`.
3. Open the **Rules** tab, delete what's there, paste the contents of `firestore.rules`,
   and Publish.

**Storage** (only if you want portraits and video clips)
1. Build → Storage → Get started. It asks you to attach a billing account (Blaze plan).
   A group this size stays inside the free allowance.
2. Rules tab → paste `storage.rules` → Publish.
3. If you skip Storage, everything else still works; portraits are shrunk and stored in
   the database instead, and animations aren't available.

## 2. GitHub Pages

1. Create a repository, e.g. `bag-of-holding`. Public is fine; nothing secret is in here.
   (The Firebase apiKey is a public identifier, not a password. The rules are what
   protect your data.)
2. Upload: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`.
3. Settings → Pages → Source: **Deploy from a branch**, branch `main`, folder `/ (root)`.
4. After a minute your link is `https://YOURNAME.github.io/bag-of-holding/`.
5. Add that domain in Firebase Authentication → Settings → Authorized domains.

## 3. First sign-in (do this yourself, before anyone else)

**The first Google account to sign in becomes the DM.** Sign in with your account
straight away so the DM seat is yours.

Then open **Characters**:
- **Player access** — add each player's Google address. Nobody else can get in.
- **Import party file** — choose `party-import.json`. It loads all seven sheets
  (Akra, Gak, Darg, Azcroth, Detlef, Astrid, Ivy) as unclaimed.
- **Open DM screen** — party view, roll feed, and whispers.

Akra's portrait doesn't survive the move, since it was stored inside Claude. She can
upload it again on her sheet.

## 4. What to send the players

> Here's our character tracker: https://YOURNAME.github.io/bag-of-holding/
> 1. Sign in with the Google account you gave me.
> 2. Pick your character from the list to claim it.
> 3. Add it to your home screen: iPhone → Share → Add to Home Screen.
>    Android → menu → Install app / Add to Home screen.
> 4. Tap the screen once when you open it so dice sounds and alerts can play.
> 5. Check your stats, spells and gear — I filled in placeholders.

## 5. Quick test before game night

- Two devices: your DM screen and one player sheet.
- Player rolls a skill → it appears in your roll feed within a second or two.
- You send damage from a party card → the player gets the alert, resistances applied.
- You whisper them as a trickster god → thumbnail, sound, note.
- Player hides → fog on their sheet, Stealth total on your card.

## Troubleshooting

- **"You're not on the player list yet"** — add that exact address under Player access.
- **Sign-in popup closes and nothing happens** — the domain isn't in Firebase's
  Authorized domains list, or the browser blocked the popup; it falls back to a redirect.
- **"Missing or insufficient permissions"** — the rules weren't published, or the player
  is trying to edit a character that isn't theirs.
- **Changes not syncing** — check the status text at the top right; it shows
  "Synced", "Saving…", or "Read only: not your character".
- **App looks stale after an update** — reload twice; the service worker caches the app
  shell. Bump `CACHE = "boh-v1"` in `sw.js` to `boh-v2` when you upload a new version.
