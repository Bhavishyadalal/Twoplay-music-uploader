<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:FF6FA5,100:7C9CFF&height=220&section=header&text=twoplay&fontSize=70&fontColor=ffffff&fontAlignY=38&desc=Cozy%20music%20uploader%20—%20sends%20tracks%20straight%20to%20your%20repo&descAlignY=58&descSize=18&animation=fadeIn" width="100%"/>

<br/>

<a href="#">
  <img src="https://readme-typing-svg.demolab.com?font=Baloo+2&weight=700&size=22&duration=2800&pause=900&color=FF6FA5&center=true&vCenter=true&width=520&lines=Drop+in+a+few+MP3s...;playlist.json+updates+itself+%F0%9F%8E%B5;GitHub+as+your+free+music+CDN;No+backend.+No+database.+Just+a+repo." alt="Typing SVG" />
</a>

<br/><br/>

<img src="https://img.shields.io/badge/status-purring-FF6FA5?style=for-the-badge&labelColor=2B1F30" />
<img src="https://img.shields.io/badge/backend-none-7C9CFF?style=for-the-badge&labelColor=2B1F30" />
<img src="https://img.shields.io/badge/storage-your%20repo-4CAF7D?style=for-the-badge&labelColor=2B1F30" />
<img src="https://img.shields.io/badge/made%20with-%E2%99%A5-FF6FA5?style=for-the-badge&labelColor=2B1F30" />

</div>

<br/>

<p align="center">
  <img src="https://img.shields.io/badge/HTML-single--file-E85D5D?style=flat-square&logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/JS-vanilla-F7DF1E?style=flat-square&logo=javascript&logoColor=black" />
  <img src="https://img.shields.io/badge/GitHub%20API-contents-181717?style=flat-square&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/hosting-GitHub%20Pages-222?style=flat-square&logo=githubpages&logoColor=white" />
</p>

<p align="center">🐾 · 🎵 · ✨ · 🎵 · 🐾</p>

---

## 🐱 What is this?

**twoplay** is a tiny, cozy dashboard that turns any GitHub repo into a music library.

Paste a personal access token, drag in a stack of MP3s, and they land straight in your repo's `music/` folder — no server, no database, no build step. `playlist.json` keeps itself in sync, and your site just reads from it.

Built for one thing: **making it stupidly easy to add tracks to a personal music site without ever opening a terminal.**

<div align="center">

|  |  |  |
|:---:|:---:|:---:|
| 🎧 **Drop & go** | 🔄 **Self-healing** | 📦 **Zero backend** |
| Drag in several files, they queue up automatically | Detects a corrupted playlist and rebuilds it from your actual files | Everything lives in your GitHub repo — token never leaves the browser |

</div>

---

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 🚀 Upload flow
- Multi-file drag & drop, queued and previewable
- Per-track cover art, custom titles, duplicate detection
- Parallel uploads, then **one single commit** to `playlist.json`
- Real retry logic for GitHub's read‑after‑write delay — no more random "sync conflict" fails

</td>
<td width="50%" valign="top">

### 🎛️ Library management
- Search, manual drag-reorder, sort by title / date / duration
- Inline rename, tag, and delete with bulk actions + undo
- Built-in mini player with waveform-style scrubber
- Live repo stats — storage used, tracks added this week

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🛡️ Reliability
- Token expiry warnings before things break
- Human-readable errors instead of raw API noise
- One-click **rebuild playlist.json** from real files on GitHub
- Internally-scrolling track list — the dashboard never gets unwieldy

</td>
<td width="50%" valign="top">

### 🎨 Vibes
- Tournament-cozy, hand-drawn accents, floating paw prints
- Light & dark theme, both equally soft
- A tiny cat mascot that reacts to upload state
- Keyboard shortcuts for the mouse-averse

</td>
</tr>
</table>

---

## 🧵 How it works

```
   you                 twoplay                    your repo
 ┌─────┐        ┌──────────────────┐        ┌────────────────────┐
 │ 🎵  │  drop   │                  │  PUT   │  music/track.mp3   │
 │ mp3 │ ──────► │  reads & queues  │ ─────► │  music/track2.mp3  │
 │ mp3 │         │  each file       │        │  ...                │
 └─────┘         │                  │        └────────────────────┘
                  │  merges titles/  │                 │
                  │  covers/order    │      one commit ▼
                  └──────────────────┘        ┌────────────────────┐
                                               │  music/playlist.json│
                                               │  [ {file, title,   │
                                               │     cover, tags} ] │
                                               └────────────────────┘
```

1. **Paste a GitHub token** — classic PAT with `repo` scope, kept only in your browser (`localStorage`, optionally)
2. **Drop your tracks** — queue shows size, cover art, duplicate warnings
3. **Hit upload** — files go up first (in parallel), then a single `playlist.json` commit merges them all in
4. **Your site reads `playlist.json`** — done, tracks are live

---

## 🗂️ Repo layout

```text
your-repo/
└── music/
    ├── playlist.json      ← the single source of truth
    ├── track-one.mp3
    ├── track-two.mp3
    └── ...
```

`playlist.json` looks like this:

```json
[
  {
    "file": "midnight-drive.mp3",
    "title": "Midnight Drive",
    "cover": "data:image/jpeg;base64,...",
    "addedAt": "2026-08-20T18:04:00.000Z",
    "duration": 214
  }
]
```

---

## 🔑 Getting started

<table>
<tr><td>

**1.** Generate a token at [github.com/settings/tokens](https://github.com/settings/tokens) → *Generate new token (classic)* → check the **`repo`** box

**2.** Open the dashboard, paste your token into **GitHub access**

**3.** Drop in some MP3s, hit **Upload**

**4.** That's it — check `music/` in your repo 🎉

</td></tr>
</table>

> **Note:** the token only ever talks to `api.github.com` directly from your browser. Nothing is sent to, or stored on, a server.

---

## 🩹 Self-healing playlist

If `playlist.json` ever gets corrupted (interrupted write, dropped connection, whatever) — twoplay notices, rebuilds it straight from the actual files sitting in `music/`, and writes a clean copy back automatically. Or hit **Rebuild** yourself if you want to force it.

<div align="center">
<sub>corrupt JSON in → real files scanned → fresh <code>playlist.json</code> out → life goes on</sub>
</div>

---

## 🎨 Theme

<div align="center">

| | | | |
|:---:|:---:|:---:|:---:|
| ![#FF6FA5](https://placehold.co/60x60/FF6FA5/FF6FA5.png) | ![#7C9CFF](https://placehold.co/60x60/7C9CFF/7C9CFF.png) | ![#4CAF7D](https://placehold.co/60x60/4CAF7D/4CAF7D.png) | ![#E85D5D](https://placehold.co/60x60/E85D5D/E85D5D.png) |
| `#FF6FA5` accent | `#7C9CFF` accent-2 | `#4CAF7D` good | `#E85D5D` bad |

*Font pairing: **Baloo 2** for display, a soft rounded body font underneath. Felt-cozy, not corporate.*

</div>

---

<div align="center">

### 🐾 built with love, one commit at a time 🐾

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:7C9CFF,100:FF6FA5&height=100&section=footer" width="100%"/>

</div>
