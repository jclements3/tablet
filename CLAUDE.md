# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a distribution repo for pre-built Android APKs targeting ARM64 tablets. There is no source code here — APKs are built in other projects (harp, debar) and committed as binaries for sideloading via ADB or direct download.

## Apps

- **harp/harp-hymnal.apk** — 284-hymn leadsheet viewer with harp voicings (source in `../harp/`)
- **harp/harp-player.apk** — Harp player app (source in `../harp/`)
- **debar/debar-v1.0-release.apk** — Hebrew pictograph Bible study toolkit

## Workflow

APKs are built externally and copied into this repo. The typical update cycle:

1. Build updated APK in the source project
2. Copy APK into the appropriate directory here
3. Commit and push so the tablet can `git pull` to get updates

Install on tablet via:
```bash
adb install <path>.apk        # USB or WiFi ADB
adb install -r <path>.apk     # replace existing install
```
