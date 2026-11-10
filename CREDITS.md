# Credits

TunerBro stands on the work of others. Here is whose.

## Pitch detection method

**McLeod Pitch Method.** Philip McLeod and Geoff Wyvill, "A Smarter Way to Find Pitch", Proceedings of the International Computer Music Conference, Barcelona, 2005, pp. 138-141. University of Otago. Paper list: https://www.cs.otago.ac.nz/graphics/Geoff/tartini/papers.html

TunerBro's implementation was written from the paper's description; no code was copied. It is part of `index.html` and MIT licensed with the rest of the app. The two-pass refinement (half rate, then full rate) and the median smoothing are TunerBro's own additions.

## Typeface

**Archivo** by Omnibus-Type. SIL Open Font License 1.1. https://github.com/Omnibus-Type/Archivo

The latin and latin-ext variable font files in `fonts/` come from the Fontsource package `@fontsource-variable/archivo` (https://fontsource.org/fonts/archivo). Fontsource's packaging is MIT licensed; the font files keep Archivo's licence, included as `fonts/OFL.txt`. They are served from the app itself, never from an outside font service.

## System fonts (named, not shipped)

For Japanese, Chinese and Korean text, and for the small monospace labels, the styles name fonts that many devices already have. They are used only if installed; nothing is downloaded:
Hiragino Sans, Yu Gothic, PingFang SC, Microsoft YaHei, Apple SD Gothic Neo, Malgun Gothic, Noto Sans CJK, Source Han Sans, SF Mono, Menlo, Consolas, Roboto Mono, Liberation Mono.

## Web platform

Built only on standard browser features, with no libraries: the Web Audio API, Media Capture and Streams (`getUserMedia`), the Screen Wake Lock API, Service Workers and the Cache API, and Web App Manifest.

## Hosting

**Netlify** hosts the live app. The `_headers` file uses Netlify's format. https://www.netlify.com

## Tools used while building (not shipped)

- **Node.js**, to test the pitch detection on synthetic tones. MIT licence. https://nodejs.org
- **Pillow**, to render the PNG icons from the drawing in `icon.svg`. HPND licence. https://python-pillow.org
- **Playwright** with Chromium, to check the layout at phone width in every language. Apache 2.0 licence. https://playwright.dev

## Artwork

The icons were drawn in code for TunerBro.

Written by Julien and Claude the AI
