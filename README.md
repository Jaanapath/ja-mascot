# Ja Mascot Page

GitHub Pages site: looping mascot "Ja" with a talking speech bubble.

## Add the real mascot image

Drop your AI-generated image into this folder as `mascot.png` (same folder as `index.html`).
It'll replace the pink placeholder blob automatically — no code changes needed.

## Add more bubble lines

Edit the `lines` array near the bottom of `index.html`:

```js
const lines = [
  "Baby in process!",
  "another line here",
];
```

## Publish to GitHub Pages

```
git init
git add .
git commit -m "Initial Ja mascot page"
git branch -M main
git remote add origin https://github.com/Jaanapath/ja-mascot.git
git push -u origin main
```

Then on GitHub: repo **Settings → Pages → Branch: main → Save**.
Site will be live at `https://jaanapath.github.io/ja-mascot/`.
