# Pre-M15 Commander (installable web app)

Searches every Magic card with a printing before Magic 2015 (Scryfall query `date<m15 game:paper`).
On first launch it downloads the card list from Scryfall and stores it on the device; after that
searching works offline (card images still need a connection).

## Put it on your iPhone
The app must be served over HTTPS. Easiest free route from the phone itself (GitHub Pages):
1. Unzip this folder in the Files app.
2. In Safari, sign in at github.com and create a new public repository.
3. Choose "uploading an existing file", select all files from the unzipped folder, and commit.
4. Settings > Pages > Deploy from a branch > main, folder / (root). Wait a minute for the URL.
5. Open that URL in Safari > Share > Add to Home Screen.
6. Open it from the Home Screen and tap "Download cards".

Any other static host works too (Netlify, Cloudflare Pages). Opening index.html straight from
Files will not work, because phones block storage and service workers on file:// pages.

## Using it
- Search words are ANDed. Use "quotes" for a phrase and a leading minus to exclude (add -black).
- Tap "Set commander", pick a legendary creature, and every result is limited to cards that fit its color identity (the commander itself is hidden). Change or remove it any time.
- Without a commander, the color buttons are your commander's colors: "Fits within" shows every card you can legally
  run in that identity; "Exactly" shows only that identity.
- Filters: card type, max mana value, sort (name, mana value, EDHREC popularity, oldest).
- Cards Scryfall lists as banned or not legal in Commander are flagged; a checkbox hides them.
- Data > Update cards refreshes the list.

Card data and images: Scryfall. Unofficial; not affiliated with Wizards of the Coast.

## Deck builder
- Tap **+** on any search result to add it to your deck. Tap again to remove it. Basic lands and
  "any number of cards" cards (like Relentless Rats) stack instead.
- The **Deck** button (top right) shows the card count. Inside you can keep several decks, rename them,
  set the commander, and see a mana curve, cards grouped by type, and warnings for off-color,
  banned, duplicate or missing cards. The count includes the commander and targets 100.
- Import: paste a list (one card per line, like `1 Sol Ring`). Cards not printed before M15 are listed as
  "Not in this format". Sideboard sections are skipped, and a `Commander` section sets the commander.
- Export: Copy deck list (or Share on iPhone).
- Decks are saved on the device.
