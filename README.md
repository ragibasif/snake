# Snake

Snake is a lightweight CLI utility that sanitizes file and directory names by replacing non-alphanumeric characters with underscores.

## How it works

- Every character that is not `a-z`, `A-Z`, or `0-9` is replaced with `_`
- Consecutive underscores are collapsed into one
- Leading and trailing underscores are removed
- If the resulting name is empty (e.g. the original name was all symbols), the file is renamed to a UTC timestamp
- Hidden files and directories (names starting with `.`) are skipped

## Requirements

Python 3.13+

## Installation

### Prerequisites

Install Python 3.13+ for your platform before proceeding.

**macOS (Homebrew)**
```bash
brew install python@3.13
```

**Ubuntu / Debian**
```bash
sudo apt update && sudo apt install -y python3.13
```

**Fedora**
```bash
sudo dnf install python3.13
```

**Arch Linux**
```bash
sudo pacman -S python
```

**openSUSE**
```bash
sudo zypper install python313
```

**Windows (winget)**
```powershell
winget install Python.Python.3.13
```

**Windows (Chocolatey)**
```powershell
choco install python --version=3.13
```

### Install snake

**macOS / Linux**
```bash
chmod +x snake.py
mv snake.py snake
sudo cp snake /usr/local/bin/snake
```

**Windows (PowerShell — run as Administrator)**

Place `snake.py` somewhere on your `PATH` (e.g. `C:\Tools`) and create a wrapper:
```powershell
New-Item -ItemType Directory -Force -Path "C:\Tools"
Copy-Item snake.py C:\Tools\snake.py
Set-Content C:\Tools\snake.cmd "@python C:\Tools\snake.py %*"
# Add C:\Tools to PATH if not already present
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Tools", "Machine")
```

## Usage

```bash
snake [-h] [-v] [-r] [-f FILE | -d DIR]
```

| Flag | Long form      | Description                                                   |
|------|----------------|---------------------------------------------------------------|
| `-h` | `--help`       | Show help message and exit                                    |
| `-v` | `--verbose`    | Enable DEBUG-level logging                                    |
| `-r` | `--recursive`  | Recurse into subdirectories (not usable with `-f`)            |
| `-f` | `--file`       | Operate on a single file or directory (mutually exclusive with `-d`, `-r`) |
| `-d` | `--directory`  | Operate on a specific directory (mutually exclusive with `-f`) |

## Examples

```bash
# Sanitize only the current directory (non-recursive)
snake

# Sanitize the current directory and all subdirectories
snake --recursive

# Enable verbose output
snake --verbose

# Recursive with verbose output
snake --verbose --recursive

# Operate on a single file or directory
snake --file my\ file\ (1).txt

# Operate on a specific directory (non-recursive)
snake --directory path/to/dir

# Operate on a specific directory recursively
snake --recursive --directory path/to/dir
```

### Rename examples

| Before                | After                          |
|-----------------------|--------------------------------|
| `my file (1).txt`     | `my_file_1.txt`                |
| `__Hello, World!__`   | `Hello_World`                  |
| `résumé.pdf`          | `r_sum.pdf`                    |
| `2024-01-15_notes`    | `2024_01_15_notes`             |
| `!!!.log`             | `20260224153000000000UTC.log`  |

## License

Licensed under the MIT License. See [LICENSE](LICENSE) for details.
