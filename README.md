# pudding-dog
This is a desktop pet inspired from my pet dog. It is built with the help of claude as I am not too talented in coding. It can sit, roam, and eat documents you do not want. Enjoy

# Desktop Pudding 🐶

A pixel-art desktop pet for macOS, modelled on a real dog named Pudding. He
lives in a kennel on your screen, wanders around when he feels like it, eats
files you want gone, and fetches files you've lost.

---

## Requirements

- **macOS** (he uses Finder, Spotlight, and macOS window APIs)
- **Node.js 18 or newer** (20+ recommended)

Everything else is downloaded automatically by `npm install`.

---

## Installation

### 1. Unzip

Unzip `desktop-pudding.zip` anywhere you like — your Desktop, Documents,
Applications, wherever. You'll get a folder called `desktop-pudding`.

### 2. Check whether you have Node.js

Open **Terminal** (Applications → Utilities → Terminal, or press `⌘ Space`
and type "Terminal") and run:

```bash
node --version
```

If it prints a version like `v20.11.0` or higher, skip to step 3.

If it says **"command not found"**, install Node.js one of these ways:

- **Download the installer** from [nodejs.org](https://nodejs.org) — pick the
  "LTS" version, open the `.pkg`, and click through. Easiest option.
- **Or, if you use Homebrew:**
  ```bash
  brew install node
  ```

Then close and reopen Terminal, and check `node --version` again.

### 3. Install Pudding's dependencies

In Terminal, `cd` into the folder you unzipped. The easiest way to get the
path right is to type `cd ` (with a space) and then **drag the
`desktop-pudding` folder from Finder into the Terminal window**, then press
Return:

```bash
cd /path/to/desktop-pudding
npm install
```

This downloads Electron (~100 MB) and takes a minute or two the first time.
You only ever need to do this once.

### 4. Start him

```bash
npm start
```

A 🐶 icon appears in your menu bar, the kennel appears in the bottom-right
corner, and Pudding starts snoozing in it.

**To quit:** click the 🐶 in the menu bar → **Quit Desktop Pudding**.

> Note: if you close the Terminal window, Pudding closes with it. To keep him
> running independently, use the double-click launcher below (recommended), or
> start him with `nohup npm start >/dev/null 2>&1 &` instead.

---

## Optional: a double-click launcher

So you don't need Terminal every time, you can make a little app you
double-click to start him.

Run this in Terminal, **replacing the path** with wherever your
`desktop-pudding` folder actually lives:

```bash
PUDDING_DIR="$HOME/Desktop/desktop-pudding"

osacompile -o "$HOME/Desktop/Desktop Pudding.app" -e "
do shell script \"open -n '$PUDDING_DIR/node_modules/electron/dist/Electron.app' --args '$PUDDING_DIR'\"
"
```

You'll get a **Desktop Pudding** app on your Desktop. Double-click it and he
starts — no Terminal window, and he keeps running on his own. You can move
this app to your Applications folder or Dock, but **don't move or rename the
`desktop-pudding` folder** afterwards, or the launcher won't find him.

To have him start automatically every time you log in, add that app under
 → System Settings → General → Login Items.

---

## What he does

**Idle life** — Pudding mostly sleeps in his kennel, but sometimes trots out,
sits or lies down anywhere on the screen, naps there, and eventually heads
home. He roams across **all your monitors**. Click him to pet him (tail wag +
hearts). Drag him to move him. Drag the kennel to reposition it (remembered
between launches).

**Kennel = trash bin** — Drag files or folders onto the kennel: they move into
his "bowl" (a staging folder, like the Trash), so **nothing is deleted yet**.
The badge and the kibble in his bowl show how many items are staged.
Right-click the kennel (or Pudding, or the 🐶 menu-bar icon) for:

- **Feed Pudding — delete N items** — permanently deletes everything in the
  bowl, after one confirmation. Pudding runs over and eats it.
- **Take everything back** — restores staged files to where they came from
  (never overwrites; renames with "(from Pudding)" on collision).
- **Open bowl folder** — inspect what's staged, in Finder.

**Find & fetch** — "Ask Pudding to fetch…" opens a search box (Spotlight under
the hood). For any result:

- **Fetch to Desktop** — moves the file to your Desktop; Pudding carries it
  back and drops it, then a Finder window of your Desktop opens with the file
  selected so you can see exactly what he brought. Never overwrites — renames
  with "(fetched by Pudding)" if needed.
- **Find in Finder** — Pudding dives in, and the file is revealed in Finder.

If the file lives in a folder on your **Desktop**, Pudding dives into that
real folder icon. For files elsewhere on the Mac, a pixel folder pops open
mid-screen and he dives into that instead.

**Commands** (right-click menu / 🐶 menu-bar icon):

- **Sit** — he sits down and stays sitting.
- **Stay** — he holds his spot; after a bit he lies down, and after a while
  longer he falls asleep.
- **Chase the mouse!** — he chases your cursor. If he doesn't catch it within
  a minute he flops down tired, tongue lolling. If he *catches* it, he grabs
  it and parades it around the screen for ten seconds — actually dragging your
  pointer — before letting go.
- **Roam / relax** — cancels sit/stay/chase and returns him to normal life.

Also in the menu: **Stay in the kennel when idle** (keep him home instead of
wandering), **Send Pudding to his kennel**, **Pet Pudding**, **Reset kennel
position**, and **Quit**.

> Chasing moves your real cursor only while he's actually holding it (~10s).
> Any other command — or just moving the mouse away — ends it immediately.

---

## Permissions macOS may ask for

- **"Desktop Pudding wants to control Finder"** — appears the first time you
  fetch a file. Click **OK**. This lets him dive into real Desktop folders and
  open the Finder window showing what he fetched. If you decline, everything
  still works; he just uses the pop-up pixel folder and reveals files in place.

Nothing else is required — no accessibility or screen-recording permissions.

---

## Troubleshooting

**"npm: command not found"** — Node.js isn't installed, or Terminal needs
restarting. See step 2.

**Nothing appears when I run `npm start`** — check for the 🐶 in your menu
bar. If it's there, he's running; he may just be asleep in his kennel or
napping somewhere on another monitor. Use 🐶 → **Reset kennel position** to
bring the kennel back to the bottom-right corner.

**He disappeared after restarting my Mac** — he doesn't start automatically.
Launch him again (or set up the login item described above).

**He seems stuck** — 🐶 → **Roam / relax** puts him back to normal.

---

## For developers

```bash
npm test        # unit tests: bowl staging / take-back / feed / rename logic
npm start       # run the app
```

Layout: `main/` is the Electron main process (windows, the dog's "brain",
file operations); `renderer/` holds the windows and the procedurally-drawn
pixel sprites (`sprites.js` — there are no image assets).

Data lives in `~/Library/Application Support/Desktop Pudding/` (staged files
in `bowl/`, plus `settings.json`). Deleting that folder resets him.

---

## License

MIT — see [LICENSE](LICENSE). © 2026 RolledSalmon
