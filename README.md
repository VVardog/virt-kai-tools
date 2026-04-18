# ⚡🗡️ Kai Toolbox

**A curated fleet of Windows repair, diagnostic, and admin utilities. Single-file exes. No install. Zero dependencies.**

[![Latest Release](https://img.shields.io/github/v/release/VVardog/virt-kai-tools?label=release&color=58d68d)](https://github.com/VVardog/virt-kai-tools/releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-blue)](https://github.com/VVardog/virt-kai-tools/releases/latest)
[![License](https://img.shields.io/badge/license-MIT-lightgrey)](LICENSE)

---

## What is this?

31 standalone Windows utilities compiled into individual `.exe` files, plus a launcher (**Kai-Toolbox**) with **two modes**:

- **🛡️ Easy Mode** — 7 big friendly cards with plain-language taglines. Pick the problem that sounds like yours.
- **⚔️ Advanced Mode** — full card grid with search, categories, and staging badges.

Toggle top-right. The launcher remembers your choice.

Built for computer lab work, family PC hand-offs, fresh-install bootstraps, and the kind of network/system triage where you need real tools, fast, without installing a dozen things.

## ✨ New in v1.2.4

- **🔓 Self-unblock on first launch** — Kai-Toolbox now strips the Mark-of-the-Web tag from every file in its folder the first time it runs. Fixes the cryptic `"The operation was canceled by the user"` error that Windows silently throws on `-requireAdmin` exes freshly extracted from the release zip. **No more manual `Unblock-File` steps** — it just works.

### Previously in v1.2.x
- **v1.2.3** — unified `logs/` folder, Debug button + `debug.bat`, startup auto-dump.
- **v1.2.2** — cleaner zip layout: tools live in `tools/`, top level has only the launcher.
- **v1.2.1** — portable tool discovery (find tools next to the exe).
- **v1.2.0** — Easy Mode + Advanced Mode toggle, Full Health Check combo tool, restore-point safety net.

## Download

👉 **[Grab the latest release (zip)](https://github.com/VVardog/virt-kai-tools/releases/latest)**

Extract anywhere. Double-click `Kai-Toolbox.exe`. That's it.

---

## What's inside

### 🔧 Repair / Diagnostic
| Tool | What it does |
|---|---|
| `fix-windows` | DISM/SFC/WU/DNS 15-step Windows repair, 2 passes, HTML report |
| `fix-network` | Winsock/TCP-IP/DHCP/DNS/NetBIOS nuclear reset |
| `fix-audio` | Audio service restart + endpoint re-enumerate |
| `fix-store` | Microsoft Store reset (WSReset + AppX re-register) |
| `network-diag` | Adapters, DNS, TCP 443 reachability, HTTP timing, 10MB speed — **zero ICMP** |
| `check-disk` | Interactive chkdsk (scan / spotfix / full) |
| `bsod-analyzer` | Minidump analyzer |
| `smart-check` | S.M.A.R.T. disk health report |

### ⚡ Performance / Info
| Tool | What it does |
|---|---|
| `ultimate-performance` | Unlocks + activates the Ultimate Performance power plan |
| `quick-benchmark` | 60s CPU/RAM/disk bench with verdict (EXCELLENT/FAST/AVERAGE/SLOW) |
| `system-info` | Full HTML + JSON system report |
| `gpu-info` | GPU inventory + driver info |

### 🎛️ Manage / Configure
| Tool | What it does |
|---|---|
| `bloat-remover` | Removes 45+ UWP apps + OneDrive + registry tweaks |
| `startup-manager` | Unified auto-start view + enable/disable |
| `services-panel` | Windows services manager |
| `task-killer` | Find + kill processes locking a file (Restart Manager API) |
| `dns-switcher` | Per-adapter DNS swap (Cloudflare/Quad9/Google/AdGuard/OpenDNS) |
| `hosts-editor` | hosts file editor with auto-backup |
| `firewall-manager` | Windows Firewall rules |
| `uac-toggle` | UAC level toggle |
| `backup-wifi` | Export/import saved Wi-Fi profiles (with or without passwords) |
| `driver-backup` | Export all 3rd-party drivers with restore README |
| `restore-point` | System Restore: enable/create/list/rollback |

### 🚀 Setup / Provision
| Tool | What it does |
|---|---|
| `enable-hyperv` | Hyper-V unlock (works on Home edition too) |
| `enable-gpedit` | gpedit.msc unlock for Home edition |
| `enable-sandbox` | Windows Sandbox unlock |
| `enable-wsl2` | Enable WSL2 + install Ubuntu (optional) |
| `install-essentials` | Curated winget installer (VS Code, gh, 7-Zip, etc.) |
| `update-all` | winget + Store + Windows Update one-click |
| `clean-install` | PC hand-off prep (wipes traces, keeps files) |

### 🎯 Launcher
| Tool | What it does |
|---|---|
| **Kai-Toolbox** | WPF launcher. Auto-discovers the other 30 tools. Search, categories, staging pills. **Start here.** |

---

## Requirements

- **Windows 10 or Windows 11** (Home / Pro / Enterprise — all work)
- **Local admin account** (every tool uses `-requireAdmin` in its manifest)
- ~50 MB free disk space (for auto-generated reports)

## First-run warnings

The exes are not code-signed (commercial certs cost hundreds/yr), so:

> **SmartScreen:** "Windows protected your PC" → click **More info → Run anyway**.

> **UAC:** each tool requests admin elevation → click **Yes**.

> **Antivirus:** some AVs flag ps2exe-compiled binaries as suspicious by reflex (PowerShell-in-exe heuristic). These are false positives. Whitelist the folder if needed.

## Where reports go

Any tool that generates a report writes to `%USERPROFILE%\Desktop\kai-reports\`. Safe to delete anytime.

---

## Pro tips

- **Pin it:** right-click `Kai-Toolbox.exe` → Pin to taskbar. One-click access.
- **Portable:** the whole folder runs from a USB stick. Nothing is installed, no registry writes.
- **Before bulk changes:** run `restore-point.exe` → *Create Now* before running `bloat-remover` or tweaking services. Rollback is one click away.
- **For PC hand-offs:** `clean-install.exe` wipes browser history/cache/logs but keeps user files. Great for selling/gifting a PC.

## Troubleshooting

<details>
<summary><strong>A tool's window flashes and closes immediately</strong></summary>
You declined the UAC prompt. Try again and click Yes.
</details>

<details>
<summary><strong>"This app can't run on your PC"</strong></summary>
Make sure you're on 64-bit Windows 10 or newer.
</details>

<details>
<summary><strong>Antivirus quarantined an exe</strong></summary>
Whitelist the kai-toolbox folder or restore from quarantine. These are PowerShell-in-exe false positives.
</details>

<details>
<summary><strong>A tool card in Kai-Toolbox is grayed out / says MISSING</strong></summary>
That tool's exe is missing from the folder. Re-extract the zip.
</details>

<details>
<summary><strong>A tool crashed — how do I report it?</strong></summary>
Most tools write a timestamped crash log to <code>Desktop\kai-reports\</code>. Open an issue with that file attached.
</details>

---

## Why?

 Over the years I've collected a dozen PowerShell one-liners, registry tweaks, DISM incantations, and service-restart dances — the kind of knowledge that lives in your muscle memory and dies with your next OS reinstall. This is all of that, baked into clickable exes, so anyone can use them.

.

## License

MIT — use it, fork it, ship it, whatever. If it eats your registry, you still can't sue me.

## Credits

- **Built by:** [VVardog]
- **AI partner:** Kai 
- **Compiler:** [ps2exe](https://github.com/MScholtes/PS2EXE) v1.0.13
- **UI:** WPF
- **Icon:** crossed swords ⚔️

---

<sub>⚡🗡️ Teamwork makes the dream work. Only as strong as the weakest link.</sub>
