# The Ascension Method — PWA

## File Structure
```
ascension-pwa/
├── index.html          ← The full app
├── manifest.json       ← PWA identity & install config
├── service-worker.js   ← Offline caching
├── icons/
│   ├── icon-192.png    ← Home screen icon (Android)
│   └── icon-512.png    ← Splash screen / high-res icon
└── README.md
```

---

## Deploying to GitHub Pages (step by step)

### 1. Create a GitHub account
Go to github.com and sign up if you don't have one.

### 2. Create a new repository
- Click the **+** icon → **New repository**
- Name it: `ascension-method`
- Set to **Public**
- Click **Create repository**

### 3. Upload your files
- Click **Add file** → **Upload files**
- Upload ALL files from this folder:
  - `index.html`
  - `manifest.json`
  - `service-worker.js`
  - `icons/` folder (both PNGs inside)
- Click **Commit changes**

### 4. Enable GitHub Pages
- Go to your repo → **Settings** → **Pages** (left sidebar)
- Under **Source** select **Deploy from a branch**
- Branch: **main** / folder: **/ (root)**
- Click **Save**
- Wait 1–2 minutes — your URL will appear:
  `https://YOUR-USERNAME.github.io/ascension-method/`

### 5. Fix the service worker path (IMPORTANT)
Because GitHub Pages serves from a subfolder, update `manifest.json`:
Change:
```json
"start_url": "/index.html"
```
To:
```json
"start_url": "/ascension-method/index.html"
"scope": "/ascension-method/"
```

And in `service-worker.js` change:
```js
const ASSETS = ['/index.html', '/manifest.json'];
```
To:
```js
const ASSETS = [
  '/ascension-method/index.html',
  '/ascension-method/manifest.json'
];
```

### 6. Install on your phone
- Open Chrome on your Android phone
- Go to your GitHub Pages URL
- Tap the **⋮ menu** → **Add to Home Screen**
- Name it **Ascension** → tap **Add**

For iPhone (Safari):
- Open Safari → go to your URL
- Tap the **Share** button (box with arrow)
- Tap **Add to Home Screen**
- Tap **Add**

---

## Icon Specifications

| File | Size | Used for |
|------|------|----------|
| icon-192.png | 192×192px | Android home screen icon |
| icon-512.png | 512×512px | Splash screen, Play Store listing |

### Customizing your icon
The current icons are generated from code. To use your own:
- Create a **square image** (equal width and height)
- Recommended: **1024×1024px** master, then resize down
- Format: **PNG with transparency** supported
- Safe zone: keep your logo/symbol within the **center 80%** — the outer 10% on each side may be clipped on some devices
- Background: should be **solid color** (not transparent) for best results on all launchers
- Tool: use **Canva**, **Figma**, or **Adobe Express** — export at 192px and 512px

### Maskable icons
The `"purpose": "any maskable"` in manifest.json means Android can reshape your icon (circle, squircle, etc). Keep your main symbol **centered and within 60% of the canvas** to avoid clipping.

---

## Offline behavior
After first load, the app works completely offline. Data is saved to the browser's localStorage on the device.
