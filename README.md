# Midnight Capsule

A vintage typewriter in the browser. A 3D machine sits on a lamp-lit walnut desk. Every key you press swings a typebar up to the platen, prints the character on impact and steps the carriage along. There is no on-screen keyboard: you write with your own.

It is a single static file (`index.html`), so it needs no build step.

## Features

- Real 3D scene (Three.js): enamel body, chrome, ivory keys, ink ribbon, a bent paper sheet around the platen.
- One typebar per key, with its own swing, strike, rebound and return.
- Ink is drawn onto the paper at the moment of impact, with small variations in weight and position.
- Carriage advance, bell before the right margin, margin lock, line feed and a full carriage return with lever.
- Backspace moves the carriage back one space and does not erase, so you can overstrike like on a real machine.
- Synthesised mechanical sounds (Web Audio, no audio files).
- Your sheet is saved in the browser (`localStorage`) and restored on your next visit.
- Responsive. On phones, tap the desk to open the keyboard.

## Controls

| Key | Action |
| --- | --- |
| Letters, numbers, punctuation | Strike a typebar |
| Shift | Capitals and symbols (the carriage lifts) |
| Space | Advance one space |
| Backspace | Move back one space (no erase) |
| Enter | Line feed and carriage return |
| Mouse wheel | Look up the page to re-read earlier lines |
| Esc | Close the "New sheet" prompt |

The top-right links toggle sound, copy all typed text to the clipboard and roll in a fresh sheet. When the last line of a sheet is reached, Enter loads a new sheet. Earlier sheets stay available to *Copy text* until the page is closed.

## Deploy on GitHub Pages

1. Create a new repository on GitHub (for example `midnight-capsule`). Public is fine.
2. Upload `index.html` and `README.md` to the root of the repository (**Add file → Upload files**), then commit.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose branch `main` and folder `/ (root)`, then **Save**.
5. Wait a minute or two. The site appears at `https://<your-username>.github.io/<repo-name>/`.

Or from the command line:

```bash
git init
git add index.html README.md
git commit -m "Add Midnight Capsule"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then enable Pages as in steps 3 and 4.

## Requirements

- A current Chrome, Edge, Safari or Firefox with WebGL.
- Internet access on first load. The page pulls two things from CDNs:
  - Three.js r128 from `cdnjs.cloudflare.com`
  - the Courier Prime font from Google Fonts (falls back to Courier New if blocked)

To run fully offline, download `three.min.js` (r128) into the repository, change the `<script src>` in `index.html` to `./three.min.js`, and do the same for the font with a local `@font-face`.

## Local preview

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Tuning

These values sit near the top of the script in `index.html`:

| Name | Effect |
| --- | --- |
| `CW`, `LH` | Character width and line height on the paper |
| `MX`, `TOP` | Left margin and first-line position |
| `UP`, `BACK` | Typebar flight and return time in milliseconds |
| `lamp.intensity` | Lamp brightness (search for `2.7`) |
| `EL`, `needH`, `needW` | Camera angle and framing |

## Notes

- The paper keeps 42 characters per line and about 26 lines per sheet at the default settings.
- Heavy typing on very old devices may lower the frame rate. Reducing the pixel ratio (`Math.min(devicePixelRatio, 2)`) to `1` helps.

## License

Add the licence of your choice. Three.js is MIT licensed, and Courier Prime is licensed under the SIL Open Font License.
