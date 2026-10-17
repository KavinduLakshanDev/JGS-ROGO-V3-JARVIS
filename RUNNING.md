# JGS ROGO V3: Run Guide

This guide explains how to install, run, stop, and restart JGS ROGO V3 on Windows.

## Requirements

- Windows 10 or Windows 11
- Python 3.11, 3.12, or 3.13 recommended
- A microphone and speakers for voice interaction
- A Gemini API key
- Internet access for installation and Gemini requests

Python 3.14 may work, but this project is tested through Python 3.13.

## First-time setup

Open PowerShell in this project folder:

```powershell
cd "C:\Users\kavin\OneDrive\Documents\GitHub\Personal-Project\JGS-ROGO-V3-JARVIS"
```

Check Python:

```powershell
python --version
```

Install the dependencies and Playwright browsers:

```powershell
python setup.py
```

This installs the Python packages required by the app, including PyQt6, audio support, Gemini support, browser automation, and the Windows integrations.

## Start the application

### Recommended command

```powershell
python main.py
```

The JARVIS window should open. On the first launch, enter your Gemini API key when the setup screen asks for it. The key is saved locally in:

```text
config/api_keys.json
```

Treat this file like a password. Do not share it or commit it to Git.

### Start with the batch file

You can also double-click `app.bat`, or run:

```powershell
.\app.bat
```

The batch file runs `python main.py`.

## API key

Create a Gemini API key from Google AI Studio:

```text
https://aistudio.google.com/app/apikey
```

Paste the key only into the JARVIS setup screen. If the key is missing or invalid, the application can open but Gemini conversations will not work.

If you need to replace the saved key, close JARVIS and remove this file:

```text
config/api_keys.json
```

Then start the app again and enter the new key. This may also remove other saved JARVIS settings.

## Optional features

### Wake word

The local `Hey Jarvis` wake-word engine is optional. Enable or install it from the JARVIS settings area:

```text
Settings -> Wake Word
```

### Remote dashboard

The remote dashboard is started by the main application when its remote-control feature is enabled. It uses port `8000` by default. Follow the URL or QR code shown by JARVIS to connect from another device on the same network.

Do not expose the dashboard to the public internet.

## Stop the application

### Normal stop

Close the JARVIS window using its close button.

### Stop from PowerShell

If JARVIS was started in the current PowerShell window, press:

```text
Ctrl+C
```

### Force stop if it is stuck

Use this only when the normal close does not work:

```powershell
taskkill /IM python.exe /F
```

This stops every Python process running under your Windows user account, so close other Python applications first.

## Restart the application

1. Stop JARVIS using the normal close button or `Ctrl+C`.
2. Start it again:

```powershell
python main.py
```

## Common problems

### `ModuleNotFoundError`

Run the setup script again:

```powershell
python setup.py
```

If a specific package is named in the error, install it with:

```powershell
python -m pip install PACKAGE_NAME
```

Replace `PACKAGE_NAME` with the package named in the error.

### Python version problem

Use Python 3.11, 3.12, or 3.13. If several Python versions are installed, select one explicitly, for example:

```powershell
py -3.13 setup.py
py -3.13 main.py
```

### No microphone or audio

- Check Windows microphone and speaker permissions.
- Check that the correct input and output devices are selected in JARVIS settings.
- Close applications that may have exclusive control of the microphone.

### Playwright browser problem

Install the browser engines again:

```powershell
python -m playwright install chromium firefox
```

### Port `8000` is already in use

Find the process using the port:

```powershell
Get-NetTCPConnection -LocalPort 8000 -ErrorAction SilentlyContinue
```

Stop the application that owns the port, then start JARVIS again.

## Useful commands

Check the installed Python version:

```powershell
python --version
```

Check whether the main dependencies are installed:

```powershell
python -c "import PyQt6, sounddevice, numpy; from google import genai; print('Dependencies OK')"
```

Update the project dependencies:

```powershell
python -m pip install -r requirements.txt --upgrade
```

## Quick reference

| Task | Command |
| --- | --- |
| Install everything | `python setup.py` |
| Run JARVIS | `python main.py` |
| Run with launcher | `.\app.bat` |
| Stop from terminal | `Ctrl+C` |
| Reinstall dependencies | `python -m pip install -r requirements.txt --upgrade` |
| Install Playwright browsers | `python -m playwright install chromium firefox` |
