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
- Data > Update cards refreshes the list. Scryfall allows only 2 searches a second, so the download takes a minute or two. If Scryfall blocks it, the app waits and retries, and if it still stops you can tap Resume to continue from where it left off.

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

## Choosing a commander
- **Set commander** opens a picker of every legendary creature (and any card that "can be your commander").
  Search matches name, type line and rules text, with "quotes" and -exclusions, like the main search.
- **Refine** narrows the list by color identity (exactly these colors, or these or fewer), max mana value,
  and themes such as Tokens, Graveyard, +1/+1 counters or Sacrifice. Themes are guessed from the commander's
  rules text, so treat them as a starting point. You can sort by EDHREC popularity.
- **Ideas** (on every commander in the picker, and on the commander bar once one is set) shows EDHREC's
  suggestions for that commander, limited to cards printed before M15, with the synergy score and the share of
  decks that play each card. EDHREC's own theme tags (Reanimator, Mill and so on) switch the list. From the
  picker it is a preview, with a **Use as commander** button. Once a commander is set, each suggestion has a
  + button that adds it to your deck.
- EDHREC has no official API. The app reads the same JSON pages the EDHREC site uses, one page when you open
  Ideas, and keeps it for a week. If EDHREC blocks the request or has no page for a commander, the sheet says so
  and links to the commander's page on edhrec.com.

## Seeing a card full size
Tap any card image or name to open it full screen with the large picture and its full rules text. This works on
the commander at the top (the picture is larger now and shows the first lines of its rules text), on result
thumbnails and the picture inside an expanded result, on commanders in the picker, on EDHREC suggestions, and on
the names in your deck list. Close it with the Close button (or Escape on a keyboard).
