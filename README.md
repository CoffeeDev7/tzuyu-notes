# Tzuyu Notes

A deliberately tiny, local-first notebook app built from scratch.

> **Current goal:** prove that our core notes experience can stay small, understandable, and genuinely cross-platform before we add complexity.

## Why this exists

We originally considered modifying Joplin, but its large multi-platform codebase would make our very small feature set unnecessarily difficult to maintain. Tzuyu Notes takes the opposite approach: build only what we actually want and rely on mature libraries for the hard generic pieces.

## Core values

- **Tiny:** keep our own code around ~2,000 lines or less for the first real version.
- **Cross-platform:** one React/TypeScript UI for Fedora and Android.
- **Local-first:** notes should work without an account or internet connection.
- **Simple:** no unnecessary architecture, services, or abstractions.
- **Private:** future notebook locking/encryption will be designed into the app from the start.
- **No premature sync:** LAN sync comes only after both native apps work reliably.

## Architecture experiment

The current native experiment uses **Tauri 2** as the application shell:

```text
                 React + TypeScript
                         │
                 ┌───────┴───────┐
                 ▼               ▼
             Tauri 2          Tauri 2
                 │               │
                 ▼               ▼
              Fedora          Android
```

The important test is not whether the React app runs in a browser. It is whether the **same frontend becomes a real Fedora application and a real Android application** without maintaining two separate UIs.

The UI is intentionally responsive: wide screens can show multiple panes while narrow screens can show one pane at a time. We should not duplicate the application just because the screens have different dimensions.

## Current proof of concept

The prototype currently supports:

- create notebooks
- create notes inside notebooks
- edit note titles and bodies
- local persistence with `localStorage`
- responsive React UI
- Tauri 2 desktop/mobile scaffolding

There is deliberately **no sync, SQLite, encryption, cloud service, account system, or backend** yet.

## Run in the browser

```bash
git clone https://github.com/CoffeeDev7/tzuyu-notes.git
cd tzuyu-notes
npm install
npm run dev
```

## Run as a native Fedora app

Tauri requires Rust and the Linux system dependencies described in the official Tauri prerequisites. After cloning and installing dependencies:

```bash
npm install
npm run tauri dev
```

A native Tauri window should open. This is the first real cross-platform test.

For a release build:

```bash
npm run tauri build
```

## Run as a native Android app

Android development additionally requires Android Studio, the Android SDK/platform tools, Java, and the Android Rust targets. Tauri's current prerequisites are documented here:

https://v2.tauri.app/start/prerequisites/

Once those are installed, initialize the Android project once:

```bash
npm install
npm run tauri android init
```

Then connect the phone with USB debugging enabled (or use an Android emulator) and run:

```bash
npm run tauri android dev
```

For an installable APK build:

```bash
npm run tauri android build
```

Tauri uses the normal Android Studio project underneath, so Android Studio/SDK setup is part of the native build environment.

## What we are testing now

**Milestone 0 — Native viability**

- [x] Minimal React/TypeScript app
- [x] Notebook + note basics
- [x] Local browser persistence
- [x] Tauri 2 configuration
- [ ] Fedora native window launches
- [ ] Android native app launches
- [ ] Same UI works at both screen sizes
- [ ] Data survives closing/reopening the native apps

Only after this milestone passes do we add real storage and product features.

## Later — only if the native experiment succeeds

- notebook cover images
- images inside notes
- proper SQLite storage
- notebook locking/encryption
- LAN/Wi-Fi sync

Sync is intentionally out of scope for the current experiment.

## Development rule

Every feature should be small enough to understand, build, and test independently. We prefer deleting complexity over adding abstractions.

The project should remain a small personal notes application, not a Joplin clone.
