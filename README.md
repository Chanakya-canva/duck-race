# Duck Race 🦆🏁

A browser duck race game. Paste a list of names, hit **Race!**, and watch
named rubber ducks swim to a random winner.

**Stack:** a single `index.html` with vanilla HTML, CSS and JavaScript.
No build step, no dependencies, no server. This was a deliberate choice so the
page can be hosted anywhere and embedded in a Canva Website.

## Features

- **Name list** – one racer per line (up to 30). Each duck wears a name tag.
  Duplicate names are auto-numbered, long names shrink to fit.
- **Race timer** – set how long the race takes (default 30 s, range 5–300 s).
- **Fair random winner** – a winner is drawn at random before the race starts.
  Each duck's speed is then built from layered sine noise plus random bursts,
  so ducks surge, slump and swap places many times before the finish.
- **Lily pads & currents** – toggleable (default on). Lily pads briefly slow a
  duck, currents speed one up. They only ever sit in the first 70% of the
  track, so they add drama without changing who wins.
- **Random duck designs** – 12 palettes × hats × eyewear × neckwear × wing
  patterns, with blinking eyes and quacking bills. About 1 in 16 ducks is a
  rare ✨ legendary skin (golden, rainbow, galaxy or robot).
- **Live commentary** – a ticker calls lead changes, bursts, fades, lily pad
  hits, the halfway mark, the final stretch and the winner.
- **Position board** – a live leaderboard beside the pond, so lead changes are
  legible even with 20+ ducks.
- **Photo finish** – when the runner-up is within a few pixels at the line, the
  closing stages replay in slow motion before the winner is announced.
- **Sound** – synthesised quacks on GO, splashes on bursts, plops on lily pads,
  a whoosh in currents and a fanfare at the finish. Mute toggle is remembered.
- **Remembers your setup** – names, race time, hazards and mute state persist
  in the browser's localStorage.
- **Accessible** – ducks have descriptive alt text, the countdown and winner go
  to an ARIA live region, and `prefers-reduced-motion` cuts bobbing, confetti
  and the replay.
- **Hidden tab safe** – the race clock pauses when the tab is hidden, so ducks
  never teleport when you switch back.

## Run locally

Just open the file:

```bash
open index.html
```

Or serve it (useful for some browsers' `file://` restrictions):

```bash
python3 -m http.server 8000
```

then visit http://localhost:8000.

## Hosting on a Canva Website

Canva Websites can't run custom JavaScript directly, but they can **embed**
any publicly hosted web page. So the flow is:

### 1. Host `index.html` somewhere public (free options)

**GitHub Pages**

1. Create a repo (e.g. `duck-race`) and push `index.html` to the `main` branch.
2. Repo → *Settings* → *Pages* → Source: `main`, folder `/ (root)` → Save.
3. Your page will be live at `https://<your-user>.github.io/duck-race/`.

**Netlify Drop**

1. Go to https://app.netlify.com/drop.
2. Drag the `duck-race` folder onto the page.
3. Copy the generated `https://….netlify.app` URL.

(Vercel, Cloudflare Pages or any static host work the same way.)

### 2. Embed it in your Canva Website

1. Open your Canva Website design.
2. In the left panel choose **Elements → Embeds** (or search "Embed" in Apps).
3. Paste the public URL from step 1 and press **Add to design**.
4. Resize the embed frame. A height of **1000 px or more** gives room for the
   pond, position board and results; width can be the full page width.
5. **Publish** the website. The game runs inside the embed frame and is fully
   interactive for visitors.

> If Canva's embed preview shows a blank frame, make sure the URL is `https://`
> and loads in a normal browser tab first. The page sets no frame-blocking
> headers, so it is iframe-friendly out of the box.

## Customising

- Default names live in the `<textarea id="names">` in `index.html`.
- Colours and layout are CSS variables at the top of the `<style>` block.
- Duck looks are in the `PALETTES`, `HATS`, `EYEWEAR`, `NECK` and
  `WING_PATTERN` arrays in the script. Each entry pairs a screen-reader label
  with its SVG markup. Add an entry to add a new design.
- Race length is set in the **Race time** field (default 30 s, allowed 5–300 s). Change the `value` of `<input id="duration">` to alter the default.
- Commentary lines live in the `LINES` object; legendary skins in `LEGENDARY`.
- Sounds are generated with WebAudio in the `sound` object, so there are no audio files to host.
