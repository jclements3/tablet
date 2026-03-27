# Tablet Setup Guide

First-time setup for the 2026 13" Android 16 tablet (ARM64 octa-core, 1920x1200, 32GB RAM).

## 1. Enable Developer Options

1. Open **Settings > About tablet**
2. Tap **Build number** 7 times until it says "You are now a developer"
3. Go back to **Settings > System > Developer options**
4. Enable **USB debugging**
5. Enable **Install via USB** (allows ADB sideloading)

## 2. Allow Unknown App Installs

1. Open **Settings > Apps > Special app access > Install unknown apps**
2. Enable for **Files** (or whichever file manager you use)
3. This lets you tap APK files to install them

## 3. Install Apps via USB from Lab/Home PC

Connect the tablet to your Ubuntu machine via USB-C cable.

```bash
# Verify the tablet is connected
adb devices
# Should show something like: XXXXXXXXX  device
# First time: approve the USB debugging prompt on the tablet

# Install apps
adb install tablet/harp/harp-hymnal.apk
adb install tablet/debar/debar-v1.0-release.apk
```

If `adb` is not installed on the home machine:

```bash
sudo apt install android-tools-adb
```

## 4. Install Apps Without a PC

If you don't have a USB cable handy:

1. Open Chrome on the tablet
2. Go to https://github.com/jclements3/tablet
3. Tap into `harp/` or `debar/` folder
4. Tap the APK file, then tap **Download**
5. Open the downloaded `.apk` from notifications or Files app
6. Tap **Install** (approve the unknown sources prompt if needed)

## 5. Install Apps via Termux (Advanced)

Termux gives you a Linux terminal on the tablet itself — useful for git pull workflows.

1. Install **Termux** from F-Droid (not Play Store — the Play Store version is outdated)
   - Download from: https://f-droid.org/en/packages/com.termux/
2. Open Termux and run:

```bash
# One-time setup
pkg update && pkg upgrade
pkg install git

# Clone the repo
git clone https://github.com/jclements3/tablet.git
cd tablet

# Install an APK from Termux (requires Termux:API addon)
# Or just use the file manager to tap the APKs:
termux-open harp/harp-hymnal.apk
termux-open debar/debar-v1.0-release.apk
```

3. To refresh apps after lab updates:

```bash
cd ~/tablet
git pull
termux-open harp/harp-hymnal.apk
```

## 6. WiFi ADB (No Cable Needed)

Once paired the first time, you can install over WiFi from any machine on the same network.

On the tablet:
1. Go to **Settings > System > Developer options**
2. Enable **Wireless debugging**
3. Tap **Pair device with pairing code** — note the IP:port and pairing code

On your Ubuntu machine:

```bash
# Pair (one-time)
adb pair <ip>:<pairing-port>
# Enter the pairing code when prompted

# Connect
adb connect <ip>:<port>

# Now install as usual
adb install tablet/harp/harp-hymnal.apk
```

## 7. Keyboard and Mouse Setup

The tablet comes with a keyboard case and mouse. These should work out of the box. A few useful settings:

- **Settings > System > Languages & input > Physical keyboard** — set layout to US QWERTY
- **Settings > Display > Screen timeout** — set to 30 minutes for practice sessions

## App Notes

### Harp Hymnal
- Opens full-screen with 284 hymns pre-loaded
- Use the key selector and mode buttons at the top to transpose
- Leadsheet wraps to fit the screen width
- No internet required — everything is embedded in the app

### Debar (Pictograph Bible)
- Hebrew pictograph study toolkit
- Works offline after first install
- Uses WebView — similar to running in Chrome

## Troubleshooting

**"App not installed" error:**
- Make sure **Install via USB** is enabled in Developer options
- Try: `adb install -r <app>.apk` (the `-r` flag replaces an existing install)

**ADB doesn't see the tablet:**
- Try a different USB cable (some are charge-only)
- Revoke USB debugging authorizations in Developer options and re-approve

**App crashes on launch:**
- Check logcat: `adb logcat | grep -i crash`
- Make sure you're using the ARM64 APK (not the x86_64 emulator build)
