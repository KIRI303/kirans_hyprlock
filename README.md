# 🔒 Hyprlock Config

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Hyprland](https://img.shields.io/badge/Hyprland-0.55+-58E1FF)](https://hyprland.org/)
[![hyprlock](https://img.shields.io/badge/hyprlock-config-b4befe)](https://github.com/hyprwm/hyprlock)
[![Last commit](https://img.shields.io/github/last-commit/YOUR_USERNAME/YOUR_REPO?color=a6e3a1)](https://github.com/YOUR_USERNAME/YOUR_REPO/commits)
[![Stars](https://img.shields.io/github/stars/YOUR_USERNAME/YOUR_REPO?color=f9e2af)](https://github.com/YOUR_USERNAME/YOUR_REPO/stargazers)
[![Forks](https://img.shields.io/github/forks/YOUR_USERNAME/YOUR_REPO?color=89b4fa)](https://github.com/YOUR_USERNAME/YOUR_REPO/network/members)

A minimal, centered lock screen for [Hyprland](https://hyprland.org/) built with [hyprlock](https://github.com/hyprwm/hyprlock). It uses a blurred wallpaper, a soft Catppuccin-style password field, a round avatar, a big clock, and a Japanese greeting.


## 🎬 Preview


https://github.com/user-attachments/assets/a0829511-4298-4aa9-bef2-51ba2c96eb96



## ✨ What's on the lock screen

| Element | Description |
|---|---|
| **Background** | A wallpaper with a light blur (`blur_passes = 2`, `blur_size = 2`) |
| **Clock** | Large `HH:MM` time in *Comfortaa*, updating every second |
| **Date** | Full date (e.g. `Thursday, 19 November 2026`) in *Monsieur La Doulaise*, updating every minute |
| **Avatar** | A circular 80px image above the password field |
| **Greeting** | `おかえり, 七転び八起き` ("Welcome back. Fall seven times, get up eight.") in *JetBrainsMono Nerd Font* |
| **Password field** | 300×50 rounded input with a lavender outline and dark translucent fill |
| **Cursor** | Hidden while locked (`hide_cursor = true`) |

### 🎨 Colors

| Part | Value |
|---|---|
| Outline | `rgba(180, 190, 254, 1.0)` (lavender) |
| Input background | `rgba(30, 30, 46, 0.9)` (dark base) |
| Input text | `rgba(205, 214, 244, 1.0)` (soft white) |
| Labels | `rgba(255, 255, 255, 1.0)` (white) |

---

## 📦 Requirements

- [Hyprland](https://hyprland.org/)
- [hyprlock](https://github.com/hyprwm/hyprlock)
- These fonts:
  - [JetBrainsMono Nerd Font](https://www.nerdfonts.com/font-downloads)
  - [Comfortaa](https://fonts.google.com/specimen/Comfortaa)
  - [Monsieur La Doulaise](https://fonts.google.com/specimen/Monsieur+La+Doulaise)
  - A font with Japanese glyphs (e.g. `noto-fonts-cjk`) for the greeting

### Install on Arch Linux

```bash
sudo pacman -S hyprlock noto-fonts-cjk ttf-jetbrains-mono-nerd ttf-comfortaa
yay -S ttf-monsieur-la-doulaise   # or install it manually from Google Fonts
```

On other distros, install `hyprlock` and the fonts with your package manager, or drop the font files into `~/.local/share/fonts/` and run `fc-cache -fv`.

---

## 🚀 Installation

### 1. Clone this repo

```bash
git clone https://github.com/KIRI303/kirans_hyprlock.git
cd kiran_hyprlock
```

### 2. Back up your existing config (optional but recommended)

```bash
mv ~/.config/hypr/hyprlock.conf ~/.config/hypr/hyprlock.conf.bak
```

### 3. Copy the config and assets

```bash
mkdir -p ~/.config/hypr/assets
cp hyprlock.conf ~/.config/hypr/hyprlock.conf
cp -r assets/* ~/.config/hypr/assets/
```

### 4. ⚠️ Update the file paths

The original config uses absolute paths from the author's machine. Open `~/.config/hypr/hyprlock.conf` and change them to your own:

```ini
background {
    path = /home/YOUR_USER/.config/hypr/assets/red.png
}

image {
    path = /home/YOUR_USER/.config/hypr/assets/blue-circle.png
}
```

You can use any wallpaper and avatar you like, and change the greeting text to anything you want.

### 5. Test it

Run this from a terminal inside your Hyprland session:

```bash
hyprlock
```

Your lock screen should appear. Type your password to unlock.

---

## ⌨️ Launch hyprlock from your Hyprland config

Newer Hyprland versions (0.55+) use **Lua** for configuration, so your main config is `~/.config/hypr/hyprland.lua`. Older versions use `hyprland.conf` (Hyprlang). Use whichever matches your setup.

> Note: `hyprlock.conf` itself stays in the same format. Only the main Hyprland config changed.

### Lua (`hyprland.lua`)

Add a keybind to lock the screen. Check the example config shipped at `/usr/share/hypr/hyprland.lua` for the exact style used by your version:

```lua
-- Lock screen with SUPER + L
hl.bind("SUPER + L", hl.dsp.exec_cmd("hyprlock"))
```

To lock automatically on startup (optional):

```lua
hl.on("hyprland.start", function()
    hl.exec_cmd("hyprlock")
end)
```

### Hyprlang (`hyprland.conf`, older versions)

```ini
bind = SUPER, L, exec, hyprlock

# optional: lock on startup
exec-once = hyprlock
```

### Auto-lock when idle (optional)

Use [hypridle](https://github.com/hyprwm/hypridle) in `~/.config/hypr/hypridle.conf`:

```ini
general {
    lock_cmd = pidof hyprlock || hyprlock
    before_sleep_cmd = loginctl lock-session
}

listener {
    timeout = 300
    on-timeout = loginctl lock-session
}
```

---

## 🛠️ Customization

| Want to change... | Edit this |
|---|---|
| Wallpaper | `background { path = ... }` |
| Blur strength | `blur_passes`, `blur_size` |
| Avatar | `image { path = ... }` and `size` |
| Greeting text | the `text =` line in the greeting `label` |
| Time format | `date +"%H:%M"` (use `%I:%M %p` for 12-hour) |
| Date format | `date +"%A, %d %B %Y"` |
| Colors | `outer_color`, `inner_color`, `font_color` |
| Positions | `position = x, y` on each element |

See the [hyprlock wiki](https://wiki.hypr.land/Hypr-Ecosystem/hyprlock/) for every available option.

---

## 🧯 Troubleshooting

- **Japanese text shows as boxes:** install a CJK font such as `noto-fonts-cjk`.
- **Fonts look wrong:** run `fc-list | grep -i comfortaa` to confirm the font is installed, then `fc-cache -fv`.
- **Images don't show:** the `path` must be correct and absolute (or start with `~`).
- **Locked out while testing:** switch to a TTY (`Ctrl + Alt + F3`), log in, and run `pkill hyprlock`.

---

## 📁 Repo structure

```
.
├── hyprlock.conf
├── assets/
│   ├── red.png
│   ├── blue-circle.png
├── vdo/
│   ├── preview.mp4
│   └── preview.gif
├── LICENSE
└── README.md
```

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

Wallpapers, avatar images, and fonts may have their own licenses. Please check the original sources before redistributing them.

---

## 🙏 Credits

- [Hyprland](https://hyprland.org/) and [hyprlock](https://github.com/hyprwm/hyprlock) by the Hypr project
- Color palette inspired by [Catppuccin](https://github.com/catppuccin/catppuccin)
