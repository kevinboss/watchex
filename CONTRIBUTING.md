# Contributing

## Prerequisites

Install [Git](https://git-scm.com/doc) and the
[.NET 10 SDK](https://learn.microsoft.com/en-us/dotnet/core/install/). The
solution targets `net10.0`.

## Building and testing

CI runs on `ubuntu-latest` for pushes and pull requests to `main` using these
commands:

```sh
dotnet restore ./src
dotnet build ./src --no-restore
dotnet test ./src --no-build --verbosity normal
```

To run watchex from source:

```sh
dotnet run --project ./src/Watchex -- -p path/to/App.csproj -v
```

Release builds (`-c Release`) enable single-file publishing with embedded debug
symbols and self-extracted native libraries, as configured in
[src/Watchex/Watchex.csproj](src/Watchex/Watchex.csproj).

## Code style

Follow the rules in [.editorconfig](.editorconfig): UTF-8 encoding, 2-space
indentation, trimmed trailing whitespace, and a 120-character line length limit
for source files.

## Submitting changes

Fork the repository, create a branch for your change, verify that the build and
tests pass, and open a pull request against `main`.

## Credits

watchex was created by [Francisco Metzger](https://github.com/francWhite) and
is maintained by [@kevinboss](https://github.com/kevinboss).
