# 🖥 Windows Terminal Setup Guide

This guide will help you install **WinGet**, **Oh My Posh**, set a **theme**, configure a **Nerd Font**, and set up **custom Fastfetch** for the best terminal experience on Windows.

---

## 🚀 1️⃣ Install WinGet

WinGet is the Windows Package Manager. It works on:

- Windows 10 (1809 or newer, including LTSC)
- Windows 11
- Windows Server 2019/2022

### Install Command

Open **PowerShell as Administrator** and run:

```powershell
Invoke-WebRequest https://raw.githubusercontent.com/imzairaz/Terminal_Ui/master/winget-install.ps1 -UseBasicParsing | iex
````

### Test Installation

```powershell
winget
```

✅ If it prints a list of commands, WinGet is installed successfully.

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

Fallback search if the above is empty:

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

> Applies theme **only for the current session**.

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

### Step 2 — Add the theme line

```powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json" | Invoke-Expression
```

### Step 3 — Save and restart PowerShell

> Theme will now load automatically on every terminal start.

---

## 🔤 6️⃣ Install and Set a Nerd Font

Oh My Posh themes require a Nerd Font for icons.

### Step 1 — Download a Nerd Font

Recommended fonts:

* JetBrainsMono Nerd Font
* FiraCode Nerd Font

Install the `.ttf` file → right-click → **Install** (or **Install for all users**).

### Step 2 — Set Font in Windows Terminal

1. Open **Windows Terminal → Settings → Profiles → PowerShell → Appearance**
2. Font face → type font name (e.g., `JetBrainsMono Nerd Font`)
3. Save and restart terminal

> Legacy PowerShell console: Right-click → Properties → Font → select Nerd Font

---

## ✅ 7️⃣ Quick Verification

```powershell
oh-my-posh --version
```

* Should print version number
* Prompt shows the new theme with icons

---

## ⚠ 8️⃣ Troubleshooting

* **Themes not showing** → check `$POSH_THEMES_PATH` or use fallback search
* **Icons appear as squares** → font not set correctly
* **Theme doesn’t persist** → save `$PROFILE` and restart terminal (`. $PROFILE` reloads it)

---

## 🎨 9️⃣ Optional Tweaks

* Change themes anytime by editing `$PROFILE`
* Use modern themes like `jandedobbeleer` or `tokyonight_storm`
* Enable **transparent background** or **acrylic** for Arch/Linux look

---

## ⚡ 1️⃣0️⃣ Setup Custom Fastfetch

1. Check your PowerShell profile path:

```powershell
$PROFILE
```

> Example: `C:\Users\YOUR_USERNAME\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`

2. If needed, create a new profile:

```powershell
New-Item -Path $PROFILE.CurrentUserAllHosts -Type File -Force
```

3. Copy Fastfetch files from my repo to:

```text
C:\Users\YOUR_USERNAME\.config\fastfetch
```

> Make sure the `.config` folder is hidden.

4. Open `config.jsonc` inside the folder and set your **username** at the source line.

5. Replace your profile file with my `profile.ps1` from the repo:

```text
C:\Users\YOUR_USERNAME\Documents\WindowsPowerShell\profile.ps1
```

> Open `profile.ps1` and update your username.

6. Open a new terminal → BoooM! 🎉

---

> You now have a fully customized **Windows terminal** with Oh My Posh, Nerd Fonts, and Fastfetch for a Linux/Arch-style look. 🖤✨
