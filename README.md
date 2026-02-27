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

**First run:**

```bash
jank-win-updater --all     # install LLVM and jank
```

**After initial setup:**

```bash
jank-win-updater           # check for updates and suggest actions
jank-win-updater --llvm    # install/update LLVM
jank-win-updater --jank    # install/update jank
jank-win-updater --self    # update the updater script
```

Optional: `--jank [tag]`, `--llvm [tag]`

### Manual

Binaries are available on [Releases](https://github.com/ikappaki/jank-win-release/releases) under tags `llvm-<inc>-<source-cut-date>` and `jank-<inc>-src<jank-src-cut-date>-win<jank-win-src-cut-date>` for jank (upstream jank snapshot -> Windows port snapshot).

1. Download the latest LLVM and jank-win [releases](https://github.com/ikappaki/jank-win-release/releases).

2. **Install LLVM**:

```bash
export LLVM_TAR=llvm-<...>.tar
mkdir -p ~/jank-win-temp/llvm
tar -C ~/jank-win-temp/llvm -xf ${LLVM_TAR}.tar
pacman -U --noconfirm ~/jank-win-temp/llvm/*.pkg.tar.zst
rm -fr ~/jank-win-temp/llvm
```

3. **Install jank-win**:

```bash
pacman -U mingw-w64-clang-x86_64-jank-<tag>.pkg.tar.zst
```

## Running jank

In the **MSYS2 CLANG64 terminal**, `jank` can be run directly:

```bash
jank check-health
```

On Windows, to run jank from PowerShell, cmd, or other shells, add the MSYS2 CLANG64 bin directory to your PATH.

From the MSYS2 CLANG64 terminal, run:

```bash
cygpath -w /clang64/bin
```

This prints the Windows-style path (e.g. `C:\msys64\clang64\bin`).

Temporary update:

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

For permanent access, add the same path to the system PATH.
