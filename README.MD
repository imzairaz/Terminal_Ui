# 🖥 Windows 10 Terminal Setup Guide

This guide will help you set up a **modern and beautiful Windows terminal** using **WinGet**, **Oh My Posh**, **Nerd Fonts**, and **custom Fastfetch** for a Linux/Arch-style experience.

---

## 📑 Table of Contents

- [🚀 Install WinGet](#-install-winget)
- [🎨 Install Oh My Posh](#-install-oh-my-posh)
- [🔤 Install and Set a Nerd Font](#-install-and-set-a-nerd-font)
- [⚡  Setup Custom Fastfetch](#-setup-custom-fastfetch)
- [❌ Remove Microsoft Edge](#-how-to-remove-microsoft-edge)

---

## 🚀 Install WinGet

WinGet is the Windows Package Manager. Works on:

- Windows 10 (1809 or newer, including LTSC)
- Windows 11
- Windows Server 2019/2022

### Install WinGet

Open **PowerShell as Administrator** and run:

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/imzairaz/Terminal_Ui/master/winget-install.ps1 -UseBasicParsing | iex
````

### Test Installation

```powershell
winget
```

> ✅ If it prints a list of commands, WinGet is installed successfully.

---

## 🎨 Install Oh My Posh

Install via WinGet:

```powershell
winget install JanDeDobbeleer.OhMyPosh --source winget
```

### Verify Installation

```powershell
oh-my-posh --version
```

> If a version number appears, you’re good. Otherwise, reinstall Oh My Posh.

---

### Find and Apply Themes

List installed themes:

```powershell
ls $env:POSH_THEMES_PATH -Filter *.omp.json
```

Fallback search if empty:

```powershell
Get-ChildItem -Path (Split-Path (Get-Command oh-my-posh).Source) -Recurse -Filter *.omp.json
```

> Example filenames: `jandedobbeleer.omp.json`, `paradox.omp.json`
> Use the **name without `.omp.json`** as the theme name.

### Test a Theme Temporarily

Replace `THEME_NAME` with your desired theme:

```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\THEME_NAME.omp.json" | Invoke-Expression
```

> This applies the theme **only for the current session**.

### Make the Theme Permanent

1. Open your PowerShell profile:

```powershell
notepad $PROFILE
```

2. If it doesn’t exist, create it:

```powershell
New-Item -ItemType Directory -Path (Split-Path $PROFILE) -Force
New-Item -ItemType File -Path $PROFILE -Force
notepad $PROFILE
```

3. Add this line (replace theme if desired):

```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json" | Invoke-Expression
```

4. Save and restart PowerShell. Theme will load automatically.

---

## 🔤 Install and Set a Nerd Font

Oh My Posh themes require a Nerd Font for icons.

### Step 1 — Download a Nerd Font

Recommended fonts:

* JetBrainsMono Nerd Font
* FiraCode Nerd Font

Install the `.ttf` → right-click → **Install** (or **Install for all users**).

### Step 2 — Configure Windows Terminal

1. Open **Windows Terminal → Settings → Profiles → PowerShell → Appearance**
2. Set **Font face** to your Nerd Font (e.g., `JetBrainsMono Nerd Font`)
3. Save and restart terminal

> Legacy PowerShell console: Right-click → Properties → Font → select Nerd Font

---

## ⚡ Setup Custom Fastfetch

1. Check your PowerShell profile path:

```powershell
$PROFILE
```

> Example: `C:\Users\YOUR_USERNAME\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`

2. If needed, create a new profile:

```powershell
New-Item -Path $PROFILE.CurrentUserAllHosts -Type File -Force
```

3. Copy Fastfetch files from the repo to:

```text
C:\Users\YOUR_USERNAME\.config\fastfetch
```

> Make sure the `.config` folder is hidden.

4. Open `config.jsonc` inside the folder and set your **username** at the source line.

5. Replace your profile file with `profile.ps1` from the repo:

```text
C:\Users\YOUR_USERNAME\Documents\WindowsPowerShell\profile.ps1
```

> Open `profile.ps1` and update your username.

6. Open a new terminal → BoooM! 🎉

---

> You now have a fully customized **Windows terminal** with **Oh My Posh**, **Nerd Fonts**, and **Fastfetch**, giving you a Linux/Arch-style terminal experience. 🖤✨


## ❌ How to Remove Microsoft Edge

If you want to remove Microsoft Edge from Windows:

1. Download the `removeedge.bat` file from my repo folder named **Remove Edge**.
2. Right-click the file → **Run as Administrator**.
3. Follow the prompts in the script to complete the removal.

> ⚠️ Warning: Removing Edge may affect certain Windows features. Only remove it if you know what you are doing.
