# 📜 TrinketOS Changelog

## Chapter II — The Impossible Beacon

2025-07-23

### Additions

- New page types
  - Task List (with local and global task list)
  - Web page (open any web page in a scroll design block)
  - Retroarch
  - Tapp (full tab)
- New list items
  - Tapp link
  - Mini-tapp
  - Retroarch link
  - Task list item (only in Task list page)
- New Big Icons
  - Tapp link
  - Retroarch link
- New Trinkets
  - Beacon (links to Beacon interface, is highlighted when new signals are received)

### New features

- Support for smaller, squarish, vertical screens
- Support running on Android down to 6 (SDK23)

- Design
  - Horizontal margins
  - Vertical margins
  - Asymmetry
  - Resize large backgrounds (saves them to Images folder)
  - Pixelation level for backgrounds
  - One page mode
  - UI scale
  - Screen orientation setting (automatic or manual)
  - Create custom glyphs and use them as icons
  - Create custom colors
  - Choose cursor image
  - Support for custom animated backgrounds (use .gif files)
- Workshop
  - Colorize icons/images for Big Icons
  - Pixelate images fro Big Icons
  - Hide edit buttons for Task List
- Sound
  - Mood music control
  - Music now tries to resume from the same place it was paused (e.g. when opening an app)
- Controls
  - Keyboard remapping
  - Added control WiFi and Bluetooth to button roles
  - Added Page Switch (for One Page mode) to button roles
- System
  - Hide screen when locked with glyph
  - Added resettings name and icon of apps
- Trinkets
  - Selection of custom time zone
- Added confirmation when resetting all types of settings

Tapps and Mini-tapps (check tapps_howto.md)

### Fixes

- Scrolling/selection mechanism received big updates, now it correctly remembers the previous and other-page selections
- Copying big files no more leads to crash
- Large background files do not slow down the system if they are resized
- Fixed hidden apps resetting on restart
- Fixed disabled sounds resetting on restart
- Fixed clock display (e.g. minutes not displaying on some settings)
- Fixed SD card shown twice in File Page
- Fixed Dpad and sticks not changing volume and brightness on Big Icons pages
- Fixed Sprite position resetting or not visible on settings change or restart
- Fixed not-centered icons (like Monitor, Glasses)
- Fixed occasional errors with Tabs editing (due to their naming)
- Fixed Sprite trying to talk when it is hidden
- Apps are now sorted alphabetically including renamed ones
- Reworked screen masking system, so it is more lightweight

## Chapter I — Dweller

2025-06-11

**Initial public release of TrinketOS.**  
A pixel-crafted, controller-first launcher designed for Android-based handhelds. More than a launcher — a terminal shell with personality, widgets, achievements, and hats.

---

### ✨ Core Features

- **Tab-based layout**: Create, reorder, rename, and iconify up to two-page custom tabs.
- **Page types**: Support for app/shortcuts lists, text files, images, file lists, custom lists and big icons horizontal lists.
- **Settings tab** (non-removable): Access all controls and configuration sectors.

---

### 🧩 Trinkets

- Top
  - Clock
  - Date
  - Hat
  - Moon phase
  - Zodiac sign
  - Custom image
  - Custom text
  - Dice
- Bottom
  - Status
    - SD Card
    - External screen/AR glasses
    - Bluetooth
    - Wi-Fi
  - Status with bar/number
    - Battery
    - Screen brightness
    - Sound volume
  - Music player

---

### 🎮 Controller Support

- Full navigation with D-Pad or stick
- Assign any action to any button (open tabs, control music, etc.)
- Custom selection logic (no default Android rectangles)

---

### 🎨 Design & Personalization

- Colors with loreful names
- Pixel icon set
- Customizable backgrounds (general and separate for tabs and for big icons pages)
- Glyph-based screen lock

---

### 🧙 Sprite Companions

- Two skins: Merlin the Wizard and Robert the Robot
- Companions blink, sleep, speak, and react to system events
- Draggable & thematically aware

---

### 🎩 Skills, Hats & Achievements

- Track progress in skills: `Adventurer`, `Artist`, `Engineer`, `Patron`, `Bard`
- Unlock themed hats with skill levels
  - Example: play games to gain Adventurer XP, tinker with design to gain Artist XP
- Get achievements

---

### 🧾 Glyph ID System

- Users that participate in the project or support us receive unique visual glyphs (instead of traditional codes)
- Supports simple one-time remote verification of supporters via GitHub JSON (with salt) — no hidden databases or constant online requests

---

### 📁 Workbench Tools

- Text/Markdown files viewer
- Glyph editor (with visual grid)
- File explorer with basic actions
- Image files viewer
- Big icons configuration
- App//shortcut management

---

### 🧠 Meta & Community

- Built-in version screen with trinket name, art, and lore
- “Inventory” section to browse past versions and updates
- Sprite speaks lore-dependent phrases on boot

---

Made with care, soldered in solitude, and offered freely to fellow explorers of strange UIs.
