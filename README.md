# Tzuyu Notes

A deliberately tiny, local-first notebook app built from scratch.

> **Current goal:** prove that our core notes experience can stay small, understandable, and cross-platform before we add complexity.

## Why this exists

We originally considered modifying Joplin, but its large multi-platform codebase would make our very small feature set unnecessarily difficult to maintain. Tzuyu Notes takes the opposite approach: build only what we actually want and rely on mature libraries for the hard generic pieces.

## Core values

- **Tiny:** keep our own code around ~2,000 lines or less for the first real version.
- **Cross-platform:** one React/TypeScript UI for Fedora and Android.
- **Local-first:** notes should work without an account or internet connection.
- **Simple:** no unnecessary architecture, services, or abstractions.
- **Private:** future notebook locking/encryption will be designed into the app rather than bolted onto another application's model.
- **No premature sync:** LAN sync is intentionally postponed until the local apps work correctly on both platforms.

## Current proof of concept

The current prototype intentionally does only a few things:

- create notebooks
- create notes inside notebooks
- edit note titles and bodies
- persist data locally with `localStorage`
- run as a normal React web application

It is **not yet the final desktop/Android application**. Tauri is the next step after this tiny web proof-of-concept is verified.

## Planned direction

```text
React + TypeScript
        │
        ├── Fedora → Tauri
        │
        └── Android → Tauri
        │
        ▼
     Local storage
        │
        ▼
     Notes / notebooks
```

Later, and only after the above is stable:

- notebook cover images
- notebook locking/encryption
- images inside notes
- proper SQLite storage
- LAN/Wi-Fi sync

Sync is deliberately **not** part of the current prototype.

## Development rule

Every feature should be small enough to understand, build, and test independently. We prefer deleting complexity over adding abstractions.

The project should remain a personal notes application, not a Joplin clone.

## Run the current prototype

Requirements: Node.js and npm.

```bash
git clone https://github.com/CoffeeDev7/tzuyu-notes.git
cd tzuyu-notes
npm install
npm run dev
```

Then open the local Vite URL shown in the terminal.

## Project status

- [x] Repository created
- [x] Minimal React/TypeScript prototype
- [x] Notebook CRUD basics
- [x] Note CRUD basics
- [x] Local persistence
- [ ] Tauri desktop shell
- [ ] Android build
- [ ] Notebook covers
- [ ] Images in notes
- [ ] Notebook locking
- [ ] SQLite
- [ ] LAN sync
