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

## Silver border and not-legal filters

Downloads now include silver-border and Un-set cards printed before M15 (Scryfall hides these from ordinary searches, so the app runs a second search, `date<m15 border:silver`, for them). After updating the app, tap **Update cards** once to fetch them. In Filters, "Show only cards that are not legal" has one chip per reason (Silver border, Un-set / funny, Conspiracy, Ante, Banned, Other not legal), with counts. Pick several to see any of them. While a chip is on, "Hide cards ... not legal" is ignored.

## Continuous lists

Search results, the commander picker and EDHREC ideas all load as you scroll; there is no Show more button.

## Tribal theme

A commander counts as Tribal only if its text names a creature type (for example "Goblins you control", "each Elf") or says "creature type" or "chosen type". Generic anthems such as Elesh Norn's "Other creatures you control get +2/+2" no longer count.

A card counts as Silver border if any of its printings is silver, even when its oldest printing is not (the card shows the oldest printing's image and set).

## EDHREC themes

Picking a theme in Ideas loads that theme's EDHREC page and keeps only cards played more often in those decks than in the commander's decks overall (shown as "+N% vs all decks"). The message shows how many decks the theme has, and warns when there are fewer than 10.

## Cassie mode

In Filters, tick "Cassie mode" to show only cards that have a 2015-frame printing on or after M15, each shown with its newest 2015-frame printing (image, set, year, and the Scryfall link). The first time, it asks you to download those printings (one extra search, a few minutes, kept on the device). The mode is remembered, applies to search, the commander picker and EDHREC ideas, and untick it to go back to the original printings.

## EDHREC categories in Ideas

Each commander's Ideas sheet has an "EDHREC categories" row built from the lists EDHREC itself publishes for that commander (for example New Cards, Top Cards, High Lift, Creatures, Instants, Sorceries, Utility Artifacts, Enchantments, Planeswalkers, Utility Lands, Mana Artifacts, Lands). Each chip shows how many pre-M15 cards it holds. Categories combine with the theme chips and Cassie mode. Only lists EDHREC actually has for that commander appear.

## Not-legal cards are hidden by default

Cards that are not legal in Commander (banned, silver border, conspiracies and so on) no longer appear in search, the commander picker or Ideas until you tick "Show cards that are not legal in Commander" in Filters. The three unbanned cards still count as legal. Picking a category chip (for example Silver border) shows that category even while the box is unticked. Search and Ideas tell you how many were hidden.

## Retro frame filter

In Filters, tick "Retro frame" to show only cards that have a retro-frame printing. Each card appears once, shown with its foil retro printing if it has one (otherwise its newest). Cards with a foil version come first. Tap a card to see every retro-frame printing nested under it (set, year, foil or nonfoil); tap one to view it full size. It needs a one-time download of those printings (a few minutes, kept on the device) and also limits the commander picker and Ideas to cards with a retro-frame printing.

The download searches Scryfall for `frame:retro`. If Scryfall does not accept that keyword, the app automatically tries `is:retro` and then `(frame:1993 or frame:1997)`.

## Owned checklist and buying the rest

In the deck sheet every card (and the commander) has an "Own" button. Tap it to mark a card as one you already have; for a card you run several copies of it counts up ("Own 2/4") and wraps back to zero. The sheet shows how many cards you have and how many are left to buy, plus "Mark all owned" and "Clear owned". What you own is saved with each deck on this device.

"Buy the rest…" lists only the cards you do not own (any printing) and offers:
- TCGplayer: opens Mass Entry with the list filled in (and copies it). Review the matches there and tap Add to Cart.
- Mana Pool: copies the list and opens their import page (manapool.com/add-deck); paste it there and add the matches to your cart.
- Copy list: copies the lines to paste anywhere.

Neither store lets a web page fill a cart for you, so the last tap (Add to Cart) is yours.

## Choosing a printing

Under each card name in the deck sheet is a "Any printing ▾" button (commander included). Tap it to load that card's printings from Scryfall (set, number, year, picture) and pick one, with Nonfoil or Foil where it exists. "Any printing" clears the choice. The choice is saved with the deck.

"Buy the rest…" carries the picks across: TCGplayer gets lines like `1 Sol Ring [C21] 263`, and the copied/Mana Pool list uses `1 Sol Ring (C21) 263 *F*` (the `*F*` marks foil). A "Use the printings I picked" tick box lets you fall back to plain card names if a store does not recognise a set code. TCGplayer Mass Entry has no foil field, so choose foil on its listings after the list opens.

A printing you pick for a deck card is also the one shown everywhere that card appears (lists, the full-size viewer, its Scryfall link), with a note saying it is the printing picked for your deck.

TCGplayer note: Scryfall collector numbers with symbols (for example `325★`) are not valid on TCGplayer, so for those only the set is sent (`[7ED]`). If TCGplayer shows "unable to automatically add the items to your cart" after the link opens, use "TCGplayer (paste)": it copies the list and opens plain Mass Entry so you can paste it, fix any flagged lines, and add to cart yourself.

## Maybe board
Cards you're considering but haven't committed to. Tap the ☆ beside the + on any search result or Ideas row to put a card on the maybe board (★ means it's there; tap again to remove). In the deck sheet the maybe board is listed under the deck with **To deck** and ✕ buttons, and every deck row has a **Maybe** button to bench a card. Maybe cards never count toward the 100, the issues list, the mana curve, the owned checklist or the buy lists. Adding a card to the deck takes it off the maybe board. Export adds a `Maybeboard` section, and importing a list with a `Maybeboard` header fills the board. Each deck has its own maybe board.
