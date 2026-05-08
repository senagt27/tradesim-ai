# TradeSim AI — Setup Guide

## 📱 Android PWA (Install from Browser)

The `tradesim-pwa/` folder contains a fully installable Progressive Web App.

### Host it (free options):

**Option A — GitHub Pages (recommended, free)**
1. Create a free GitHub account at github.com
2. Create a new repository named `tradesim-ai`
3. Upload all files from the `tradesim-pwa/` folder
4. Go to Settings → Pages → Source: Deploy from branch → main
5. Your app is live at `https://yourusername.github.io/tradesim-ai`

**Option B — Netlify Drop (instant, no account needed)**
1. Go to app.netlify.com/drop
2. Drag the entire `tradesim-pwa/` folder onto the page
3. You get an instant URL like `https://random-name.netlify.app`

**Option C — Local network (for testing)**
```bash
cd tradesim-pwa
npx serve .
# Opens on http://localhost:3000
```

### Install on Android:
1. Open the hosted URL in **Chrome** on your Android phone
2. Tap the **"Install TradeSim AI"** banner that appears at the bottom
   — OR — tap Chrome menu (⋮) → "Add to Home screen"
3. Tap **Install** in the popup
4. TradeSim AI appears on your home screen like a native app

### Floating Widget (Android):
- Tap the **⊞ WGT** button in the top-right nav bar
- The widget shows Entry Zone, Stop Loss, TP1/TP2 for the active pair
- Select a second instrument in the app to populate Slot 2

---

## 🖥️ Windows Desktop App

The `tradesim-windows/` folder is a complete Electron project.

### Prerequisites:
- Node.js 18+ — download at nodejs.org
- Git (optional)

### Build the .exe installer:

```bash
# 1. Navigate to the windows folder
cd tradesim-windows

# 2. Install dependencies
npm install

# 3. Run in dev mode (test before building)
npm start

# 4. Build the Windows installer (.exe)
npm run build
```

The installer appears at `tradesim-windows/dist/TradeSim AI Setup 1.0.0.exe`

Double-click it to install. It will:
- Install TradeSim AI to your Programs folder
- Create a Desktop shortcut
- Add to Start Menu under Finance
- Add a system tray icon (bottom-right taskbar)

### Windows app features:
- **Full desktop app** — resizable window, 1280×820 default
- **System tray** — minimize to tray, right-click for menu
- **Floating widget** — always-on-top overlay showing 2 pairs
  - Entry zone, Stop Loss, TP1/TP2 at a glance
  - Draggable anywhere on screen
  - Stays visible while you use other apps
- **Native OS notifications** — Windows toast notifications on new signals
- **Widget toggle** — click ⊞ WIDGET button or use tray menu

### Run without building (dev mode):
```bash
cd tradesim-windows
npm install
npm start
```

---

## 🔑 API Key

Both apps call the Anthropic API. The API key is handled by the Claude.ai
artifact environment automatically during development.

For production deployment, set your API key:
- In the HTML files, the fetch call to `api.anthropic.com` needs an
  `x-api-key` header. Add your key to the headers object in the
  `fetchAnalysis` function.

---

## 📁 File Structure

```
tradesim-pwa/
├── index.html      ← Full PWA app (single file)
├── manifest.json   ← PWA install manifest
├── sw.js           ← Service worker (offline + caching)
└── icons/
    ├── icon-192.png
    └── icon-512.png

tradesim-windows/
├── main.js         ← Electron main process
├── preload.js      ← Secure IPC bridge
├── package.json    ← Build config (electron-builder)
├── renderer/
│   ├── index.html  ← Main app window
│   └── widget.html ← Floating always-on-top widget
├── src/
│   └── widget.html ← Widget source
└── assets/
    ├── icon.png
    ├── icon.ico    ← (generate from icon.png with ImageMagick)
    └── tray.png
```

### Generate .ico for Windows (optional, improves icon quality):
```bash
# Using ImageMagick
convert assets/icon.png -define icon:auto-resize=256,128,64,48,32,16 assets/icon.ico
```

---

## ⚠️ Disclaimer

TradeSim AI is for educational and informational purposes only.
AI-generated signals do not constitute financial advice.
Always use proper risk management. Trade responsibly.
