# My Visual Studio Code config

My personal Visual Studio Code (and flavours) configuration.

![Example of my setup](https://i.imgur.com/ZymxaDt.png)

The background artwork is by [willfinyu](https://x.com/willfinyu/status/1913437359141802226).

## Installation

If you're using a different flavour of Visual Studio Code,
adjust the `Code` in the filepaths to your IDE.

### Windows (PowerShell)

Prepare a directory

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\Documents\GitHub" | Out-Null
Set-Location "$HOME\Documents\GitHub"
```

Clone the repository

```powershell
git clone https://github.com/LightArrowsEXE/vscode-config.git
Set-Location vscode-config
```

Back up original files

```powershell
If (Test-Path "$env:APPDATA\Code\User\settings.json") {
    Rename-Item "$env:APPDATA\Code\User\settings.json" "settings.backup.json"
}

If (Test-Path "$env:APPDATA\Code\User\keybindings.json") {
    Rename-Item "$env:APPDATA\Code\User\keybindings.json" "keybindings.backup.json"
}
```

Create symlinks (run PowerShell as Administrator)

```powershell
New-Item -ItemType SymbolicLink `
  -Path "$env:APPDATA\Code\User\settings.json" `
  -Target "$PWD\settings.json"

New-Item -ItemType SymbolicLink `
  -Path "$env:APPDATA\Code\User\keybindings.json" `
  -Target "$PWD\keybindings.json"
```


Install extensions

```powershell
Get-Content extensions.txt | ForEach-Object {
    code --install-extension $_
}
```

### Linux

Clone the repository

```bash
git clone https://github.com/LightArrowsEXE/vscode-config.git
cd vscode-config
```

Create symlinks

```bash
ln -s settings.json ~/.config/Code/User/settings.json
ln -s keybindings.json ~/.config/Code/User/keybindings.json
```

Install extensions

```bash
cat extensions.txt | xargs -L 1 code --install-extension
```

## Maintaining `extensions.txt`

After installing or removing extensions,
regenerate the list:

Windows

```powershell
code --list-extensions | Set-Content -Encoding utf8 extensions.txt
```

Linux

```bash
code --list-extensions > extensions.txt
```
