# Black hole simulator

A single-page WebGL simulation: `index.html` holds the page, shaders and script; `music.mp3` is the background track. No build step.

## Checking changes

Rendering in a cloud session runs in software at 1–2 fps, so screenshot checks are slow.

- **Small tweaks** (colors, text, slider ranges, button behavior, small fixes): make the change, load the page once in a headless browser to confirm there are no errors, and push. No render screenshots.
- **Big changes** (a new scene, new physics, or rendering and layout changes that could break the look): do a full render check with screenshots before pushing, and say that one is being done.

If the user reports that a quick-mode change looks wrong, run a full check on it.
