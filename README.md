# Simple Miniplayer

> A "Cinematic Terminal" Picture-in-Picture experience for web videos, Reels, and Shorts.

<img width="800" height="600" alt="Simple Miniplayer Interface Mockup" src="https://github.com/user-attachments/assets/39152ecd-8c5a-4b17-8750-7ac8e34832b2" />

---

## Overview

**Simple Miniplayer** is a browser extension designed to provide a high-performance Picture-in-Picture (PiP) experience. Utilizing the Document Picture-in-Picture API, it moves videos out of their webpage constraints and into a floating cinematic window. 

Whether you are watching YouTube, scrolling through Instagram Reels, browsing TikTok, or navigating nested frames and Shadow DOMs, Simple Miniplayer manages playback using a priority-ordered multi-tier rendering engine.

---

## Key Features

Traditional Picture-in-Picture tools are restricted by same-origin policies, iframe isolation, and customized site interfaces. Simple Miniplayer works around these limitations with a specialized architecture:

*   **Tiered Rendering (The Capture Chain)**: 
    *   *Tier 1 (Direct PiP)*: Moves the actual `<video>` element into the Document PiP window for zero-latency native playback.
    *   *Tier 2 (Iframe Proxy)*: For same-origin iframes, mirrors the video onto a `<canvas>` element in the PiP window.
    *   *Tier 3 (Iframe Relay)*: For cross-origin iframes, captures frames as `ImageBitmap` objects and relays them via optimized `postMessage` tunnels.
    *   *Tier 4 (Secure Fallback)*: Handles DRM-restricted content (HDCP, Widevine) by displaying a fallback HUD while maintaining audio and playback synchronization.
*   **SyncManager Layer**: A high-speed, cross-frame pub/sub event bus built on `chrome.storage.session`. Play/Pause, Seek, and Volume sync across frames without heavy message cascading.
*   **Video Discovery**: Uses an iterative Breadth-First-Search (BFS) scanner to traverse all Shadow DOMs and iframes, detecting and prioritizing playing or visible videos.
*   **Animated Subtitles**: Captures captions from the TextTrack API or DOM observers (such as YouTube's caption element) and renders them in the PiP window with smooth rolling animations.
*   **Persistent Audio Visualizer**: A shared `AudioContext` that remains connected even if the PiP window is minimized, bridging real-time frequency data into terminal-inspired visualizers.
*   **"Cinematic Terminal" Design System**: Glassmorphism backgrounds (`hsla(0, 0%, 5%, 0.9)` with a `backdrop-filter: blur(20px)`), neon cyan/amber interactive states, and `Space Mono` typography.

---

## Installation

Install the extension directly from the [Chrome Web Store](https://chromewebstore.google.com/detail/simple-player-universal-p/nbhenlkfbomgopnkecffgfennnobejfn?authuser=1&hl=en).

---

## How to Use

*   **Launch PiP**: Click the extension icon in your browser action bar, or use the global hotkey:
    *   `Alt + P` (Windows/Linux)
    *   `Command + Shift + P` (macOS)
*   **Toggle Playback**: Spacebar or click the main window control.
*   **Volume Adjustment**: Scroll or use Up/Down arrow keys on your keyboard.
