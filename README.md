# PlayStation Pulse PS4 Host

An offline-first PlayStation 4 host collection for supported firmware versions. The project combines firmware-specific exploit pages, GoldHEN payloads, offline caching, and a unified terminal-style interface.

> This project is intended for educational, preservation, and research purposes. Use it at your own risk. It is not affiliated with or endorsed by Sony Interactive Entertainment.

## Highlights

- Unified firmware selector at the project root.
- Dedicated hosts for PS4 firmware 5.05, 6.72, 7.00–8.52, and 9.00–9.60.
- CSSFontFace host for the 6.00–11.02 range.
- CSSFontFace UAF integration with automatic GoldHEN and payload handling on the CSS host.
- CSSFontFace launch controls with Auto Start enabled by default, a visible countdown, and an optional manual start mode.
- Persistent Lapse/NetCtrl chain selection: the selected chain remains active until the user changes it.
- A manual CSSFontFace page reload control that appears after a reported exploit error without adding automatic retry loops.
- GoldHEN v2.4b18.10 and v2.4b18.5 where the selected host provides both versions.
- Offline-first support through the existing AppCache manifests and cache files.
- Common payload tools such as FTP, PS4Debug, App2USB, backup/restore, update controls, and other host-specific utilities.
- A shared terminal, hacker, retro-computing, cyberpunk, and sci-fi UI language across the selector and host pages.
- Responsive layouts for desktop and mobile screens.

## Host matrix

| Directory | Firmware range | Entry page | Main branch | Offline cache |
|---|---|---|---|---|
| `505/` | 5.05 | `505/index.html` | Firmware-specific PS4 host | `cache.manifest` |
| `672/` | 6.72 | `672/index.html` | Firmware-specific PS4 host | `cache.manifest` |
| `700/` | 7.00–8.52 | `700/version-selector.html` | PSFree / Lapse host flow | `PSPulse.cache`, `PSPulse5.cache` |
| `900/` | 9.00–9.60 | `900/version-selector.html` | PSFree / Lapse host flow | `PSPulse.manifest`, `PSPulse5.manifest` |
| `css/` | 6.00–11.02 | `css/version-selector.html` | CSSFontFace UAF host flow | `CSSPulse.manifest`, `CSSPulse5.manifest` |

The root page, `index.html`, is the recommended starting point. It routes the user to the host that matches the console firmware.

## Supported firmware

The project is organized around the following firmware targets:

- **5.05** — legacy firmware host with a broad set of payload utilities.
- **6.72** — dedicated 6.72 host.
- **7.00–8.52** — PSFree/Lapse host flow with firmware selection.
- **9.00–9.60** — PSFree/Lapse host flow with firmware selection.
- **6.00–11.02** — CSSFontFace host flow in `css/`.

The exact exploit result can still depend on the console firmware, browser state, cached assets, and the selected host chain. Always use the page intended for the exact firmware range shown on screen.

## GoldHEN versions

The host pages include the following GoldHEN builds where supported:

- `GoldHEN v2.4b18.10`
- `GoldHEN v2.4b18.5`

Some hosts expose the versions directly on the main page, while the 7.00–8.52, 9.00–9.60, and CSSFontFace flows may expose them through their version-selection or cache pages. Choose one build and wait for the page status to confirm that the exploit chain has completed before launching payloads.

## CSSFontFace launch controls

The CSSFontFace pages in `css/index.html` and `css/index5.html` provide guarded launch controls while keeping the original exploit chain intact:

- **Auto Start: ON** is the default. A five-second countdown is shown before the exploit starts.
- The countdown gives the user time to select `Lapse`, switch Auto Start off, or leave the default flow unchanged.
- **Auto Start: OFF** selects manual mode. Press `START EXPLOIT` when the page is ready.
- The launch is guarded so the exploit is started only once per page load. The chain controls and launch controls are disabled after activation begins.
- `Lapse` is the default chain only when no valid preference has been saved. A selected `Lapse` or `NetCtrl` choice is stored in browser `localStorage` under `exploitChain` and remains selected until the user changes it.
- If the page reports a controlled `css-exploit-error`, a `RELOAD PAGE` button becomes available. Reloading is always manual; there is no automatic retry or reload loop.
- Auto Start preference is stored under `cssAutoStart`, so the user's ON/OFF choice is preserved across page reloads. A reload does not reset the selected exploit chain.

This recovery control is intentionally limited to errors reported by the page. A completely unresponsive PS4 browser tab cannot reliably execute JavaScript to reload itself; close and reopen the browser if the page is fully frozen.

## Payloads

Payload availability depends on the selected firmware host. The collection includes common utilities such as:

- FTP server
- PS4Debug
- App2USB
- Backup and restore tools
- Enable Updates / Disable Updates
- AppCache Install
- History Blocker
- PUP Decrypt
- RIF Renamer
- Kernel Clock on hosts that provide it
- Host-specific PSFree, Lapse, and GoldHEN components

The payload buttons are part of the existing host logic. Their visibility and availability may differ between firmware directories.

## Interface and design

The current interface is intentionally lightweight and functional:

- near-black background with subtle technical grid lines;
- high-contrast terminal typography;
- green status accents with amber and red states;
- bordered panels, command-style labels, and compact payload controls;
- responsive layouts for narrow mobile screens;
- the same visual language on the root selector, version selectors, cache pages, and exploit pages.

The redesign changes presentation only. The exploit scripts, payload hooks, page routes, element IDs, and host-specific functionality remain tied to their original implementations.

## Troubleshooting

### The page keeps loading or the cache is not updated

Clear the site data for the host, close and reopen the PS4 browser, then load the page again. Confirm that the correct cache/manifest file is being served and that the server returns all referenced files.

### The exploit does not complete

Confirm the exact firmware version, use the matching directory, close unrelated browser tabs, and retry from a clean browser state. On the CSSFontFace page, use `RELOAD PAGE` only when the page has reported a controlled exploit error. If Auto Start is not suitable for the current attempt, switch it off and use `START EXPLOIT` manually. Exploit reliability can vary with browser memory, cached state, and console conditions.

### The PS4 browser is fully frozen

JavaScript cannot guarantee recovery after the browser process stops responding. Do not add repeated retries or reload loops; they can increase instability. Close and reopen the PS4 browser, then open the host again. The saved CSSFontFace chain and Auto Start preference should remain available because they are stored locally by the browser.

### A payload does not respond

Wait until the host reports a successful or ready state. Verify that the PS4 and the payload receiver are on the expected network, then retry the payload from the same host page.

## Safety and limitations

- Do not use a host outside the firmware range shown for your console.
- Do not interrupt the console while a payload or system operation is running.
- Do not use exploit pages for PSN access or other online services.
- Keep a safe recovery path for important data before using backup, restore, or system-related payloads.
- No host can guarantee identical results on every console or every browser state.

## Changelog

### Current release

- Added the CSSFontFace host branch for firmware 6.00–11.02.
- Added CSSFontFace version-selection and offline-cache pages.
- Unified the root selector and firmware host pages under the new terminal/cyberpunk visual system.
- Reworked desktop and mobile layouts while preserving host functionality and page-specific text.
- Added clearer status panels, cache progress presentation, payload sections, and responsive controls.
- Aligned the 5.05, 6.72, 7.00–8.52, 9.00–9.60, and CSSFontFace pages with the same visual language.
- Added guarded CSSFontFace Auto Start controls with a five-second countdown and optional manual activation.
- Preserved the selected CSSFontFace exploit chain across reloads and sessions using browser-local preferences.
- Added a manual `RELOAD PAGE` action for reported CSSFontFace exploit errors; automatic retry and reload loops are intentionally not used.
- Refreshed the CSSFontFace AppCache manifest hashes after the launch-control changes.

### Included GoldHEN builds

- GoldHEN v2.4b18.10
- GoldHEN v2.4b18.5

---

**Author:** [BlackArch](https://t.me/sudoBlackArch)
**Telegram:** [PlayStation Pulse](https://t.me/PlayStation_Pulse)

**Important:** For any use of materials and files, links to the Author - [BlackArch](https://t.me/sudoBlackArch) and Telegram - [PlayStation Pulse](https://t.me/PlayStation_Pulse) must remain on all pages.