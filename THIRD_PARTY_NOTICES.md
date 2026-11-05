# Third-party software in GPU Farm Monitor

GPU Farm Monitor (GFM) 0.2.0 beta, by crazykkid2000productions, is built with — and works alongside — the
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
8. Optional Linux vLLM bundle

---

## 1. Inside the Windows app and the desktop client

GFM is a Python application packaged with PyInstaller. Its installer contains a private Python runtime and the
libraries below, at exactly these versions (0.2.0 beta build). The desktop client contains the same set **except**
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
| cffi / pycparser | 2.1.1 / 3.11 | MIT-0 / BSD-3-Clause | Native code bridge used by cryptography and bcrypt. |
| keyring | 25.7.0 | MIT | Stores passwords, keys and tokens in Windows Credential Manager. |
| jaraco.classes, jaraco.context, jaraco.functools | 3.4.0, 6.1.2, 4.6.0 | MIT | Helper libraries of keyring. |
| more-itertools | 11.1.0 | MIT | Helper library of keyring. |
| pywin32-ctypes | 0.2.3 | BSD-3-Clause | Windows Credential Manager access for keyring. |
| Pillow | 12.3.0 | MIT-CMU (HPND) | Pictures: icons, chat images, generated images. |
| tkinterdnd2 (includes TkDnD) | 0.6.x (resolved version in `licenses\INDEX.md`) | MIT; bundled TkDnD: Tcl/Tk licence (BSD-style) | Native file and picture drops into GFM Chat. Sources and terms: [tkinterdnd2](https://github.com/Eliav2/tkinterdnd2/blob/master/LICENSE), [TkDnD](https://github.com/petasis/tkdnd/blob/master/license.terms). |
| pystray | 0.19.5 | LGPL-3.0 | The system-tray icon. |
| pypdf | 6.20.1 | BSD-3-Clause | Reads PDF attachments in GFM Chat. |
| jsonschema, jsonschema-specifications, referencing, rpds-py, attrs | 4.26.0, 2025.9.1, 0.37.0, 2026.9.1, 26.1.0 | MIT | Checks tool definitions (OpenAPI / JSON Schema) in GFM Chat. |
| truststore | 0.10.4 | MIT | Uses Windows' own certificate store for HTTPS downloads. |
| miniaudio | 1.71 | MIT (its C decoders are public domain / MIT-0) | Plays generated songs inside GFM Chat. By Irmen de Jong, wrapping David Reid's miniaudio and the dr_flac / dr_mp3 / dr_wav / stb_vorbis decoders. |
| ModernGL / glcontext | 5.13.0 / 3.1.0 | MIT | Optional GPU renderer of the Neon Fusion themes. |
| pythonnet / clr_loader | 3.2.1 / 0.3.1 | MIT | GFM's own window: reaches Windows Forms and WebView2 from Python (app only). |
| Microsoft WebView2 SDK (Microsoft.Web.WebView2.Core.dll, Microsoft.Web.WebView2.WinForms.dll, WebView2Loader.dll) | taken from pywebview 6.2.1, see `gpufarm\bundled\webview2\SOURCE.txt` | BSD-3-Clause style, Microsoft's text in `gpufarm\bundled\webview2\Microsoft.Web.WebView2.LICENSE.md` | GFM's own window (app only). The WebView2 runtime itself is part of Windows. |
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

### AWAY FROM HOME (Windows app only)

| Component | Version | Licence | What it does in GFM |
|---|---|---|---|
| Tailscale (`tailscale\tailscaled.exe`, `tailscale\tailscale.exe`) | 1.104.1, built by GFM from Tailscale's published source | BSD-3-Clause, with Tailscale's additional patent grant | Reaches the farm from anywhere (AWAY FROM HOME). GFM starts it itself in userspace networking: no network driver, no Windows service, only while AWAY FROM HOME is on. Copyright Tailscale Inc & contributors (`tailscale\TAILSCALE-LICENSE.txt`, `tailscale\TAILSCALE-PATENTS.txt`). |
| Go runtime and standard library, and the Go modules Tailscale is built from (WireGuard-go, gVisor's network stack and others) | Go 1.27.1; module versions as listed | Go: BSD-3-Clause; each module under its own licence, listed with its texts | Built into the two programs above. Every module, its version and its licence texts: `tailscale\licenses\INDEX.md`. |

Tailscale's sign-in and coordination servers are run by Tailscale Inc under their own terms, which you accept with
Tailscale when you sign in on the AWAY FROM HOME page; GFM accepts nothing for you.

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
- **Complete source code:** `GFM-Stream-12.2-gfm2-source.zip` — on the release page, and right next to the APK on
  your own GFM server's Downloads page. It contains everything needed to build the APK, including the
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
| qwen-tts (Qwen team, Alibaba) | The GFM Voice Studio's speech engine (DEPLOY SERVICES -> GFM Voice Studio) | Apache-2.0 |
| faster-whisper (SYSTRAN) and CTranslate2 | The GFM Voice Studio's word check (it listens to every take) | MIT |
| soundfile (libsndfile) | Reading and writing audio in the GFM Voice Studio | BSD-3-Clause (libsndfile: LGPL-2.1) |

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

**The GFM OS image (HYPERVISOR → BUILD GFM OS)**

GFM does not ship the GFM OS image. BUILD GFM OS builds it on a Linux rig you pick, from the Ubuntu archive and the
publishers' own package sources; GFM sends only its own build scripts and settings (and GFM OS's own desktop package, whose lock screen carries
modified Plasma files - see the last row). The image then carries, each under
its own licence:

| Component | Used for | Licence |
|---|---|---|
| Ubuntu 26.04 LTS packages (Canonical and the Ubuntu / Debian maintainers) incl. the Linux kernel | The system itself | Each package's own licence (the kernel: GPL-2.0) |
| QEMU / KVM | Running virtual machines on a VM server | GPL-2.0 (parts LGPL / BSD / MIT) |
| libvirt | Defining and starting virtual machines | LGPL-2.1-or-later |
| OVMF (EDK II) | UEFI firmware for virtual machines | BSD-2-Clause-Patent |
| swtpm | A virtual TPM 2.0 for Windows 11 guests | BSD-3-Clause |
| OpenZFS (Ubuntu's zfsutils-linux) | Storage pools (mirror, stripe, RAIDZ) | CDDL-1.0 |
| mdadm, LVM2 | Non-ZFS drive layouts | GPL-2.0 (LVM2 libraries LGPL-2.1) |
| cifs-utils, nfs-common | Reaching SMB / NFS shares | GPL-2.0 / GPL-2.0 |
| smbclient (Samba; from GFM OS 0.1.3) | CONNECT in ADD A NETWORK PLACE lists a server's shares | GPL-3.0-or-later |
| Tailscale Linux client (from Tailscale's own package repository; installed switched off) | AWAY FROM HOME | BSD-3-Clause |
| NVIDIA driver 580 (Ubuntu's prebuilt kernel modules) | NVIDIA GPUs | NVIDIA's licence |
| LACT (Ilya Zlobintsev) | Fan curves, clocks and power limits | MIT |
| Plasma lock-screen QML from plasma-workspace 6.6 (KDE: Aleix Pol Gonzalez, David Edmundson, Kai Uwe Broulik, Yifan Zhu), modified by GFM; from GFM OS desktop 0.3.29, shipped as source in `mineros/desktop/lockscreen` | The GFM OS lock screen: Plasma's own unlocking with GFM's look | GPL-2.0-or-later (MainBlock.qml: LGPL-2.0-or-later) |
| Poppins Light lettering (Indian Type Foundry) in the GFM OS boot-screen pictures, from GFM OS desktop 0.3.67 - drawn once into the pictures; no font file is shipped | GFM OS's boot screen (GFM OS - Cosmic Startup) | SIL Open Font License 1.1 |


**The GFM Tiny OS image (IMAGE A KEY / BUILD GFM OS → GFM Tiny OS)**

GFM does not ship the GFM Tiny OS image either. It is built the same way, on a Linux rig you pick, from the same Ubuntu
26.04 sources, on the GFM OS files; GFM sends only its own build scripts and settings (from GFM Tiny OS 0.1.4 also
GFM's own Windows programs engine, gfm-winapps). It is the light one: it carries no VM server (no QEMU / KVM
packages, libvirt, OVMF or swtpm) and no SMB / NFS client. It carries, each under its own licence:

| Component | Used for | Licence |
|---|---|---|
| Ubuntu 26.04 LTS packages (Canonical and the Ubuntu / Debian maintainers) incl. the Linux kernel and its firmware | The system itself | Each package's own licence (the kernel: GPL-2.0) |
| OpenZFS (Ubuntu's zfsutils-linux) | Program storage pools (mirror, stripe, RAIDZ) | CDDL-1.0 |
| mdadm | Non-ZFS drive layouts | GPL-2.0 |
| GRUB 2 (Ubuntu's grub-pc / grub-efi binaries) | Starting the installed drive (BIOS and UEFI) | GPL-3.0-or-later |
| Tailscale Linux client (from Tailscale's own package repository; installed switched off) | AWAY FROM HOME | BSD-3-Clause |
| NVIDIA driver 580 (Ubuntu's prebuilt kernel modules) | NVIDIA GPUs | NVIDIA's licence |
| LACT (Ilya Zlobintsev; optional) | Fan curves, clocks and power limits | MIT |
| Wine (Ubuntu's wine, wine64 and wine32; from GFM Tiny OS 0.1.4) | Running Windows programs and their installers (MANAGEMENT -> INSTALL) | LGPL-2.1-or-later |
| winetricks (from GFM Tiny OS 0.1.4) | Windows runtimes a program needs | LGPL-2.1-or-later |
| msitools (from GFM Tiny OS 0.1.4) | Reading MSI installers | GPL-2.0-or-later (libmsi: LGPL-2.1-or-later) |
| icoutils (from GFM Tiny OS 0.1.4) | Program icons from Windows files | GPL-3.0-or-later |
| cabextract (from GFM Tiny OS 0.1.4) | Unpacking Microsoft CAB archives | GPL-3.0-or-later |
| innoextract (from GFM Tiny OS 0.1.4) | Reading Inno Setup installers | zlib |
| unshield (from GFM Tiny OS 0.1.4) | Reading InstallShield cabinets | MIT |
| 7-Zip (Ubuntu's 7zip; from GFM Tiny OS 0.1.4) | Unpacking archives and self-extracting installers | LGPL-2.1-or-later (parts BSD-3-Clause; the unRAR code with the unRAR licence restriction) |
| UnZip (Info-ZIP; Ubuntu's unzip, from GFM Tiny OS 0.1.14) | Unpacking ZIP archives - what winetricks unpacks runtimes such as OpenAL with | Info-ZIP licence (BSD-style) |
| Xvfb and xauth (X.Org; from GFM Tiny OS 0.1.4) | A hidden screen, so installers run with no monitor | MIT / X11 |
| x11vnc (from GFM Tiny OS 0.1.5) | SHOW SCREEN: an installer's hidden screen, only while an install runs and only on the rig itself (GFM reaches it over its SSH login) | GPL-2.0-or-later |
| GStreamer plugins (Ubuntu's gstreamer1.0-plugins-base, gstreamer1.0-plugins-good and gstreamer1.0-libav; from GFM Tiny OS 0.1.15) | Videos and cutscenes in Windows programs (Wine plays them through GStreamer) | LGPL-2.1-or-later (gstreamer1.0-libav decodes with Ubuntu's FFmpeg libraries, built GPL-2.0-or-later) |
| Steam (Valve; Ubuntu multiverse's steam-installer, from GFM Tiny OS 0.1.6 MANAGEMENT - installed on the rig only when you press INSTALL STEAM, never bundled) | Steam on the rig (OPEN / SHOW / CLOSE STEAM) | Valve's Steam Subscriber Agreement - you accept it yourself in INSTALL STEAM's confirmation |
| steam-devices (installed with Steam) | Controllers and VR devices for Steam (udev rules) | MIT |
| Sunshine 2025.924.154138 (LizardByte; GFM's pinned `sunshine-ubuntu-24.04-amd64.deb` from LizardByte's GitHub release, size + sha256 checked by the build; from GFM Tiny OS 0.1.7) | PROGRAMS: streams one program's session to GFM | GPL-3.0-only (source: section 2) |
| libminiupnpc17 and libicu74 (Ubuntu 24.04's packages, pinned by size + sha256; from 0.1.7) | Libraries Sunshine's 24.04 build needs | BSD-3-Clause / Unicode (ICU) licence |
| sway (wlroots; from 0.1.7) | A program's own headless session on its GPU | MIT |
| wlroots (Ubuntu's libwlroots source, built by the GFM Tiny OS factory with GFM's exact-frame-clock change - mineros/factory/gfm-wlroots-exact-clock.py - and installed as <version>+gfm1; from 0.1.16) | The session screen's frame clock: exactly the stream's frame rate (it was whole milliseconds) | MIT |
| Xwayland (X.Org; from 0.1.7) | Windows (X11) programs inside that session | MIT / X11 |
| PipeWire, pipewire-pulse and WirePlumber (from 0.1.7) | The session's sound | MIT |
| pulseaudio-utils (from 0.1.7) | Sound checks in the session (pactl) | LGPL-2.1-or-later |
| dbus-bin (from 0.1.7) | The session's message bus | AFL-2.1 or GPL-2.0-or-later |
| Mesa (mesa-vulkan-drivers incl. 32-bit, mesa-va-drivers, libgl1-mesa-dri; from 0.1.7) | AMD / Intel graphics, Vulkan and video encoding | MIT |
| vulkan-tools (from 0.1.7) | Checking that Vulkan works | Apache-2.0 |
| NVIDIA's graphics, encode and decode libraries (libnvidia-gl / -encode / -decode at the driver's version; from 0.1.7) | NVIDIA graphics and NVENC video encoding for the stream | NVIDIA's licence (as the driver) |
| NVIDIA's GBM library (libnvidia-extra at the driver's version; from 0.1.8) | Lets a program's session make NVIDIA screen buffers (without it the stream is black) | NVIDIA's licence (as the driver) |
| MangoHud (mangohud; from 0.1.10) | The performance strip over a program (FPS / CPU / GPU / RAM / VRAM) | MIT |
| SDL 2 (Ubuntu's libsdl2-2.0-0; from 0.1.11) | Controllers in programs that run on Proton (Proton reaches controllers through SDL) | zlib |
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
| Music | ACE-Step 1.5 | MIT |
| Music | Stable Audio Open 1.0 (short clips) | Stability AI Community License |
| Music | ACE-Step 1.5 with 4B LLM | ACE-Step licence |
| Music | MiniMax Music 3 | MiniMax model licence |
| Music | ACE-Step 1.5 XL Turbo | ACE-Step licence |
| 3D | Hunyuan3D 2.0 | Tencent Hunyuan Community License (not EU, UK, South Korea) |
| 3D | Hunyuan3D 2.1 | Tencent Hunyuan Community License (not EU, UK, South Korea) |
| 3D | Pixal3D + TRELLIS.2 | TRELLIS.2 MIT + Pixal3D licence |

GFM's small support models (for example Qwen3 1.7B / 4B in GGUF form) are downloaded from Hugging Face under
their makers' licences (Qwen3: Apache-2.0).

The GFM Voice Studio (DEPLOY SERVICES) downloads Qwen3-TTS-12Hz-1.7B-VoiceDesign and Qwen3-TTS-12Hz-1.7B-Base (Qwen,
Apache-2.0) and Whisper small.en in the faster-whisper format (Systran, MIT) onto the rig. Rigsby's voice that ships
with GFM (`gpufarm/web/rigby/voice`: the recording his voice is locked to and his voice pack) was made with
Qwen3-TTS (Apache-2.0); a voice you lock from a real person's recording must be your own or used with that person's
permission.

---

## 7. Data: the PCI ID list

When a GPU has no driver yet, Windows only calls it "Microsoft Basic Display Adapter". GFM then looks up its PCI
device ID in the public PCI ID list by **The PCI ID Repository** (https://pci-ids.ucw.cz), used under the
**BSD 3-Clause License** (the list is dual-licensed BSD-3-Clause / GPL-2.0-or-later). The GFM PC downloads the
list when a card needs it and keeps the NVIDIA, AMD and Intel display entries in GFM's data folder (refreshed
monthly). GFM does not ship or change the list.

---

## 8. Optional Linux vLLM bundle

INSTALL VLLM copies the separately built, reviewed `vllm-0.32.0-gfm1` bundle from GFM's Deployment Cache to a
Linux rig's program storage. It contains vLLM 0.32.0 with GFM's tensor-padding and serving patches; it is not a
library inside the Windows app or desktop client. The reviewed bundle's size and SHA-256 are pinned in
`gpufarm/vllm_manifest.py`.

| Component | Version | Licence | What it does in GFM |
|---|---|---|---|
| vLLM (the vLLM project and contributors) | 0.32.0, with GFM patches | [Apache-2.0](https://github.com/vllm-project/vllm/blob/v0.32.0/LICENSE) | Serves the selected worker's language model through GFM's adapter and gateway. Upstream source: https://github.com/vllm-project/vllm/tree/v0.32.0; GFM's patch sources: `gpufarm/vllm_patches`. |

The factory copies its Python environment, including package metadata and licence files, into the bundle. Python,
PyTorch, NVIDIA CUDA runtime libraries and the other dependencies each keep their own licences; the vLLM licence
does not replace those terms. Their versions come from the factory's reviewed `conda-explicit.lock` and
`requirements.lock` inputs, with installed package metadata under the bundle's `env` directory. The model weights
are a separate download under their publisher's terms.
