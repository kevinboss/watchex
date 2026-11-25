# Usage

watchex evaluates a `.csproj` file and its `ProjectReference` dependencies for
items with `CopyToOutputDirectory` set to `Always` or `PreserveNewest`. It
watches those files and copies them to the build output directory on change.

## Installation

Install with
[winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/):

```powershell
winget install francWhite.watchex
```

Or install with [scoop](https://scoop.sh):

```powershell
scoop bucket add maple 'https://github.com/kevinboss/maple.git'
scoop install watchex
```

You can also download an archive from the
[releases page](https://github.com/kevinboss/watchex/releases), extract it, and
add the folder to your `PATH`.

## Command options

```text
USAGE:
    watchex [OPTIONS]

OPTIONS:
    -h, --help                 Prints help information
    -v, --verbose              Prints verbose log output
    -V, --version              Prints version information
    -p, --project <PROJECT>    Path to the project file. Defaults to the first *.csproj file found in the current directory.
```

If `-p` is omitted, watchex selects the first `*.csproj` file in the current
working directory. If no valid `.csproj` file is found, it prints an error and
exits with code `1`.

Pass `-v` to print the number of loaded projects, the detected
`CopyToOutputDirectory` items, each source-to-destination watcher mapping, and
a log line whenever a watched file changes.

Press Enter to stop watching and exit.

## How it works

watchex registers the default local MSBuild instance via `MSBuildLocator` and
loads the target `.csproj` together with all direct and transitive
`ProjectReference` projects. Because `Microsoft.Build` runtime assets are
excluded from the build, a local .NET SDK or MSBuild installation is required
at runtime.

For every item whose `CopyToOutputDirectory` metadata is not `Never`, watchex
maps the file from its owning project directory to the root project's
`OutputPath` directory. It creates a `FileSystemWatcher` monitoring `LastWrite`
events, throttles change notifications by 10 ms, creates missing destination
directories, and copies the updated file using `FileShare.ReadWrite`.

## Why not dotnet watch

`dotnet watch` has a limitation with non-compiled files in referenced projects.
When a dependency includes files with a wildcard like `translations\**\*.json`,
`dotnet watch` evaluates those paths in the startup project directory instead
of the dependency directory and misses changes. watchex resolves each file
relative to the dependency project that declared it.
