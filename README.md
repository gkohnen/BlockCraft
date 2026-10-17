# BlockCraft 🧱🐷💥

A small, Minecraft-style block-building game that runs in your web browser. It's made for kids aged 8–10: there are no monsters, nobody can get hurt, and it's all about building, digging, flying and blowing things up with TNT.

The whole game is a single file, `index.html` (about 50 KB). It has no build step and no dependencies to install.

## Features

- An island world of 128 × 128 blocks, with hills, snowy peaks, beaches, a lake and trees
- 24 blocks to build with: rainbow wool, glass, bricks, gold, diamond, glowing lamps, TNT and more
- Gold and diamond ore hidden underground to dig for
- TNT that sets off other TNT nearby and throws pigs (and you) into the air
- Friendly pigs that oink and jump when you click them
- Flying, swimming, and day and night with a sun, moon, stars and clouds
- Simple sound effects made by the game itself (no audio files)
- The world saves itself in the browser, so you can carry on later

## Run it locally (localhost)

The game needs an internet connection the first time it loads, to fetch the Three.js 3D library from a CDN.

### Option 1: double-click (Mac)

1. Double-click **`start.command`**.
2. Your browser opens at **http://localhost:8080**.
3. To stop the game, close the Terminal window.

> The first time, macOS may say the file is from an unidentified developer. If so, right-click `start.command`, choose **Open**, then click **Open** again.

### Option 2: from the Terminal

```bash
git clone git@github.com:gkohnen/BlockCraft.git
cd BlockCraft
python3 -m http.server 8080
```

Then open **http://localhost:8080** in Chrome. Press `Ctrl+C` in the Terminal to stop the server.

You can use any port you like, for example `python3 -m http.server 3000` serves the game at http://localhost:3000.

**No Python?** If you have Node.js installed, this works too:

```bash
npx serve -l 8080
```

### Option 3: no server at all

You can also just double-click `index.html` to open it straight in Chrome. The localhost options above are a bit more reliable for saving your world.

## Controls

| Key / mouse | What it does |
|---|---|
| `W` `A` `S` `D` or arrow keys | Walk |
| Move the mouse | Look around |
| `Space` | Jump (or swim up) |
| `Shift` | Run |
| Left click | Break a block (hold to keep digging) |
| Right click, or `Ctrl` + click | Place a block |
| `1`–`9` or scroll | Choose a block |
| `E` | Open the block picker with all the blocks |
| `F` | Fly on/off (`Space` up, `Shift` down) |
| `T` | Switch between day and night |
| `M` | Sound on/off |
| `Esc` | Pause |

**On a Mac trackpad:** click with two fingers to place a block, and scroll with two fingers to change blocks.

**Tips:** place TNT, click it, then run! 🏃 Click a pig to make it jump. Dig deep to find gold and diamonds.

## Saving

The world is saved in your browser's local storage every 30 seconds, and again when you pause or close the tab. Saves belong to one browser and one address, so a world made at `localhost:8080` won't show up at `localhost:3000` or when you open the file directly. **🌍 New World** on the pause screen replaces the saved world with a fresh island.

## How it works

- Rendering uses [Three.js](https://threejs.org/) r128, loaded from cdnjs.
- The world is split into 16 × 16 chunks. Only block faces that touch air are drawn, with simple ambient-occlusion shading.
- Every texture is drawn by code into one small texture atlas when the game starts, so the game has no image files.
- Saves are run-length encoded to keep them small (about 80 KB).
