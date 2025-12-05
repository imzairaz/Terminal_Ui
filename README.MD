# 🖥 Windows Terminal Setup Guide

This guide will help you install **WinGet**, **Oh My Posh**, set a **theme**, and configure a **Nerd Font** for the best terminal experience on Windows.

---

## 🚀 1️⃣ Install WinGet

WinGet is the Windows Package Manager. It works on:

- Windows 10 (1809 or newer, including LTSC)
- Windows 11
- Windows Server 2019/2022

### Install Command

Open **PowerShell as Administrator** and run:

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/imzairaz/TerminalUi/master/winget-install.ps1 -UseBasicParsing | iex
````

### Test Installation

```powershell
winget
```

If it prints a list of commands, WinGet is installed successfully ✅

---

## 🎨 2️⃣ Install Oh My Posh

Install via WinGet:

```powershell
winget install JanDeDobbeleer.OhMyPosh --source winget
```

### Verify Installation

```powershell
oh-my-posh --version
```

> If it prints a version number, you’re good. Otherwise, reinstall Oh My Posh.

---

## 🗂 3️⃣ Find Available Themes

List all installed themes:

```powershell
ls $env:POSH_THEMES_PATH -Filter *.omp.json
```

If nothing appears, use this fallback:

```powershell
Get-ChildItem -Path (Split-Path (Get-Command oh-my-posh).Source) -Recurse -Filter *.omp.json
```

> Example theme filenames: `jandedobbeleer.omp.json`, `paradox.omp.json`
> Use the **filename without `.omp.json`** as the theme name.

---

## 🎯 4️⃣ Test a Theme Temporarily

Replace `THEME_NAME` with your desired theme:

```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\THEME_NAME.omp.json" | Invoke-Expression
```

> This will apply the theme **for the current session only**.

---

## 💾 5️⃣ Make a Theme Permanent

### Step 1 — Open PowerShell profile

```powershell
notepad $PROFILE
```

> If the file doesn’t exist:

```powershell
New-Item -ItemType Directory -Path (Split-Path $PROFILE) -Force
New-Item -ItemType File -Path $PROFILE -Force
notepad $PROFILE
```

### Step 2 — Add this line (replace theme name if needed)

```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json" | Invoke-Expression
```

### Step 3 — Save and restart PowerShell

> Your chosen theme will now load automatically on every terminal start.

---

## 🔤 6️⃣ Install and Set a Nerd Font

Oh My Posh themes require a Nerd Font to display icons correctly.

### Step 1 — Download a Nerd Font

Recommended fonts:

* JetBrainsMono Nerd Font
* FiraCode Nerd Font

Install the `.ttf` by right-click → **Install** (or **Install for all users**).

### Step 2 — Set Font in Windows Terminal

1. Open **Windows Terminal → Settings → Profiles → PowerShell → Appearance**
2. Font face → type the font name (e.g., `JetBrainsMono Nerd Font`)
3. Save and restart terminal

> For legacy PowerShell console: Right-click → Properties → Font → select Nerd Font

---

## ✅ 7️⃣ Quick Verification

Open PowerShell:

```powershell
oh-my-posh --version
```

* Should print version number
* Prompt should show the new theme with icons

---

## ⚠ 8️⃣ Troubleshooting

* **Themes not showing** → double-check `$POSH_THEMES_PATH` or use fallback search
* **Icons appear as squares** → font not set correctly
* **Theme doesn’t persist** → ensure profile changes are saved and terminal restarted (`. $PROFILE` can reload it)

---

## 🎨 Optional Tweaks

* Change themes anytime by editing `$PROFILE`
* Use modern themes like `jandedobbeleer` or `tokyonight_storm`
* Combine with **transparent background**, **acrylic**, or **custom colors** for an Arch/Linux look

---

> Now you have a fully customized Windows terminal with Oh My Posh, icons, and a beautiful theme! 🖤✨
