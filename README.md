# jank-win-release

Prebuilt Windows binaries for **jank** using MSYS2 CLANG64.
Includes:

* **LLVM** (dependency)
* **jank-win** (Windows build)

Binaries are on [Releases](https://github.com/ikappaki/jank-win-release/releases) under tags:

* `llvm-<source-cut-date>`
* `jank-<jank-src-cut-date>-<jank-win-src-cut-date>`

---

## Prerequisites

Install [MSYS2](https://www.msys2.org/) and use the **MSYS2 CLANG64** terminal for all commands.

---

## Installation

### Using `jank-win-updater` (recommended)

```bash
curl -fsSL https://github.com/ikappaki/jank-win-release/raw/refs/heads/main/jank-win-updater | bash
```

> Installs `jank-win-updater` to `~/.local/bin`. Make sure it's in your `PATH`.

```bash
jank-win-updater           # checks for updates and suggests actions
jank-win-updater --llvm    # install/update LLVM
jank-win-updater --jank    # install/update jank
jank-win-updater --self    # update the updater script
```

Optional: `--all`, `--jank [tag]`, `--llvm [tag]`,

---

### Manual

1. Download releases from [Releases](https://github.com/ikappaki/jank-win-release/releases).

2. **Install LLVM** (multiple packages):

```bash
mkdir -p ~/jank-win-temp/llvm
tar -C ~/jank-win-temp/llvm -xf llvm-<tag>.tar
pacman -U --noconfirm ~/jank-win-temp/llvm/*.pkg.tar.zst
rm -rf ~/jank-win-temp/llvm
```

3. **Install jank-win** (single package):

```bash
pacman -U /path/to/mingw-w64-clang-x86_64-jank-<tag>.pkg.tar.zst
```

---

## Running jank

**MSYS2 CLANG64 terminal:**

```bash
jank
```

**Windows PowerShell / cmd:**

1. Open the **MSYS2 CLANG64 terminal** and get the Windows path:

```bash
cygpath -w /clang64/bin
```

2. Use that path to update your Windows PATH temporarily:

Powershell:
```powershell
$env:Path = "<output-of-cygpath>" + ";" + $env:Path
jank
```

cmd:
```cmd
set PATH=<output-of-cygpath>;%PATH%
jank
```

> For permanent access, add the path returned by `cygpath -w /clang64/bin` to the system PATH.
