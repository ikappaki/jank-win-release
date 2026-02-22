# jank-win-release

Prebuilt Windows binaries for [jank-win](https://github.com/ikappaki/jank-win) using MSYS2 CLANG64.
Includes **LLVM** (dependency) and **jank-win** (the windows build).

## Prerequisites

Install [MSYS2](https://www.msys2.org/) and use the **MSYS2 CLANG64** terminal for all commands.

## Installation

### Using `jank-win-updater`

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

### Manual

Binaries are available on [Releases](https://github.com/ikappaki/jank-win-release/releases) under tags `llvm-<inc>--<source-cut-date>` and `jank-<inc>-<jank-src-cut-date>-<jank-win-src-cut-date>`.

1. Download the latest [releases](https://github.com/ikappaki/jank-win-release/releases).

2. **Install LLVM**:

```bash
export LLVM_BIN_PREFIX=llvm-<...>
mkdir -p ~/jank-win-temp/llvm
tar -C ~/jank-win-temp/llvm -xf ${LLVM_BIN_PREFIX}.tar
pacman -U --noconfirm ~/jank-win-temp/llvm/*.pkg.tar.zst
rm -fr ~/jank-win-temp/llvm
```

3. **Install jank-win**:

```bash
pacman -U mingw-w64-clang-x86_64-jank-<tag>.pkg.tar.zst
```

## Running jank

**MSYS2 CLANG64 terminal:**

```bash
jank check-health
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
jank check-health
```

cmd:
```cmd
set PATH=<output-of-cygpath>;%PATH%
jank check-health
```

> For permanent access, add the path returned by `cygpath -w /clang64/bin` to the system PATH.
