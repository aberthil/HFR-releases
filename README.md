# HFR — High Frame-Rate Interpolation

Windows app for **GPU frame-rate interpolation**: scene detect → interpolate → encode.

Pick the engine that fits the job:

- **RIFE** (default) — Practical-RIFE via TensorRT — fastest path for most titles
- **FILM** — Google FILM via TensorRT — often smoother on hard motion
- **GIMM** — GIMM-VFI (compile backend) — alternate VFI when you want that look

Native PySide6 GUI · NVIDIA GPU required · one Setup.exe with App Update built in.

---

## Download

| | |
|--|--|
| **Latest Setup** | [HFR-1.0.22-Setup.exe](https://github.com/aberthil/HFR-releases/releases/latest/download/HFR-1.0.22-Setup.exe) |
| **All versions** | [Releases](https://github.com/aberthil/HFR-releases/releases) |
| **SHA-256** | [HFR-1.0.22-Setup.exe.sha256](https://github.com/aberthil/HFR-releases/releases/latest/download/HFR-1.0.22-Setup.exe.sha256) |

> Prefer the **latest** tag always:  
> https://github.com/aberthil/HFR-releases/releases/latest

Install to `C:\DolbyVisionScripts\HFR` by default. Settings / Pushover / queue live in AppData and survive Update; Remove wipes them.

---

## What it does

1. **Scene detect** — TransNetV2 (default) or AutoShot  
2. **Interpolate** — RIFE / FILM / GIMM to your target fps  
3. **Encode** — NVEncC HEVC (GPU), defaults tuned for archival delivery  

Queue files, tune per job, run batch. Tool updates and App update are both in Settings (Tool updates ≠ App update).

---

## Requirements

| | |
|--|--|
| OS | Windows 10/11 **x64** |
| GPU | **NVIDIA** (CUDA) — RTX recommended |
| Disk | Setup ~250 MB + first-run CUDA `.venv` (network; can take several minutes) |
| After install | Finish Launch waits until `create_venv` succeeds (`venv_cuda_ok.txt`) |

---

## Install

1. Download **HFR-*-Setup.exe** from [Releases](https://github.com/aberthil/HFR-releases/releases/latest)  
2. Run Setup (admin)  
3. Wait for the hidden venv step (progress in the wizard + `install_venv.log`)  
4. Launch **HFR** from the Finish page / Start Menu  

**Repair venv later:** run `create_venv.cmd` in the install folder (visible console).

**Update the app:** Settings → App update → Check → Update & Install  
(keeps AppData userdata; does not replace Tool updates)

---

## Engines (defaults)

| Engine | Backend | Notes |
|--------|---------|--------|
| **RIFE** | TensorRT | Default — best throughput here |
| **FILM** | TensorRT | Slower; strong on difficult motion |
| **GIMM** | `torch.compile` | Needs MSVC + triton-windows for compile path |

Scene detector default: **TransNetV2** @ thr **0.4**. Encode default: **NVEncC** · preset **P7** · bitrate **same as source**.

---

## What's New

### v1.0.22

Preserve user settings on update: RestoreCredentialsAfterWipe + ForceDirectories; cover `gui_config` / `pushover` / `queue`.

See full history on the [Releases](https://github.com/aberthil/HFR-releases/releases) page.

---

## Project layout (installed)

```
C:\DolbyVisionScripts\HFR\
  HFR.exe              # GUI
  Python312\           # bootstrap interpreter for create_venv
  binaries\            # ffmpeg / NVEncC / tools
  create_venv.py|.cmd  # first-run / repair CUDA env
  app_version.json     # App update metadata
```

User data (not wiped on Update):

`%LOCALAPPDATA%\DolbyVisionScripts\` — `gui_config.json`, `pushover.json`, `queue.json` (and installer Backup/Restore for the same names under `{app}` legacy paths).

---

## Links

- **Latest download:** https://github.com/aberthil/HFR-releases/releases/latest  
- **This repo:** public Setup hosting + project page (source stays private)

---

## License / support

Windows installers published here for end users. Issues with a specific Setup build: open a discussion on the release that fails, or contact the publisher (`aberthil`).
