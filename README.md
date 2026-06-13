# ⚡🗡️ virt-kai-tools  ·  suite v1.3.0

**A curated fleet of Windows repair, diagnostic, and admin utilities.**
Single-file `.exe`s. No install. Zero dependencies. Built by [VVardog] with AI partner **Kai**.

See [`CHANGELOG.md`](CHANGELOG.md) for release history.

> *Teamwork makes the dream work. Only as strong as the weakest link.*

---

## What is this?

31 standalone Windows utilities compiled into individual `.exe` files, plus a
launcher (**Kai-Toolbox**) with two modes:

- 🛡️ **Easy Mode** — big friendly cards with plain-language taglines. Pick the
  problem that sounds like yours.
- ⚔️ **Advanced Mode** — full card grid with search, categories, and staging badges.

Built for computer-lab work, family-PC hand-offs, fresh-install bootstraps, and
network/system triage where you need real tools, fast, without installing a dozen things.

**Download:** [Grab the latest release (zip)](https://github.com/VVardog/virt-kai-tools/releases/latest)
→ extract anywhere → double-click `Kai-Toolbox.exe`. That's it.

---

## 🆕 What's new

### Fix Windows v2.0 — the legendary repair engine

The flagship `fix-windows` tool was rebuilt from the ground up:

- **Convergence-aware multi-pass repair.** Runs DISM `RestoreHealth` + SFC
  `/scannow` in a loop (up to 3 passes by default), and **stops early the moment
  the component store is clean AND SFC reports no integrity violations.** No more
  guessing whether one pass was enough — it verifies and repeats until fixed.
- **Timeout watchdog on every heavy step.** DISM, SFC, and chkdsk each run under
  a watchdog that kills the process tree on overrun and logs a `TIMEOUT` instead
  of hanging forever. **This is the fix for the "it locks up" problem.**
- **In-process live progress.** A single console shows a real `[####------] 45%`
  bar parsed from DISM/SFC output — no more fragile second-window log tails that
  raced and stalled.
- **DISM source fallback.** If `RestoreHealth` can't reach Windows Update
  (the #1 real-world DISM hang), it auto-retries against a local
  `install.wim`/`install.esd` (e.g. a mounted Windows ISO) with `/LimitAccess`.
- **Safer chkdsk pre-flight.** Read-only and time-boxed. It no longer
  auto-schedules a slow boot-time `/F /R` on a bare exit-1 (a healthy NTFS volume
  often returns 1 read-only) — it **suggests** running `check-disk.exe` instead.
- **Richer HTML report** with a per-pass convergence table.

Tune behavior with environment variables before launch:
`FW_MAX_PASSES`, `FW_DISM_TIMEOUT_MIN`, `FW_SFC_TIMEOUT_MIN`, `FW_CHKDSK_TIMEOUT_MIN`.

### Launcher
- 🔓 **Self-unblock on first launch** — strips the Mark-of-the-Web tag from every
  file in its folder, fixing the cryptic *"The operation was canceled by the user"*
  error on freshly-extracted `-requireAdmin` exes. No manual `Unblock-File` steps.
- Unified `logs/` folder, **Debug** button + `debug.bat`, startup auto-dump.
- Clean zip layout: tools live in `staging/<tool>/`, launcher at top level.

---

## The tools

### 🔧 Repair
| Tool | What it does |
|---|---|
| **fix-windows** | Convergence multi-pass DISM/SFC repair + WU/DNS reset, timeout-guarded, HTML report |
| **fix-network** | Winsock/TCP-IP/DHCP/DNS/NetBIOS nuclear reset |
| **fix-audio** | Audio service restart + endpoint re-enumerate |
| **fix-store** | Microsoft Store reset (WSReset + AppX re-register) |
| **check-disk** | Interactive chkdsk front-end (scan / spotfix / full `/F /R` repair) |

### 🩺 Diagnostics
| Tool | What it does |
|---|---|
| **network-diag** | Adapters, DNS, TCP 443 reachability, HTTP timing, 10 MB speed — zero ICMP |
| **bsod-analyzer** | Minidump analyzer |
| **smart-check** | S.M.A.R.T. disk health report |
| **system-info** | Full HTML + JSON system report |
| **gpu-info** | GPU inventory + driver info |
| **quick-benchmark** | 60 s CPU/RAM/disk bench with verdict |

### ⚡ Performance
| Tool | What it does |
|---|---|
| **ultimate-performance** | Unlocks + activates the Ultimate Performance power plan |
| **bloat-remover** | Removes 45+ UWP apps + OneDrive + registry tweaks |
| **startup-manager** | Unified auto-start view + enable/disable |
| **services-panel** | Windows services manager |
| **task-killer** | Find + kill processes locking a file (Restart Manager API) |

### 🌐 Network & Admin
| Tool | What it does |
|---|---|
| **dns-switcher** | Per-adapter DNS swap (Cloudflare/Quad9/Google/AdGuard/OpenDNS) |
| **hosts-editor** | hosts file editor with auto-backup |
| **firewall-manager** | Windows Firewall rules |
| **uac-toggle** | UAC level toggle |
| **backup-wifi** | Export/import saved Wi-Fi profiles |
| **driver-backup** | Export all 3rd-party drivers with restore README |
| **restore-point** | System Restore: enable/create/list/rollback |

### 🚀 Setup & Bootstrap
| Tool | What it does |
|---|---|
| **enable-hyperv / enable-gpedit / enable-sandbox / enable-wsl2** | Unlock Windows features (Home edition too) |
| **install-essentials** | Curated winget installer (VS Code, gh, 7-Zip, …) |
| **update-all** | winget + Store + Windows Update one-click |
| **clean-install** | PC hand-off prep (wipes traces, keeps files) |

### 🧭 Launcher
| Tool | What it does |
|---|---|
| **Kai-Toolbox** | WPF launcher. Auto-discovers the other 30 tools. Easy/Advanced modes, search, categories. Start here. |

---

## Requirements
- Windows 10 or 11 (Home / Pro / Enterprise — all work), 64-bit
- Local admin account (every tool uses `-requireAdmin`)
- ~50 MB free disk for auto-generated reports (saved next to the exe under `logs/`)

## Not code-signed?
Correct — commercial certs cost hundreds/yr. So:
- **SmartScreen:** "Windows protected your PC" → *More info* → *Run anyway*.
- **UAC:** click *Yes* on the elevation prompt.
- **Antivirus:** some AVs flag ps2exe binaries by reflex (PowerShell-in-exe
  heuristic). False positives — whitelist the folder if needed.

## Tips
- **Pin it:** right-click `Kai-Toolbox.exe` → Pin to taskbar.
- **Portable:** the whole folder runs from a USB stick. Nothing installed, no registry writes.
- **Before bulk changes:** run `restore-point.exe` → *Create Now* before
  `bloat-remover` or service tweaks. Rollback is one click away.
- **Fix Windows keeps failing on RestoreHealth?** Mount a matching Windows ISO —
  v2.0 auto-detects `D:\sources\install.wim` and repairs offline.

---

## Building from source
```powershell
# From an elevated PowerShell, in the repo root:
.\Build-Exe.ps1
```
`Build-Exe.ps1` installs the pinned `ps2exe` version, **parse-checks every
source first** (catches syntax errors before compile), then builds each `.exe`
with the crossed-swords icon and `-requireAdmin` manifest.

## Credits
- Built by: **[VVardog]** · AI partner: **Kai**
- Compiler: [ps2exe](https://github.com/MScholtes/PS2EXE) v1.0.13 · UI: WPF · Icon: ⚔️

## License
MIT — use it, fork it, ship it. If it eats your registry, you still can't sue me.

⚡🗡️ *Teamwork makes the dream work. Only as strong as the weakest link.*
