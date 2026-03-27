# Tablet Apps

Pre-built Android APKs for ARM64 tablets.

## Apps

| App | Description | APK |
|-----|-------------|-----|
| **Harp Hymnal** | 284-hymn leadsheet viewer with harp voicings | `harp/harp-hymnal.apk` |
| **Debar** | Hebrew pictograph Bible study toolkit | `debar/debar-v1.0-release.apk` |

## Install

On the tablet:

```bash
# Clone (one-time)
git clone https://github.com/jclements3/tablet.git

# Install APKs
adb install tablet/harp/harp-hymnal.apk
adb install tablet/debar/debar-v1.0-release.apk
```

Or download the APK files directly from GitHub, transfer to the tablet, and tap to install.

## Refresh

When apps are updated in the lab:

```bash
cd tablet
git pull
# reinstall whichever APKs changed
```
