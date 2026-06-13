# Changelog

All notable changes to **virt-kai-tools** are recorded here.
Format loosely follows [Keep a Changelog](https://keepachangelog.com/).
The suite version is the umbrella release number; individual tools carry their
own internal versions (shown in parentheses).

---

## [1.3.0] — 2026-06-13 — "Legendary Repair"

### Changed — Fix Windows (2.0.0) — full rewrite of the repair engine
- **Convergence-aware multi-pass repair.** DISM `RestoreHealth` + SFC `/scannow`
  now run in a loop (up to `FW_MAX_PASSES`, default 3) and **stop early the moment
  the component store is clean AND SFC reports no integrity violations.** Replaces
  the previous single-pass behavior; verifies the fix instead of guessing.
- **Timeout watchdog on every heavy step** (`Invoke-Watched`). DISM, SFC, and
  chkdsk run under a watchdog that kills the process tree on overrun (logged as
  exit `1460`). **Root-cause fix for the lock-ups.**
- **In-process live progress bar** parsed from DISM/SFC stdout. Removed the
  fragile second-window `Get-Content -Wait` log tails that raced and stalled.
- **DISM source fallback.** If `RestoreHealth` can't reach Windows Update, it
  auto-retries against a local `install.wim`/`install.esd` with `/LimitAccess`
  (offline repair from a mounted Windows ISO).
- **Per-pass convergence table** added to the HTML report.

### Fixed
- **chkdsk pre-flight freeze.** It is now read-only and time-boxed, and **no
  longer auto-schedules a boot-time `/F /R`** on a bare exit-1 (which healthy NTFS
  volumes return routinely under read-only chkdsk). It suggests running
  `check-disk.exe` (Full repair) instead.

### Tunables (new)
`FW_MAX_PASSES`, `FW_DISM_TIMEOUT_MIN`, `FW_SFC_TIMEOUT_MIN`, `FW_CHKDSK_TIMEOUT_MIN`
— set as environment variables before launch.

### Changed — Kai-Toolbox (1.6.0)
- Ships Fix Windows v2.0; refreshed the Repair card copy to describe the new
  multi-pass + watchdog behavior.
- Unified internal version strings (debug dump + UI tag were stale at 1.5.3/1.5.1).

### Docs
- Real `README.md` in the source repo covering the full 31-tool suite and v2.0.
- Public landing README (`virt-kai-tools`) synced to v2.0.
- Added this `CHANGELOG.md`.

---

## [1.2.4] — 2026-04-18 — "Self-Unblock"
- Kai-Toolbox strips Mark-of-the-Web from sibling files on first launch, fixing
  the cryptic *"The operation was canceled by the user"* error on `-requireAdmin`
  exes freshly extracted from a Releases zip.

## [1.2.3] — Logs & Debug
- Unified `logs/` folder, **Debug** button + `debug.bat`, startup auto-dump.

## [1.2.2] — Cleaner zip layout
- Tools live under `staging/<tool>/`; top level holds only the launcher.

## [1.2.1] — Portable discovery
- Launcher finds tools next to the exe.

## [1.2.0] — Easy + Advanced
- Easy Mode + Advanced Mode toggle, Full Health Check combo tool,
  restore-point safety net.

---

### Earlier history
The suite grew from a handful of repair scripts to 31 tools across 2026-04 →
2026-05 (see `git log` for the full per-tool trail): network-diag, bsod-analyzer,
firewall-manager, services-panel, uac-toggle, gpu-info, smart-check, and the
power-user batch (bloat-remover, startup-manager, task-killer, dns-switcher,
hosts-editor, backup-wifi, driver-backup, restore-point, enable-* feature
unlocks, install-essentials, update-all, clean-install).

[1.3.0]: https://github.com/VVardog/virt-kai-tools/releases/tag/v1.3.0
[1.2.4]: https://github.com/VVardog/virt-kai-tools/releases
