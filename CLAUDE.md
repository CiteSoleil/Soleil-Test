# CLAUDE.md: soleilsportswear site

Read this whole file before every session. It is the handoff from the claude.ai chats where this site was built.

---

## 1. What this site is

The brand site for **Cite Soleil** and its clothing line **soleilsportswear**.

- **Main job:** a place where potential sponsors can see all of Soleil's creative work (events, campaigns, media, the Pynk Project archive).
- **Second job:** showcase clothes and, later, sell them.
- **Not public yet.** Visitors get in with a code that Stevens hands out. He opens specific pages for sponsor meetings.
- **Live test link:** https://citesoleil.github.io/Soleil-Test/ (GitHub Pages, repo `Soleil-Test`, account `CiteSoleil`).
- **Future:** may move to soleilsportswear.com, and may become a Shopify theme or connect Shopify only for products and checkout. Nothing is decided. Whatever happens, the design, motion, music and interactions must stay exactly as they are now.

---

## 2. How to work with Stevens

**Ask before you push.** Show what you changed and get his OK before committing or pushing to the repo. Never send messages, accept prices or commit to anything on his behalf.

**Garments are his designs.** Do not design clothing. You can place, organize, spec and present his designs.

**Writing style.** Never use em dashes, anywhere: code comments, copy, commit messages. Section content with headings and short blocks, not one long list.

**No mimicked handwriting.** No handwriting fonts, scrawled notes or fake pen marks anywhere on the site.

**Leopard print needs his approval.** Before using leopard anywhere new, get his explicit OK on both where it goes and why. Leopard already in his own designs (backpack, booth lining and floor option) stays as he made it.

**Nothing is final until he says so.** Prices, product details, FAQ answers and policies are placeholders.

**Test before you call it done.** Check phone size and desktop size, light and dark mode. Use `checklist.html` (Section 9).

---

## 3. Brand rules (short version)

**Names**
- CITE SOLEIL ("Soleil"): parent brand and creative studio. No accent, ever.
- soleilsportswear: all clothing and merch.
- Anhedonia: party series name only. Never on products. It is a rave and electronic party, never a skate event.
- Shred Soleil: future skate showcase, on hold.
- The meaning of the name "Soleil" is never explained or hinted at.

**Lines**
- Culture line (site, social): "Soleil is a creative world where fashion, music, skate culture, art, and nightlife meet."
- Business line (sponsors, press): "Soleil makes clothes, throws parties, and documents the culture around them."
- Sponsor-facing pages can use both: business line first.
- Never publish the internal north star or a mission statement.

**Type and wordmarks**
- Neue Helvetica Bold, tight tracking (about -0.03em). Webfont license still needed; the site uses a Helvetica fallback for now.
- Wordmarks are black #0B0B0B or white #F9F9F9 (pink this season). No outlines or effects. Never stretch, rotate or retype a wordmark.
- Clear space around wordmarks: at least the height of the "O".

**Colors**
- Rich black #0B0B0B, leopard white #F9F9F9, spot gray #B7B7B7, graphite #5E5E5E.
- Red #E1251B is the site accent (banners, mock garments). Stevens chose it. It is not yet in the official brand palette.
- Season pink (#FA98B8 or #FFBADC) is still OPEN.

**Art direction**
- Product: clean editorial luxury.
- Events and culture: raw nightlife (flash, grain, real moments).
- AI imagery is never used for product shots. Event content is always real.

**Third-party characters stay off the site.** Do not add artwork that shows recognizable characters owned by others (for example Betty Boop or Woody Woodpecker), even redrawn. Stevens manages his own additions through `my-items.js` (Section 5). Do not edit that file or move its contents into the site.

---

## 4. Files

| File | What it is | Who edits it |
|---|---|---|
| `index.html` | The whole site: HTML, CSS, JS and most images (embedded as data URIs) | Claude |
| `my-items.js` | Extra pieces Stevens adds to the homepage pile and archive | **Stevens only** |
| `site-settings.js` | Which pages are open without the code, and whether the homepage is locked | **Stevens** (Claude can explain it) |
| `music.mp3` | Background music, loops site-wide | Stevens supplies |
| `video.mp4` | Background video for the video page (muted) | Stevens supplies |
| `checklist.html` | Tester checklist (Pass, Fail, Skip, send results) | Claude, when features change |
| `sticker_03.png` etc. | Images referenced by `my-items.js` | Stevens |

**Recommended first job:** split `index.html` into normal files (`css/`, `js/`, `assets/img/`) without changing how anything looks or behaves. The embedded images make the file about 1.2 MB, and the photo and video library coming next cannot work that way. Then run the checklist on the new version and compare it side by side with the current live site.

---

## 5. How the site works

**One page, hash routes.** Every "page" is a section shown or hidden by `route()` on `hashchange`. Routes:
`home`, `mens`, `womens`, `accessories`, `campaigns`, `media`, `archive`, `about`, `faq`, `more`, `cart`, `terms`, `privacy`, `refunds`, `shipping`, `booth`, `video`, plus `random` (redirects).
Because it is one document, music keeps playing between pages. Keep that true in any rebuild (page transitions if pages become separate files or a Shopify theme).

**Top banner (menu)** and **bottom banner** ("JOIN SMS FOR EARLY ACCESS TO EXCLUSIVE DROPS & GIVEAWAYS"): red, Helvetica Bold, the top one includes the real wordmark SVG. Both auto-scroll in opposite directions. Hold to stop, drag to scrub, release to resume. A quick tap on a menu word navigates; a drag never does.

**Homepage pile.** Draggable pieces (the `ITEMS` array). One finger drags and flicks. Two fingers rotate and resize. Desktop scroll or trackpad pinch resizes. Tap opens a slide-up panel; red mock garments open their shop page instead. Shuffle rescatters. Pieces avoid the sign-up box when scattered and pass **under** it when dragged. Desktop pieces are scaled down (about 66 percent of phone size).

**Sign-up box** in the middle of the homepage: +1, numbers only, 10 digits, auto-formatted. Demo only (Section 7). Consent line links to Terms and Privacy.

**Braille art** repeats down the left side of the homepage behind the pile.

**Music bar** above the bottom banner: play and pause icons (drawn SVG, not text symbols), scrolling waveform. Music starts on the first tap anywhere, loops, and remembers mute. A round speaker button covers other pages.

**Lock.** Every page except the homepage, Terms and Privacy shows a lock screen. Code: **SOLEIL** (case-insensitive, stored only as a SHA-256 hash). The SMS pop-up appears on each locked page visit. Unlocking is remembered on that device (`localStorage: soleil-access`). `site-settings.js` can open chosen pages and lock the homepage. This is a soft lock for a static site, not real security.

**Random.** Every 1st or 2nd tap lands on a surprise, alternating between the **video page** (same pile over `video.mp4`; the sign-up hides after a valid number) and the **3D booth** (three.js r128, loaded only when opened; views, tower tops, heights, colors, floor). Other taps land on regular pages.

**Shop pages** (Mens, Womens, Accessories): item rail, corner frame, pixel build-in, console sounds, sold-out size, add to cart. Placeholder prices and copy. CSH003 hoodie is in Mens and Womens (all hoodies sell as both). Backpack side and front are two separate items in Accessories. The pink hoodie back is not on shop pages (not a product photo).

**Cart.** Quantities, remove, subtotal, demo checkout. Saved in `localStorage: soleil-cart`.

**Archive (Pynk Project).** Deconstructed tech pack: spec sheets (PP-001 codes, crop marks, measured dimensions, colorway swatches pulled from the art) on a board with the same drag, flick, rotate and resize as the homepage. Background grid: `rgba(0,0,0,0.08)` 1px lines, 40px, drifting diagonally at 25px per second (white lines in dark mode). Tap a sheet for full spec. Pulls every non-mock piece plus `my-items.js` pieces automatically.

**Policy pages** (Terms, Privacy, Refunds, Shipping): drafts with dashed fill-in boxes. A lawyer must review before launch.

**Other:** dark mode supported everywhere; reduced motion respected; safe-area insets for phones; Instagram links to instagram.com/soleilsportswear.

---

## 6. What Stevens wants next

1. **Portfolio for sponsors.** Large photography and video library across Media, Campaigns and events. Photos stored as separate, web-sized files and lazy-loaded. Videos hosted on a streaming service (Vimeo, Mux or Cloudflare Stream) and embedded, not stored in the repo.
2. **Per-page access for sponsor meetings** (already possible with `site-settings.js`; may grow into separate codes per audience).
3. **Asset pages.** Tapping a pile piece should eventually open its own page: a product page to buy it, or an info page for a mark or sticker.
4. **Shop** once real product photos exist.
5. **Domain and Shopify decision** later. If it becomes a Shopify theme, everything above must look, move and sound the same; music needs page transitions so it does not restart.

---

## 7. Open items

- **SMS is not connected.** The sign-up boxes collect nothing yet. Klaviyo (or Postscript) needs an account, SMS sender approval, and the form wired to its subscribe API. Do not collect numbers anywhere until consent wording matches the final SMS terms.
- International SMS is not decided (diaspora outreach matters). For now +1 covers the US and Canada.
- Season pink, prices, FAQ answers, policy details, launch date: all OPEN.
- Neue Helvetica webfont license.
- Possible lookalike concerns Stevens is reviewing with his lawyer: rabbit sticker vs FR2, backpack frame vs MLB logo, I love CS vs I love NY.

---

## 8. Things not to do

- Do not edit `my-items.js` or `site-settings.js` unless Stevens asks.
- Do not add recognizable third-party characters or reproduce other brands' logos.
- Do not use em dashes or handwriting fonts.
- Do not use leopard anywhere new without his approval.
- Do not change the look, motion or sound of existing features while restructuring.
- Do not push without his OK.

---

## 9. Testing

`checklist.html` lives next to the site at `/checklist.html`. Testers mark Pass, Fail or Skip and send results. It does not yet cover the lock, the SMS pop-up, Random surprises, the video page, music, the booth or the archive; add those sections.
