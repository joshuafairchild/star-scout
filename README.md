# ⭐ Star Scout — Alt1 Shooting Stars Reporter

A [RuneApps Alt1 Toolkit](https://runeapps.org/alt1) app for RuneScape 3 that reads the shooting star telescope dialog and generates a formatted `/call` string for Discord.

## What it does

- **Scans your screen** for the telescope dialog when you use a telescope in-game
- **Auto-detects your current world** via Alt1's game state API
- Parses the **region, size, and relative landing time** from the dialog
- Outputs a formatted Discord call string:
  ```
  /call world: 84 region: C/K size: 7 relative-time: 8
  ```
- One-click **copy to clipboard** — paste directly into Discord

## Deploying to GitHub Pages

1. Create a new GitHub repository (e.g. `star-scout`)
2. Upload all files from this folder:
   - `index.html`
   - `appconfig.json`
   - `assets/icon.png` *(optional — replace with your own)*
   - `README.md`
3. Go to **Settings → Pages** in your repo
4. Set source to **Deploy from branch → main → / (root)**
5. Save — your app will be live at:
   ```
   https://YOUR-USERNAME.github.io/star-scout/
   ```

## Installing into Alt1

Once deployed, paste this URL into your browser address bar:

```
alt1://addapp/https://YOUR-USERNAME.github.io/star-scout/appconfig.json
```

Or navigate to your GitHub Pages URL in the Alt1 built-in browser and click **Add App**.

**When prompted, enable all 3 permissions:**
- ✅ View screen (pixel)
- ✅ Get game state
- ✅ Show overlay

## Using the app

1. Open the app in Alt1
2. Log into RuneScape and navigate to any telescope (e.g. Varrock Observatory)
3. Use the telescope — the dialog will appear on screen
4. Click **Scan Screen for Dialog** in the app
5. The region, size, and time fields will auto-fill
6. World is auto-detected from game state (or enter manually)
7. Click **Copy to Clipboard**
8. Paste into your Discord star scouting channel

## Manual entry

If OCR scan doesn't work (e.g. custom UI scale), all fields have manual dropdowns/inputs. The region dropdown uses the standard [starfind.net abbreviations](https://starfind.net/abbreviations/).

## Region abbreviations

| Full Name | Abbrev |
|-----------|--------|
| Anachronia | Ana |
| Asgarnia | Asg |
| Ashdale | Ash |
| Crandor/Karamja | C/K |
| Daemonheim | Daem |
| Kharidian Desert | Des |
| Fremennik/Lunar Isle | F/L |
| Feldip Hills | Feld |
| The Lost Grove | Grove |
| Kandarin | Kand |
| Morytania/Mos Le'Harmless | M/M |
| Menaphos | Mena |
| Misthalin | Mist |
| Piscatoris/Gnome/Tirannwn | PGT |
| Wendlewick | Wend |
| Wilderness | Wild |

## Development notes

- The app uses **Alt1's pixel capture + captureHtml** to read the RS chat area
- World detection uses `alt1.currentWorld` from the game state API
- When run outside Alt1 (e.g. in a regular browser), the Scan button simulates a sample dialog for testing
- No external data is sent anywhere — fully local to your machine

## Adjusting the scan region

If your RS client is at a non-standard resolution or UI scale and OCR is missing the dialog, you can tune the capture bounds in `index.html` by editing the `bounds` array inside the `scanScreen()` function:

```js
const bounds = [0, alt1.rsHeight - 200, alt1.rsWidth, 200];
//              x   y (from top)         width         height
```

The telescope dialog typically appears in the RS chat box area (bottom of screen).
