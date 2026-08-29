# basil.js

A programming language that runs in a browser, with a 3D renderer and its own
editor built in. One file, no build step, no install.

basil.js is C-like, and the file contains the whole thing: the lexer, parser,
resolver, bytecode compiler and interpreter that run the language, a WebGL2
renderer with a shader transpiler so shaders are written in it too, and the
development environment — editor, syntax highlighting, tabbed buffers and a
linter.

It was written by [Jubel Sanabria](https://basilworld.net) and is used for
[basilScape](https://basilscape.basilworld.net), a rebuild of the 2004 version
of RuneScape that runs entirely in the browser.

## Getting started

Put `basil.js` next to an HTML file and load it:

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>basil.js</title>
<style>
  html, body { margin: 0; height: 100vh; background: #000;
               display: flex; align-items: center; justify-content: center; }
</style>
</head>
<body>
  <canvas id="basil-canvas"></canvas>
  <script>
    window.BASIL_WIDTH = 765;
    window.BASIL_HEIGHT = 503;
  </script>
  <script src="./basil.js"></script>
</body>
</html>
```

Open that page through a web server rather than from the file system, since
the browser blocks `fetch` on `file://` URLs. Anything will do:

```bash
python -m http.server
```

On startup basil.js fetches `./program.txt` next to the page and runs it. **If
there is no `program.txt`, the editor opens instead** — which is the easiest
way to begin. Write something, press Run, and it executes. Press `F1` at any
point to bring the editor back over a running program and read or change its
source.

The `example/` folder is exactly the page above, with no `program.txt`, so it
drops you straight into the editor.

## Configuring the page

Set these on `window` before loading `basil.js`:

| Global | Meaning |
| --- | --- |
| `BASIL_WIDTH` / `BASIL_HEIGHT` | Render resolution in pixels. Defaults to 240×160. |
| `BASIL_SCALE` | Largest whole-number upscale allowed when fitting the canvas to the window. Defaults to 8. |
| `BASIL_LETTERBOX` | Set to `false` to fill rather than letterbox. |
| `BASIL_APP_NAME` | Name shown in the window chrome. |

`BASIL_SCALE` is a maximum, not a fixed factor: the engine picks the largest
whole-number multiple of your resolution that still fits, so the picture stays
pixel-exact instead of being resampled. For a program that should fill the
window at its true size, set the width and height from `window.innerWidth` and
`window.innerHeight` and set `BASIL_SCALE` to 1.

## Writing it with an AI

basil.js is small enough to explain and unusual enough to be worth exploring, and
it pairs well with an AI assistant. Give one this repository, describe what you
want, and let it write the code — that is how most of what basilScape is made
of came together. It is a good way to find out what the language can do without
learning it front to back first.

## License

MIT — see [LICENSE](LICENSE). Use it, change it, ship it; just keep the
copyright notice.
