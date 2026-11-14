# strum

A guitar you play with your mouse. Pick a chord from the radial menu, drag across
the strings, and watch each one vibrate as a damped standing wave while real
acoustic guitar samples ring out.

**[▶ Play it in your browser](https://drbarros2004.github.io/strum/)**

<!-- TODO: add a GIF here, e.g. ![strum demo](assets/demo.gif) -->

Built with [p5.js](https://p5js.org) and [Tone.js](https://tonejs.github.io). No build step.

## Controls

| Action | Input |
|--------|-------|
| Play | drag the mouse across the strings |
| Change chord | ← / → or A / D |
| Pick a chord directly | keys 1–6 |
| Change key (chord wheel) | ↑ / ↓, W / S or scroll |
| Toggle neck / full guitar view | V |
| Help | H or ? |

How hard you strum matters: faster drags play louder.

## How it works

- **Strings**: each string is drawn as a standing wave whose amplitude decays
  exponentially after a pluck. Thicker strings oscillate slower and ring longer.
- **Strumming**: the pointer's vertical speed is smoothed and mapped to note
  velocity through a perceptual curve.
- **Audio**: a Tone.js sampler pitches six recorded notes to any fret. A gain
  stage plus a limiter keep six stacked voices from clipping. When you change
  chords, only the strings whose note changed are released.
- **Views**: the neck view and the full guitar view share one physics model and
  are swapped at runtime.

## Run locally

Serve the folder with any static server, because browsers block audio loading from `file://`:

```bash
python3 -m http.server 5173
```

Then open <http://localhost:5173>.

## Project layout

| File | Role |
|------|------|
| `js/config.js` | constants, geometry, palette, physics |
| `js/chords.js` | chord wheels and fingerings |
| `js/guitarString.js` | string physics and drawing |
| `js/audio.js` | Tone.js sampler and anti-clipping chain |
| `js/strummer.js` | strum detection |
| `js/radialMenu.js` | radial chord menu |
| `js/views.js`, `js/guitarView.js` | view modes |
| `js/sketch.js` | `setup`/`draw`, input, coordinate transforms |

## Credits

- Acoustic guitar samples from [tonejs-instruments](https://github.com/nbrosowsky/tonejs-instruments)
  by Nicholaus Brosowsky, licensed [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/).
- Started as a small final project for a Computer Graphics course.

## License

Code is [MIT](LICENSE). The audio samples in `assets/samples/` keep their CC BY 3.0 license.
