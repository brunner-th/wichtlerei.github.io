# Secret draw

A static page for drawing names (Secret Santa / Wichteln style) with groups.
People in the same group never draw each other, and each person sees only
the name they drew. The organizer can't see anyone else's result either.

Everything runs in the browser. There is no server and no database, so it
works on GitHub Pages as a single `index.html`. The page itself is in German.

## Put it on GitHub Pages

1. Create a new **public** repository on GitHub, for example `secret-draw`.
2. Upload `index.html` (and this README if you like) to the main branch.
3. Go to **Settings → Pages**, set **Source** to *Deploy from a branch*, pick
   `main` and `/ (root)`, then save.
4. After a minute the site is live at
   `https://<your-username>.github.io/secret-draw/`.

## Running a draw

1. **Everyone joins.** Send the site link to everyone. Each person (you too)
   opens **Mitmachen** (Join), enters their name and a secret word, and sends you the
   code it shows (`SD1.…`). The code doesn't contain the secret word.
2. **You draw.** Open **Organisieren** (Organizer), paste all codes (pasting a whole chat
   is fine) and give people who belong together the same group label.
   Click **Namen auslosen** (Draw names). You get one link. The page never shows who drew whom.
3. **Everyone reveals.** Send that link to everyone. Each person picks their
   name, enters their secret word and sees who they drew.

## Why the organizer can't peek

Each person's code is a public key, derived from their name and secret
word. When you draw, every result is encrypted to the matching public key
(X25519 + AES-GCM), so it can only be opened with that person's secret word.
You only ever hold the public keys. The pairings exist in memory for a
moment during the draw and are never displayed or stored.

Things to keep in mind:

- **Forgotten secret word:** there is no reset. That person joins again with
  a new word, you replace their code and draw again, and everyone uses the
  new link (check the *Auslosungs-ID*).
- **Weak secret words** like `123456` could be guessed by someone determined,
  because everyone has the link. Short phrases or uncommon words are safer.
- **Trust in the page:** participants trust that the organizer didn't
  modify `index.html` to log the pairings. The repository is public, so
  anyone can check the code.
