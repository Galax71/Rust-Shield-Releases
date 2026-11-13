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
| Address/search and navigation controls | 🟢 **Working** | User confirmed toolbar buttons work again after the JavaScript syntax fix; broader regression testing remains |
| Tab creation, switching, closing | 🟡 **Needs testing** | Inactive WebViews now remain alive; Windows session and memory testing required |
| Browser-inspired toolbar themes | 🟡 **Needs testing** | Light/Dark styling and preset selection implemented; full native layouts are not available |
| Settings and persistence | 🟡 **Needs testing** | Light/Dark, layout, home button and Settings navigation have updated code; full Windows end-to-end validation remains |
| Two-way and four-way Snap Layout previews | 🟡 **Needs testing** | Preview UI implemented; native Windows integration absent |
| Print Screen / Snipping Tool while focused | 🔴 **Not functional** | Reported to fail when Rust Shield has focus |
| Resize borderless window from edges/corners | 🟡 **Reported functional — needs testing** | Resizing reported functional; confirm edge and corner dragging across window states |
| Floating Snap Layout popup | 🟡 **Needs more testing — functional** | Popup is reported functional; verify that it floats without expanding the toolbar or shifting the webpage |
| Windows native multi-app Snap Assist | ⚪ **Not implemented** | Custom positioning is not the Windows Snap Assist picker |
| Preserve inactive tab state | 🟡 **Needs testing** | Code now hides inactive WebViews instead of destroying them; not yet Windows-tested |
| Approved taskbar/application icon | 🟡 **Needs testing** | Supplied shield emblem committed; Windows build script embeds the icon, but the built EXE/taskbar icon are not yet verified |
| Built-in content/ad blocking and privacy shields | ⚪ **Not implemented** | No verified blocking engine |
| Tor browsing and isolated tab processes | ⚪ **Not implemented** | Not available in prototype |
| Extension compatibility | ⚪ **Not implemented** | No extension subsystem |
| Windows installer and portable EXE | 🟡 **Needs testing** | Build and local release scripts exist; installed behavior and publishing require verification |
| Digitally signed release | ⚪ **Not implemented** | No verified code-signing process |
| Servo as primary rendering engine | ⚪ **Not implemented** | WebView2 remains the current Windows renderer |
| Linux/macOS functional builds | 🟡 **Needs testing** | Platform scaffolding exists; successful native builds not confirmed |
| Android browser application | 🟡 **Needs testing** | Basic Java/Android WebView test app and local APK build script added; successful build and device testing not yet confirmed |

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

**Important limitation:** The current source attempts to preserve inactive WebViews rather than destroy them; behavior still requires Windows testing. Unsaved forms, page state, and media playback may be lost. Do not rely on this prototype for sensitive or important browsing.

## Known issues and work in progress

- **Print Screen:** Windows' PrtSc/Snipping Tool shortcut may not activate while Rust Shield has focus.
- **Window resizing:** Edge/corner resizing has been reported functional; verify all edges, corners, and maximized/restored states.
- **Snap preview:** Floating Snap Layout popup is reported functional, but further testing is needed to confirm it does not expand the toolbar or shift the webpage.
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

## Download Rust Shield

**Windows executable downloads and versioned application builds will be distributed through the public [Rust Shield Releases page](https://github.com/Galax71/Rust-Shield-Releases/releases).** Each published version will have its own GitHub Release with **two Windows download choices**: an installer (`RustShield-Setup-VERSION-windows-x64.exe`) that installs the app with Start Menu shortcuts and uninstall support, and a portable executable (`RustShield-Portable-VERSION-windows-x64.exe`) that runs directly without an installer. Older published versions will remain accessible from the releases history unless explicitly withdrawn.

**Publication is intentionally manual:** the private source repository's Windows release workflow builds both files and publishes them to the public releases repository only when explicitly dispatched with publishing enabled. It requires a repository secret with public-repository Contents write permission. The workflow and generated binaries still require testing before any release is considered verified.\n\n**Do not use source-code ZIP archives as Windows executables.** Download the attached `.exe` or installer asset for the version you want. No build should be advertised as verified or production-ready before it has been tested.

## Repository and platform overview

| Platform | Location | Renderer / approach | Status |
| --- | --- | --- | --- |
| Windows 10 / 11 | [platforms/windows-10-11](platforms/windows-10-11) | WebView2 | Active prototype |
| Linux | [platforms/linux](platforms/linux) | WebKitGTK | Prototype, untested |
| macOS | [platforms/macos](platforms/macos) | WKWebView | Prototype, untested |
| Android | [platforms/android](platforms/android) | Android System WebView | Basic test prototype in private source; APK build unverified |

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

**Versioned executable downloads belong on this repository's GitHub Releases page. No verified signed installer or production-ready release is claimed here.** Use the [Releases page](https://github.com/Galax71/Rust-Shield-Releases/releases) to see whether a downloadable build has actually been published. Feature statuses reflect the development source at the time of this documentation update and are **not automatically synchronized**.

## Bug reports and feature requests

**[🐛 Report a bug](https://github.com/Galax71/Rust-Shield-Releases/issues/new/choose) · [📋 View reported issues](https://github.com/Galax71/Rust-Shield-Releases/issues) · [💡 Suggest a feature](https://github.com/Galax71/Rust-Shield-Releases/issues/new/choose)**

Use the public **Rust Shield Releases** issue tracker for Windows, Linux, macOS and Android feedback. Choose **Bug report** or **Feature request** to open the appropriate form.

| Operating system | Report options | Additional information |
| --- | --- | --- |
| 🪟 **Windows** | Windows 11, Windows 10, other Windows | Version/build number |
| 🐧 **Linux** | Ubuntu, Debian, Fedora, Arch, other distributions | Distribution release and desktop environment |
| 🍎 **macOS** | macOS | macOS version and device architecture |
| 🤖 **Android** | Android | Android version and device model |
| 🌐 **Multiple / Other** | Multiple platforms or other OS | Explain which systems are affected |

For bug reports, include the **Rust Shield version**, steps to reproduce, expected versus actual behavior, and any error messages or screenshots. **Remove passwords, tokens, personal data and private browsing details before posting.** Linux and macOS support remains experimental; choosing an OS does not imply a working build is available.

Source-code contributors with repository access can also use the [private developer issue tracker](https://github.com/Galax71/Rust-Brave-inspired-Browser/issues).

## Contributing and feedback

The source repository is private, so access is required to view code or submit changes there. Development issues and feature requests can be tracked in the project's GitHub repository when access is available.

For build artifacts, see [BUILD-ARTIFACTS.md](BUILD-ARTIFACTS.md).

---

<div align="center">

**Rust Shield Browser** · Built with Rust · Independent experimental project

</div>
