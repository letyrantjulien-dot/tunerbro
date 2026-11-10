# TunerBro

A chromatic and instrument tuner that runs in the browser. Play a note, and TunerBro shows the note name and how many cents sharp or flat you are, on a needle or a strobe. It works offline once it has been opened, and the sound never leaves your device.

- Live: https://tunerbro.netlify.app
- Version: v1.1.0
- Licence: MIT
- An InvisibleChaos app. Impressum: https://invisiblechaos.netlify.app/impressum.html · Privacy (Datenschutz): https://invisiblechaos.netlify.app/datenschutz.html

Built with AI assistance: the code, the translations and this README were written by Julien and Claude, Anthropic's AI. Every file is reviewed, credited and maintained by a person, and this repository is the maintained home of TunerBro, not a dump.

## Browsers

TunerBro needs a browser with microphone access and the Web Audio API, which current Chrome, Edge, Firefox and Safari all offer, on desktop and mobile. The page must be served over https, or from `localhost`; browsers only allow the microphone on secure pages.

What has been tested so far: headless Chromium during development, and real use: Julien tuned his cello with it in November 2026.

## What it does

**Instruments and tunings.** These are all the presets the app offers. Chromatic mode tunes any note from about 27 Hz to 2,100 Hz.

| Instrument | Tuning | Strings, low to high |
|---|---|---|
| Chromatic | Any note | |
| Guitar | Standard | E2 A2 D3 G3 B3 E4 |
| Guitar | Half step down | D♯2 G♯2 C♯3 F♯3 A♯3 D♯4 |
| Guitar | Drop D | D2 A2 D3 G3 B3 E4 |
| Guitar | DADGAD | D2 A2 D3 G3 A3 D4 |
| Guitar | Open G | D2 G2 D3 G3 B3 D4 |
| Bass | 4-string | E1 A1 D2 G2 |
| Bass | 5-string | B0 E1 A1 D2 G2 |
| Bass | Drop D | D1 A1 D2 G2 |
| Ukulele | Standard (high G) | G4 C4 E4 A4 |
| Ukulele | Low G | G3 C4 E4 A4 |
| Ukulele | Baritone | D3 G3 B3 E4 |

With a preset, TunerBro picks the nearest string on its own. Tap a string to lock it; a locked string can play a reference tone.

There is no cello preset. The cello (C2 G2 D3 A3) has been tested in Chromatic mode.

**Reference pitch.** A4 = 440 Hz by default, adjustable from 415 to 466 Hz in 1 Hz steps. Equal temperament only.

**Displays.** A needle with a ±50 cent scale, or a three-band strobe that drifts when the note is off and stands still when it is in tune. A note counts as in tune within ±2 cents.

**Note names.** C D E F G A B, the German C D E F G A H, or Do Re Mi (with the Franco-Italian octave numbering, where La3 = 440 Hz).

**Languages.** English, French, Italian, German, Spanish, Japanese, Chinese (simplified) and Korean. The translations were written with Claude and have not yet been checked by native readers.

## The microphone and your privacy

- TunerBro listens through the browser's microphone permission, and only after you tap "Start listening". "Stop" releases the microphone.
- The sound is analysed in the page, on your device. No audio is recorded, stored or sent anywhere. The app has no server of its own: its only requests go to the site it is hosted on, to load its files and check for a new version.
- The browser's own echo cancellation, noise suppression and automatic gain are switched off, so they cannot bend the pitch.
- While listening, the app asks the browser to keep the screen awake, where the browser supports it.
- What stays on your device (browser local storage): your settings (instrument, tunings, display, A4, note names), your language choice, and whether you have seen the welcome tiles. Nothing else.
- The only links out are in the footer (the InvisibleChaos hub, Ko-fi, the Impressum), and they open only when you tap them.
- Like any website, the host (Netlify) sees the request when the page is loaded. The shared InvisibleChaos privacy page covers that: https://invisiblechaos.netlify.app/datenschutz.html

## Offline

A service worker keeps the app's files, fonts included, on the device after the first visit, so TunerBro works with no network. When the network is there, it picks up a new version on the next start; an update that arrives while you are tuning waits until you tap Stop.

## How the pitch is found

TunerBro uses the McLeod Pitch Method (McLeod and Wyvill, 2005), implemented from the published paper in plain JavaScript inside `index.html`, with no library. A first pass runs at half the sample rate to find the period; a second pass refines it at the full rate with parabolic interpolation. A median of the last few readings steadies the display. See [CREDITS.md](CREDITS.md) for the paper.

## Deploy

No build step: the files in this repository are the app.

- **Netlify:** drag the folder (or a zip of it) onto Netlify Drop. The `_headers` file is Netlify's format for cache rules: the page and the service worker are always revalidated, so updates arrive at once.
- **Any other static host:** upload the files and serve them over https. `_headers` can be ignored, but configure the host not to cache `index.html` and `sw.js` for long.
- **On your own computer:** run `python3 -m http.server` in this folder and open http://localhost:8000. The microphone is allowed on `localhost`.

When you change the code, raise the version in three places so devices pick up the update: `CACHE` in `sw.js`, `VERSION` and the footer line in `index.html`.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app: markup, styles, translations, pitch detection, display |
| `sw.js` | Service worker, for offline use and updates |
| `manifest.webmanifest` | Lets the browser install TunerBro as an app |
| `_headers` | Netlify cache rules |
| `icon.svg`, `icon-*.png` | App icons |
| `fonts/` | Archivo typeface, self-hosted, with its licence (`OFL.txt`) |

## Credits and licence

Every typeface, method and tool is credited in [CREDITS.md](CREDITS.md). The code is MIT licensed (see [LICENSE](LICENSE)); the Archivo font files keep their own SIL Open Font License, in `fonts/OFL.txt`.

Written by Julien and Claude the AI
