# Edh Package Manager

- [Prerequisite](#prerequisite)
  - [To manage Edh packages locally](#to-manage-edh-packages-locally)
  - [To build and run Edh programs](#to-build-and-run-edh-programs)
- [Installation](#installation)
- [Features](#features)
- [Roadmap](#roadmap)

## Prerequisite

- **Linux** or **macOS**

> On Windows? Maybe try your luck with:
>
> - [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
>
> But don't expect things would work smoothly if at all.

### To manage Edh packages locally

- [bash](https://www.gnu.org/software/bash/) -

  > You already have it on a decent **Linux** or **macOS** box.

- [git](https://git-scm.com/) - You get it

  > From your **Linux** distribution's package manager, e.g.

  ```bash
  sudo apt install git
  ```

  > Or for your **macOS**, run following command and follow its prompts

  ```bash
  xcode-select --install
  ```

### To build and run Edh programs

- [GHC](https://haskell.org/ghc)
- [Cabal-install](https://www.haskell.org/cabal)

> You install'em all by any single **one**, or **all** of the following:

- [ghcup](https://www.haskell.org/ghcup)
- [Stack](https://haskellstack.org)
- [Nix](https://nixos.org/download.html)

> Confused? You are not alone, just continue the
> [struggling](https://www.reddit.com/r/haskell/comments/a69ww2/struggling_to_get_started_with_developing_with)
> and keep questioning that many competing options with the
> [Haskell community](https://www.haskell.org/community)

## Installation

```bash

curl -o ~/.local/bin/epm -L https://github.com/e-wrks/epm/raw/stable/epm

chmod a+x ~/.local/bin/epm

epm --help

```

## Features

```console
epm 0.1.0 >> Edh Package Manager <<

USAGE:
    epm [FLAGS] <SUBCOMMAND>

FLAGS:
    -v, --verbose         Enable verbose output
    -h, --help            Prints help information
    -V, --version         Prints version information
    -B, --base <URL>      URL prefix for upstream package repositories
                    default:  https://github.com/e-wrks
                    environment variable EPM_REPO_BASE overrides above

SUBCOMMANDS:
    init                  Initialize current working directory as an EPM home
    install    | i        Install new, or change branches of existing packages
    list       | l        List homes and packages
    update     | u        Pull upstream changes of packages from tracked branches
    with       | w        Run command within the directory of a package
    run | exec | x        Run command with all effective EPM home's bin on $PATH
    rm                    Remove specified package(s) from nearest EPM home
```

## Roadmap

Priority to be added:

- Dependency based simple aggregation installation

- Dependency resolution & settlement

- Localized dependency settlement

- Content-addressable local cache
