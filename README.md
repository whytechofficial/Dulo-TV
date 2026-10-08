# Dulo TV for Android

An installable Android WebView wrapper for **https://dulotv.online/**
(movie/TV discovery), built as Cat Building Project 003.

- Package: `com.canejoy.app`
- Current version: **1.0.6** (versionCode 7)
- Built with the CineJoy pattern: `build-apk.sh` drives aapt2 → javac → d8 →
  zipalign → apksigner directly (Gradle can't run in the original build
  sandbox); the Gradle files are kept for reference.

## What it does

- Fullscreen WebView with landscape rotation and keep-screen-on during video.
- **Hosts-based ad blocker** (`app/src/main/assets/adblock-hosts.txt`, 131
  hosts): blocked requests fail, blocked iframes are removed.
- **Navigation allowlist** (`MainActivity.isAllowedNavHost`): top-level page
  navigations may only go to dulotv.online and known media hosts
  (YouTube, TMDB, googlevideo, googleusercontent). Everything else is
  swallowed — this kills the tap-hijack redirect mechanism itself instead of
  chasing rotating ad domains.
- App branding is "Dulo TV" using the site's own red-D logo.

## Build

```bash
./build-apk.sh
```

Produces the APK under `app/build/outputs/apk/debug/`.
`canejoy-debug.keystore` is the debug signing key (not for distribution).

## Note

Binary icon PNGs under `app/src/main/res/mipmap-*` are excluded from this
text-only archive; the APK in the GitHub Release carries the final icons.
