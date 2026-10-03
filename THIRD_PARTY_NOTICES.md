# Third-party software in GPU Farm Monitor

GPU Farm Monitor (GFM) 0.1.0 beta, by crazykkid2000productions, is built with — and works alongside — the
open-source and third-party software listed here. Thank you to every one of these projects and their authors.

- Each component stays under **its own licence**. GFM's own licence (`LICENSE.txt`) covers GFM only; it never
  limits the rights these licences give you.
- The **full licence texts** ship with the app in the `licenses` folder of the install folder (and of the desktop
  client). `licenses\INDEX.md` lists every text and the component it belongs to.
- Questions about any of this: crazykkid2000productions@gmail.com

Contents:
1. Inside the Windows app and the desktop client
2. Streaming programs bundled with GFM (Sunshine, Moonlight)
3. GFM Stream for Android (GPL-3.0, source included)
4. The GFM Android app
5. Downloaded only when you ask for it (not shipped by GFM)
6. AI models
7. Data: the PCI ID list

---

## 1. Inside the Windows app and the desktop client

GFM is a Python application packaged with PyInstaller. Its installer contains a private Python runtime and the
libraries below, at exactly these versions (0.1.0 beta build). The desktop client contains the same set **except**
Paramiko, bcrypt, PyNaCl and invoke (the client never opens SSH connections itself).

### Runtime

| Component | Version | Licence | What it does in GFM |
|---|---|---|---|
| Python runtime and standard library | 3.12.10 | PSF License 2.0 | Runs GFM. Python's Windows build also contains OpenSSL 3 (Apache-2.0), libffi (MIT), zlib (zlib), bzip2 (bzip2 licence), liblzma (public domain), Expat (MIT), libmpdec (BSD-2-Clause) and Tcl/Tk 8.6 (Tcl/Tk licence, BSD-style). Texts: `licenses\python\LICENSE.txt` (Python, libffi, bzip2, Tcl/Tk) and `licenses\python\bundled-libraries.txt` (the others). |
| Tcl/Tk | 8.6 | Tcl/Tk licence (BSD-style) | The window toolkit behind GFM's desktop interface (licence text also in `_internal\_tk_data\license.terms`). |
| Microsoft Visual C++ runtime (`VCRUNTIME140.dll`, `VCRUNTIME140_1.dll`) | 14 | Microsoft redistributable licence terms | C runtime used by Python; redistributable files. |
| PyInstaller bootloader | 6.16.0 | GPL-2.0 with the PyInstaller bootloader exception | Starts `GPU Farm Monitor.exe`. The exception allows it in programs under any licence. |

### Python libraries

| Library | Version | Licence | What it does in GFM |
|---|---|---|---|
| Paramiko | 4.0.0 | LGPL-2.1 | SSH connections to your rigs (app only). |
| bcrypt | 5.0.0 | Apache-2.0 | Key handling for Paramiko (app only). |
| PyNaCl | 1.6.2 | Apache-2.0 (includes libsodium, ISC) | Ed25519 SSH keys for Paramiko (app only). |
| invoke | 3.0.3 | BSD-2-Clause | Helper library of Paramiko (app only). |
| cryptography | 46.0.7 | Apache-2.0 OR BSD-3-Clause (includes OpenSSL, Apache-2.0) | TLS, AES-256 encryption of saved sign-ins, SSH crypto. |
| cffi / pycparser | 2.1.1 / 3.0 | MIT-0 / BSD-3-Clause | Native code bridge used by cryptography and bcrypt. |
| keyring | 25.7.0 | MIT | Stores passwords, keys and tokens in Windows Credential Manager. |
| jaraco.classes, jaraco.context, jaraco.functools | 3.4.0, 6.1.2, 4.6.0 | MIT | Helper libraries of keyring. |
| more-itertools | 11.1.0 | MIT | Helper library of keyring. |
| pywin32-ctypes | 0.2.3 | BSD-3-Clause | Windows Credential Manager access for keyring. |
| Pillow | 12.3.0 | MIT-CMU (HPND) | Pictures: icons, chat images, generated images. |
| pystray | 0.19.5 | LGPL-3.0 | The system-tray icon. |
| pypdf | 6.19.0 | BSD-3-Clause | Reads PDF attachments in GFM Chat. |
| jsonschema, jsonschema-specifications, referencing, rpds-py, attrs | 4.26.0, 2025.9.1, 0.37.0, 2026.6.3, 26.1.0 | MIT | Checks tool definitions (OpenAPI / JSON Schema) in GFM Chat. |
| truststore | 0.10.4 | MIT | Uses Windows' own certificate store for HTTPS downloads. |
| miniaudio | 1.71 | MIT (its C decoders are public domain / MIT-0) | Plays generated songs inside GFM Chat. By Irmen de Jong, wrapping David Reid's miniaudio and the dr_flac / dr_mp3 / dr_wav / stb_vorbis decoders. |
| ModernGL / glcontext | 5.12.0 / 3.0.0 | MIT | Optional GPU renderer of the Neon Fusion themes. |
| packaging | 26.3 | Apache-2.0 OR BSD-2-Clause | Version comparisons. |
| six, typing_extensions | 1.17.0, 4.16.0 | MIT, PSF-2.0 | Compatibility helpers used by the libraries above. |
| setuptools (import helper only) | 84.0.0 | MIT | Pulled in by PyInstaller's import system. |

**LGPL libraries (Paramiko, pystray).** These two ship unmodified as plain Python source files in
`_internal\paramiko` and `_internal\pystray` inside the install folder — not packed into the EXE — so you can
replace them with your own modified versions. Their complete source is the files themselves; the upstream projects
are at https://github.com/paramiko/paramiko and https://github.com/moses-palmer/pystray. GFM's licence agreement
(`LICENSE.txt`, section 3) allows the modification and reverse engineering the LGPL permits for this purpose.

### Web dashboard (served by GFM's optional server)

| Component | Version | Licence | What it does in GFM |
|---|---|---|---|
| xterm.js and its fit add-on | 5.x | MIT | The SSH terminal in the web dashboard. Copyright the xterm.js authors, SourceLair Private Company and Christopher Jeffrey (`licenses\xterm.js\`). |

---

## 2. Streaming programs bundled with GFM

GFM ships these programs **unmodified**, exactly as their projects publish them (each file is checked against a
pinned SHA-256 before it is bundled), so GFM can set up streaming without an internet connection. They run as
separate programs; GFM installs Sunshine on your rigs and runs Moonlight on your PC.

| Program | Version and files | Licence | What it does in GFM | Complete source code |
|---|---|---|---|---|
| **Sunshine** (LizardByte) | Windows rigs: 2026.914.233613 (`Sunshine-Windows-AMD64-installer.msi`). Linux rigs: 2025.924.154138 (`sunshine-ubuntu-22.04-amd64.deb`, `sunshine-ubuntu-24.04-amd64.deb`, `sunshine-debian-trixie-amd64.deb`) | GPL-3.0-only | The streaming server GFM installs on a rig for **STREAM DESKTOP**. | `Sunshine-2026.914.233613-complete-source.tar.xz` and `Sunshine-2025.924.154138-complete-source.tar.xz`, published on GFM's release page next to the installers (each tag with all of Sunshine's git submodules). Upstream: https://github.com/LizardByte/Sunshine (`git clone --recursive --branch <tag> https://github.com/LizardByte/Sunshine.git`). |
| **Moonlight** (moonlight-qt) | 6.1.0 (`MoonlightPortable-x64-6.1.0.zip`, `Moonlight-6.1.0-x86_64.AppImage`) | GPL-3.0-or-later | Shows a rig's desktop in GFM's stream window ("Powered by Moonlight"). | `MoonlightSrc-6.1.0.tar.gz` (Moonlight's own complete source archive), published on GFM's release page and on https://github.com/moonlight-stream/moonlight-qt/releases/tag/v6.1.0 — https://moonlight-stream.org |

Both packages include further libraries under their own licences (for example Qt and FFmpeg under the LGPL, SDL
under zlib, OpenSSL under Apache-2.0, Opus under BSD-3-Clause, Boost under the Boost licence); their notices are
inside each package and its source archive. The GPL-3.0 text is in `licenses\GPL-3.0.txt`.

**Source on request.** For three years from the date we distribute this version, anyone may ask
crazykkid2000productions@gmail.com for the complete corresponding source code of Sunshine and Moonlight at the
versions above, and of GFM Stream (section 3); we will send it for no more than the cost of providing it.

### Parsec Virtual Display Driver (not bundled)

| Component | Version | Licence | What it does in GFM |
|---|---|---|---|
| Parsec Virtual Display Driver | 0.41.0.0 | Proprietary, © Parsec Cloud, Inc. | A virtual monitor on Windows rigs that have no screen attached, switched on only while you stream. **Not redistributed:** when you choose it, GFM downloads Parsec's own signed installer from `builds.parsec.app` and checks its SHA-256 and Parsec's signature. https://parsec.app |

---

## 3. GFM Stream for Android (GPL-3.0, source included)

**GFM Stream** is GFM's companion streaming app for Android: tap **▶ STREAM DESKTOP** on a rig in the GFM Android
app and GFM Stream opens that rig's desktop, pairing itself the first time. It is a **modified version of Moonlight
for Android** (https://github.com/moonlight-stream/moonlight-android, release v12.2, commit `b48494cb`), made by
crazykkid2000productions in October 2026, and it is licensed under the **GNU General Public License v3.0** — the
same licence as Moonlight. GFM's own licence agreement (`LICENSE.txt`) does **not** apply to GFM Stream.

- Version: 12.2-gfm2 (app ID `com.crazykkid2000.gfmstream`; it installs next to the official Moonlight).
- What changed from Moonlight: a one-tap launch screen that GFM starts with the rig's address and a pairing PIN, its
  own app ID and name, a 60-second pairing time-out with a plain-English message, and release signing with GFM's key.
  Every change is listed in `GFM-CHANGES.md` inside the source archive.
- **Complete source code:** `GFM-Stream-12.2-gfm2-source.zip`, published right next to the APK — on the release
  page and on your own GFM's download page. It contains everything needed to build the APK, including the
  moonlight-common-c submodule.
- You may copy, change and share GFM Stream under the terms of the GPL-3.0 (`licenses\GPL-3.0.txt`).

Libraries inside GFM Stream:

| Library | Version | Licence |
|---|---|---|
| Moonlight for Android / moonlight-common-c (Moonlight Game Streaming Project) | 12.2 | GPL-3.0 |
| ENet (Lee Salzman), as modified by the Moonlight project | — | MIT |
| nanors (Joseph Calderon) | — | MIT |
| OpenSSL | 4.0.2 | Apache-2.0 |
| Opus audio codec | — | BSD-3-Clause |
| Bouncy Castle (bcprov / bcpkix) | 1.85 | Bouncy Castle licence (MIT-style) |
| OkHttp | 5.5.0 | Apache-2.0 |
| JmDNS | 3.6.3 | Apache-2.0 |
| JCodec | 0.2.5 | BSD-2-Clause |
| ShieldControllerExtensions (Cameron Gutman) | 1.0.1 | MIT |

---

## 4. The GFM Android app

The GFM Android app (`GPU-Farm-Monitor-Client-0.1.0-beta-Android.apk`) is GFM's own code under GFM's licence. It
uses only the Android platform itself and contains no third-party libraries. It opens GFM Stream (or, if GFM Stream
is not installed, the official Moonlight app) as a separate app.

---

## 5. Downloaded only when you ask for it (not shipped by GFM)

GFM downloads these from their official sources when you choose the feature — usually onto a rig, sometimes onto
your GFM PC — and checks them where the publisher provides checksums or signatures. They are never part of GFM's
installer. When a download comes with terms you must accept, GFM shows them to you first.

**Rig management and monitoring**

| Component | Used for | Licence |
|---|---|---|
| GPU drivers (NVIDIA, AMD, Intel) | INSTALL / UPDATE DRIVERS on rigs | The vendor's licence |
| LACT (Ilya Zlobintsev) | Linux fan curves, clocks and power limits | MIT |
| LibreHardwareMonitor 0.9.6 | Extra sensor readings on Windows rigs (INSTALL WINDOWS SENSORS) | MPL-2.0 |
| PawnIO 2.2.0 (namazso) | The signed driver LibreHardwareMonitor uses on Windows rigs | GPL-2.0-or-later, with exceptions (see its project page) |
| OpenSSH for Windows (Microsoft, Win32-OpenSSH) | Fallback of GFM's SSH installer when Windows cannot add its own OpenSSH Server; Microsoft-signed MSI checked by SHA-256 | OpenSSH licence (BSD-style) |
| Microsoft Visual C++ Redistributable | Needed by llama.cpp and the AI services on Windows rigs; Microsoft's signature is checked | Microsoft software licence terms |

**AI services on your rigs**

| Component | Used for | Licence |
|---|---|---|
| llama.cpp (ggml-org) | Running AI models (built for CUDA / Vulkan / CPU, or official Windows builds) | MIT |
| ComfyUI | Image, image-edit, music and 3D generation | GPL-3.0 |
| SearXNG | Web search for GFM Chat | AGPL-3.0 |
| Docling | Document conversion support model | MIT |
| PyTorch | Runtime for ComfyUI and the generation services | BSD-3-Clause |
| Hugging Face diffusers | Picture generation service | Apache-2.0 |
| Hunyuan3D-2 (Tencent) | 3D generation service | Tencent Hunyuan Community License (not licensed for use in the EU, the UK or South Korea) |
| uv (Astral) | Python environments for the services | MIT OR Apache-2.0 |

**Build machines (APP BUILDER → VERSIONS → BUILD EXE / APPIMAGE / APK)**

| Component | Licence |
|---|---|
| Node.js 20.18.0 | MIT |
| git (MinGit 2.46.0 from Git for Windows on Windows; the distribution's git package on Linux) | GPL-2.0 |
| Eclipse Temurin JDK 17 (Adoptium) | GPL-2.0 with the Classpath Exception |
| Android SDK (platform 34, build-tools 34, command-line tools) | Android Software Development Kit License Agreement — GFM installs it only after you accept it yourself |
| .NET 8 SDK (Microsoft) | MIT |
| uv and PyInstaller | uv: MIT OR Apache-2.0; PyInstaller: GPL-2.0 with the bootloader exception |
| binutils (objdump, for PyInstaller on Linux) | GPL-3.0 |
| appimagetool (AppImage project) | MIT |

Godot and Unity are not downloaded by GFM: you install them yourself under their own terms.

---

## 6. AI models

AI models are not part of GFM. When you download a model through GFM (Hugging Face browser, MODEL CACHE, DEPLOY
SERVICES, INSTALL COMFYUI TEMPLATE), it comes under the licence its maker chose, and **you are responsible for
following it** — some models do not allow commercial use or use in certain countries. GFM shows the licence of
each ComfyUI template before it downloads anything. The templates GFM offers:

| Tool | Template | Model licence |
|---|---|---|
| Image | SDXL Turbo | Stability AI Community License |
| Image | Z-Image-Turbo Int8 | Apache 2.0 |
| Image | Flux.2 Klein 4B | Apache 2.0 |
| Image | Flux.1 Schnell FP8 | Apache 2.0 |
| Image | Qwen-Image | Apache 2.0 |
| Image edit | Flux.2 Klein 4B Image Edit | Apache 2.0 |
| Image edit | OmniGen2 Image Edit | Apache 2.0 |
| Image edit | Flux Kontext Dev Image Edit | FLUX.1 [dev] Non-Commercial License |
| Image edit | Qwen-Image-Edit | Apache 2.0 |
| Music | ACE-Step 1.5 | ACE-Step licence |
| Music | Stable Audio Open 1.0 (short clips) | Stability AI Community License |
| Music | ACE-Step 1.5 with 4B LLM | ACE-Step licence |
| Music | MiniMax Music 3 | MiniMax model licence |
| Music | ACE-Step 1.5 XL Turbo | ACE-Step licence |
| 3D | Hunyuan3D 2.0 | Tencent Hunyuan Community License (not EU, UK, South Korea) |
| 3D | Hunyuan3D 2.1 | Tencent Hunyuan Community License (not EU, UK, South Korea) |
| 3D | Pixal3D + TRELLIS.2 | TRELLIS.2 MIT + Pixal3D licence |

GFM's small support models (for example Qwen3 1.7B / 4B in GGUF form) are downloaded from Hugging Face under
their makers' licences (Qwen3: Apache-2.0).

---

## 7. Data: the PCI ID list

When a GPU has no driver yet, Windows only calls it "Microsoft Basic Display Adapter". GFM then looks up its PCI
device ID in the public PCI ID list by **The PCI ID Repository** (https://pci-ids.ucw.cz), used under the
**BSD 3-Clause License** (the list is dual-licensed BSD-3-Clause / GPL-2.0-or-later). The GFM PC downloads the
list when a card needs it and keeps the NVIDIA, AMD and Intel display entries in GFM's data folder (refreshed
monthly). GFM does not ship or change the list.
