<div align="center">

# 🛡️ Rust Shield Browser

**A Rust-powered browser prototype for Windows, with an experimental cross-platform roadmap.**

![Rust](https://img.shields.io/badge/Rust-2021_edition-000000?logo=rust&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-10%20%2F%2011-0078D4?logo=windows&logoColor=white)
![WebView2](https://img.shields.io/badge/Rendering-WebView2-5C2D91)
![Status](https://img.shields.io/badge/Status-early%20development-orange)
![License](https://img.shields.io/badge/License-check%20repository-lightgrey)

**[Source repository](https://github.com/Galax71/Rust-Brave-inspired-Browser) · [Public release repository](https://github.com/Galax71/Rust-Shield-Releases) · [Build documentation](BUILD-ARTIFACTS.md)**

</div>

> [!IMPORTANT]
> **Work in progress — not a finished or security-audited browser.** This project is not affiliated with Brave Software, Mozilla, Google, Microsoft, Apple, or any other browser vendor. A familiar interface does **not** imply the corresponding browser's security, privacy, extensions, or features.

## Overview

Rust Shield is an independent browser experiment written primarily in Rust. Its current Windows prototype uses **winit** for the application window and **wry / Microsoft Edge WebView2** for rendering. The goal is to explore configurable browser layouts, practical desktop navigation, and a lightweight architecture. **WebView2 is the current Windows renderer; a Servo-based browser engine is not implemented as the primary renderer.**

## Feature status legend

| Color | Meaning | Evidence required |
| --- | --- | --- |
| 🟢 **Green — Working** | Fully implemented **and verified functional** | Successful relevant test or user-confirmed working behavior |
| 🟡 **Yellow — Needs testing** | Implemented, but functionality is unverified or incomplete testing remains | Code exists; successful end-to-end behavior is not yet established |
| 🔴 **Red — Not functional** | Feature exists but is known to fail or behave incorrectly | Reproducible issue or reported failure |
| ⚪ **Gray — Not implemented** | Feature does not exist yet | No functional implementation in the current prototype |

> **Conservative ratings:** Code presence is not proof that a feature works. Green is reserved for verified behavior; the current prototype's unverified features remain yellow. Status applies to the Windows prototype unless a platform is explicitly named.

## Feature implementation and functionality matrix

| Feature | Status | Notes |
| --- | --- | --- |
| Windows application launches | 🟢 **Working** | User has launched and tested the prototype on Windows |
| Custom title-bar minimize, maximize, close | 🟢 **Working** | User-confirmed controls |
| Basic left/right window snapping | 🟢 **Working** | User-confirmed left/right snapping |
| WebView2 webpage rendering | 🟢 **Working** | User has opened and interacted with the prototype |
| Address/search and navigation controls | 🟡 **Needs testing** | Implemented; comprehensive behavior not verified |
| Tab creation, switching, closing | 🟡 **Needs testing** | Implemented, but switching discards inactive WebViews and loses live page state |
| Browser-inspired toolbar themes | 🟡 **Needs testing** | Presets exist; not all layouts verified |
| Settings and persistence | 🟡 **Needs testing** | Code exists; full end-to-end validation outstanding |
| Two-way and four-way Snap Layout previews | 🟡 **Needs testing** | Preview UI implemented; native Windows integration absent |
| Print Screen / Snipping Tool while focused | 🔴 **Not functional** | Reported to fail when Rust Shield has focus |
| Resize borderless window from edges/corners | 🔴 **Not functional** | Dragging borders does not resize the window |
| Floating Snap Layout popup | 🔴 **Not functional** | Current popup expands toolbar and shifts webpage |
| Windows native multi-app Snap Assist | ⚪ **Not implemented** | Custom positioning is not the Windows Snap Assist picker |
| Preserve inactive tab state | 🔴 **Not functional** | Switching tabs intentionally destroys inactive WebViews |
| Approved taskbar/application icon | ⚪ **Not implemented** | Approved artwork not integrated into Windows executable |
| Built-in content/ad blocking and privacy shields | ⚪ **Not implemented** | No verified blocking engine |
| Tor browsing and isolated tab processes | ⚪ **Not implemented** | Not available in prototype |
| Extension compatibility | ⚪ **Not implemented** | No extension subsystem |
| Verified installer and signed release | ⚪ **Not implemented** | No verified signed installer |
| Servo as primary rendering engine | ⚪ **Not implemented** | WebView2 remains the current Windows renderer |
| Linux/macOS functional builds | 🟡 **Needs testing** | Prototype source exists, not tested |
| Android browser application | ⚪ **Not implemented** | Documentation/planning only |

## What is implemented today?

| Area | Current state |
| --- | --- |
| Windows application | Rust desktop prototype with custom borderless window controls |
| Rendering | WebView2-powered embedded browser pages |
| Navigation | Address/search input, back, forward, reload, and home commands |
| Tabs | Create, switch, and close tabs; inactive views may be discarded to reduce memory |
| Appearance | Several browser-inspired toolbar presets and custom styling |
| Settings | Settings interface and persisted browser preferences |
| Window layouts | Custom two-way and four-way snap preview UI; not native Windows Snap Assist |
| Search | Brave Search default, with other search engine options in the prototype |

**Important limitation:** Switching away from a tab can destroy its WebView and later reload its URL. Unsaved forms, page state, and media playback may be lost. Do not rely on this prototype for sensitive or important browsing.

## Known issues and work in progress

- **Print Screen:** Windows' PrtSc/Snipping Tool shortcut may not activate while Rust Shield has focus.
- **Window resizing:** Dragging the edges and corners of the borderless window is not yet working.
- **Snap preview:** The popup currently expands the toolbar WebView, which can shift the page downward.
- **Snap Assist:** Selecting a custom snap zone repositions Rust Shield, but does not yet integrate with Windows' native multi-app Snap Assist.
- **Windows trust prompts:** Microsoft Defender may scan newly built, unsigned executables. This alone is not a malware finding. Do not disable Defender to run the app.

These items are **not fixed merely by changing this README**. The next build should wait until the relevant code changes are implemented and tested.

## Windows build (development — private source access required)

**Requirements:** Windows 10/11, stable Rust toolchain with Cargo, Visual Studio C++ Build Tools, and the Microsoft Edge WebView2 Runtime.

For an existing local checkout:

```powershell
cd "C:\Users\wwste\Rust-Shield-Browser"
git pull origin main
cargo run --release
```

For a new checkout, clone the **private source repository** using an account with access:

```powershell
git clone https://github.com/Galax71/Rust-Brave-inspired-Browser.git
cd Rust-Brave-inspired-Browser
cargo run --release
```

> [!NOTE]
> These commands are for development and testing, **not** a recommendation to build while the known windowing issues remain. GitHub Actions and local Windows results should be verified before publishing a release.

## Repository and platform overview

| Platform | Location | Renderer / approach | Status |
| --- | --- | --- | --- |
| Windows 10 / 11 | [platforms/windows-10-11](platforms/windows-10-11) | WebView2 | Active prototype |
| Linux | [platforms/linux](platforms/linux) | WebKitGTK | Prototype, untested |
| macOS | [platforms/macos](platforms/macos) | WKWebView | Prototype, untested |
| Android | [platforms/android](platforms/android) | Android System WebView | Planning/documentation |

**Source and releases:** This public repository documents release status and does not include the private source. Development source lives in the private [Rust-Brave-inspired-Browser](https://github.com/Galax71/Rust-Brave-inspired-Browser) repository. The [Rust-Shield-Releases](https://github.com/Galax71/Rust-Shield-Releases) repository is intended for public compiled builds; the presence of that repository does not establish that a verified installer or release is available.

## Architecture at a glance

```text
Rust Shield Browser
├── Rust application (src/main.rs)
│   ├── Window and event handling (winit)
│   ├── Browser commands and tab management
│   └── Settings persistence
├── Toolbar and settings UI (HTML/CSS/JavaScript)
├── Embedded webpage rendering (wry / WebView2 on Windows)
├── Supporting Rust crates (crates/)
└── Platform prototypes and release workflows
```

## Roadmap

- [ ] Fix native-feeling borderless window resizing and Snap Assist behavior
- [ ] Make layout previews float without resizing the webpage
- [ ] Investigate and resolve PrtSc handling while focused
- [ ] Improve tab lifecycle so inactive tabs preserve state reliably
- [ ] Integrate the approved Rust Shield icon into the application and taskbar
- [ ] Add and test privacy protections and content blocking
- [ ] Validate downloads, history, bookmarks, and profiles
- [ ] Create signed, reproducible Windows installers and verify published releases
- [ ] Explore cross-platform engines and a possible Servo integration

Roadmap entries are **plans, not claims of completed functionality**.

## Security and privacy notes

Rust Shield currently relies on the security properties of its embedded web renderer and the surrounding operating system. It has **not** been independently security audited. Do not assume Brave Shields, Tor isolation, hardened sandboxing, ad blocking, extension support, or other protections are present unless implemented and verified.

Only install builds you trust. Leave Microsoft Defender and Windows security features enabled.

## Release availability

**No verified signed installer or production-ready release is claimed here.** Use the [Releases page](https://github.com/Galax71/Rust-Shield-Releases/releases) to see whether a downloadable build has actually been published. Feature statuses reflect the development source at the time of this documentation update and are **not automatically synchronized**.

## Contributing and feedback

The source repository is private, so access is required to view code or submit changes there. Development issues and feature requests can be tracked in the project's GitHub repository when access is available.

For build artifacts, see [BUILD-ARTIFACTS.md](BUILD-ARTIFACTS.md).

---

<div align="center">

**Rust Shield Browser** · Built with Rust · Independent experimental project

</div>
