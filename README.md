# <p align="center">ikeg-maker</p>

<p align="center">
  <img src="https://img.shields.io/badge/Available_for-Auro-4c1" alt="Available for Auro" />
  <a href="https://vibescale.github.io/#1">
    <img src="https://vibescale.github.io/badge-bar/3.svg" alt="3/6 Reviewed Copilot | Vibescale" />
  </a>
</p>

<p align="center">
  <i>Automatically generate `.ikeg` metadata files for **auro** package repositories.</i>
</p>

## Overview

`ikeg-maker` is a simple CLI tool that creates `.ikeg` metadata files used by the [auro](https://github.com/EliCJonas/auro) package manager (v1.4.5+). These files contain package metadata such as name, version, author, description, and download URL. The tool also maintains a `pkgs.list` index file that tracks all available packages in the repository.

## Installation

```bash
#Install from Auro repo
auro repo ikeg-maker

#Install from file
auro install ikeg-maker.keg
```

Requires **Python 3.6+**.

## Usage

```bash
ikeg-maker <package-name> [options]
```

### Required Arguments

| Argument | Description |
|----------|-------------|
| `name` | Package name (used as the `.ikeg` filename) |

### Optional Arguments

| Option | Short | Default | Description |
|--------|-------|---------|-------------|
| `--version` | `-v` | `0.1.0` | Package version |
| `--author` | `-a` | `""` | Package author |
| `--description` | `-d` | `""` | Package description |
| `--url` | `-u` | `""` | Download URL for the `.keg` archive |
| `--repo` | `-r` | `../auro-repo` | Path to the repository directory |

## Examples

### Basic Usage

```bash
ikeg-maker my-package --version 1.0.0 --author "John Doe" --description "A useful utility" --url "https://example.com/my-package.keg"
```

### Using Defaults

```bash
ikeg-maker simple-tool
# Creates simple-tool.ikeg with version 0.1.0, empty author/description/url
```

### Custom Repository Path

```bash
ikeg-maker my-package --repo /path/to/my/auro-repo
```

## Output

The tool creates two files in the repository directory:

1. **`<name>.ikeg`** - JSON metadata file:
   ```json
   {
     "name": "my-package",
     "version": "1.0.0",
     "author": "John Doe",
     "description": "A useful utility",
     "download-url": "https://example.com/my-package.keg"
   }
   ```

2. **`pkgs.list`** - Index file (appends package name if not already present):
   ```
   package-a
   package-b
   my-package
   ```

## Error Handling

- Exits with code `1` and prints an error if `<name>.ikeg` already exists
- Creates the repository directory and `pkgs.list` automatically if they don't exist