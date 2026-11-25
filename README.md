![logo](doc/img/logo-banner.png)

# watchex

[![CI](https://github.com/kevinboss/watchex/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/kevinboss/watchex/actions/workflows/ci.yml)
[![GitHub release](https://img.shields.io/github/v/release/kevinboss/watchex)](https://github.com/kevinboss/watchex/releases)
[![licence](https://img.shields.io/github/license/kevinboss/watchex)](https://github.com/kevinboss/watchex/blob/main/LICENSE)

watchex evaluates a `.csproj` file and its project references for files marked
with `CopyToOutputDirectory` set to `Always` or `PreserveNewest`. It watches
those files and copies them to the build output directory whenever they change,
so you do not need to rebuild the project after editing content files like
translations or non-standard configurations.

Install with
[winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/):

```powershell
winget install francWhite.watchex
```

Run `watchex` in a project directory, and press Enter to stop:

```sh
watchex                            # watch the .csproj in the current directory
watchex -p src/MyApp/MyApp.csproj  # target a specific project file
watchex -v                         # log watched files and change events
```

See [doc/usage.md](doc/usage.md) for other install methods, all options, and
how project evaluation works.

## How to contribute

Fork the repository and open a pull request against `main`. See
[CONTRIBUTING.md](CONTRIBUTING.md) for prerequisites, build and test commands,
code style, and credits.
