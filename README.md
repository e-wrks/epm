# Đ (Edh) Package Manager

## What is EPM

**epm** is a single [bash](https://www.gnu.org/software/bash/) script making
it easy to put together various [Đ (Edh)](https://github.com/e-wrks/edh)
packages from different parties, and work well.

**Edh** has localization of package dependencies in mind, **epm** is so far
semi-automatic in dealing with that, and ought to go fully automatic as it
evolves.

**EPM** may evolve to have some <b title="Graphical User Interface">GUI</b>
in the future, but stays merely the **epm**
<b title="Command Line Interface">CLI</b> at the moment.

- [What is EPM](#what-is-epm)
- [Prerequisite](#prerequisite)
  - [Operation System](#operation-system)
  - [UNIX Toolchain](#unix-toolchain)
- [Installation](#installation)
- [Usage](#usage)
  - [Create a new EPM home](#create-a-new-epm-home)
  - [Develop your Edh projects](#develop-your-edh-projects)
    - [Code Editor for Đ (Edh)](#code-editor-for-đ-edh)
  - [Build Edh interpreters](#build-edh-interpreters)
- [Roadmap](#roadmap)

## Prerequisite

### Operation System

- **Linux** or **macOS**

  <details><summary>
  On Windows<sup>TM</sup> ? 
  </summary>

  Maybe try your luck with:

  - [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)

  But don't expect things would go smoothly if it works at all.

  </details>

### UNIX Toolchain

> You may already have all of them if you are a software developer, otherwise:

<details><summary>
To manage Edh packages locally, you need
</summary>

- [bash](https://www.gnu.org/software/bash/) - You already have it

  It comes with a decent **Linux** or **macOS** box.

- [git](https://git-scm.com/) - You get it

  From your **Linux** distribution's package manager, e.g.

  ```bash
  sudo apt install git
  ```

  Or for your **macOS**, run following command and follow its prompts

  > Note:
  > It installs a full fledged compiler toolchain, maybe bloating to
  > you, yet better to have.

  ```bash
  xcode-select --install
  ```

</details>

<details><summary>
To build Haskell executables from Edh packages, you need
</summary>

- [GHC](https://haskell.org/ghc)
- [Cabal-install](https://www.haskell.org/cabal)

  You install'em all by any single **one**, or **all** of the following:

- [ghcup](https://www.haskell.org/ghcup)
- [Stack](https://haskellstack.org)
- [Nix](https://nixos.org/download.html)

  > Confused? You are not alone, just continue the
  > [struggling](https://www.reddit.com/r/haskell/comments/a69ww2/struggling_to_get_started_with_developing_with)
  > and keep questioning that many (yet none perfect) competing options with
  > the [Haskell community](https://www.haskell.org/community)

</details>

## Installation

```bash

curl -o ~/.local/bin/epm -L https://github.com/e-wrks/epm/raw/latest/epm

chmod a+x ~/.local/bin/epm

```

<details><summary>

```bash
$ epm --help
```

</summary>

```console
epm 0.1.7 >> Edh Package Manager <<

USAGE:
    epm [FLAGS] <SUBCOMMAND>

FLAGS:
    -v, --verbose      Enable verbose output
    -h, --help         Prints help information
    -V, --version      Prints version information
    -B, --base <URL>   URL prefix for upstream package repositories
                         default:  https://github.com/e-wrks
                         environment variable EPM_REPO_BASE overrides above

SUBCOMMANDS:
    init               Initialize current working directory as an EPM home
    install     | i    Install new, or change branches of existing packages
    list        | l    List homes and packages
    update | up | u    Pull upstream changes of packages from tracked branches
    with        | w    Run command within the directory of a package
    run | exec  | x    Run command with all effective EPM home's bin on $PATH
    rm                 Remove specified package(s) from nearest EPM home
```

</details>

## Usage

### Create a new EPM home

```bash
$ mkdir epm-home
$ cd epm-home
$ epm init edh nedh # and other packages you like
```

<details><summary>...</summary>

```console
Installing edh to edh-universe/e-wrks/edh ...
Cloning into 'edh-universe/e-wrks/edh'...
remote: Counting objects: 3664, done.
remote: Compressing objects: 100% (677/677), done.
remote: Total 3664 (delta 2233), reused 3609 (delta 2211)
Receiving objects: 100% (3664/3664), 726.31 KiB | 9.95 MiB/s, done.
Resolving deltas: 100% (2233/2233), done.
Installed edh .
Installing nedh to edh-universe/e-wrks/nedh ...
Cloning into 'edh-universe/e-wrks/nedh'...
remote: Counting objects: 902, done.
remote: Compressing objects: 100% (244/244), done.
remote: Total 902 (delta 412), reused 842 (delta 384)
Receiving objects: 100% (902/902), 120.68 KiB | 3.35 MiB/s, done.
Resolving deltas: 100% (412/412), done.
Installed nedh .
$
```

</details>

> Note **epm** maintains `${EPM_HOME}/edh-universe` as both a valid
> [Cabal](https://www.haskell.org/cabal) project and a valid
> [Stack](https://haskellstack.org) project.

```bash
$ ls
edh-universe	edh_modules
$ cd edh-universe/
$ ls
bin		cabal.project	e-wrks		stack.yaml
```

> and **epm** redirects **Haskell** executables to be built into
> `${EPM_HOME}/edh-universe/bin` .

### Develop your Edh projects

These 2 folders - `edh-universe` and `edh_modules` - are material of an **EPM**
home and maintained by **epm**, you create folder structures beside them to
organize your **Edh** related stuff, maybe just simple **Edh** scripts,
full fledged interpreter packages, or database server and applications
atop [HasDB](https://github.com/e-wrks/hasdb).

#### Code Editor for Đ (Edh)

The officially recommended code editor (and **IDE**) for
[Đ (Edh)](https://github.com/e-wrks/edh) is:

[Visual Studio Code](https://code.visualstudio.com) with
[Edh Language Pack](https://marketplace.visualstudio.com/items?itemName=ComplYue.edh-vscode-pack)

There you go with decent syntax highlighting and automatic code formatting.

Semantic hinting and debugging features will come along.

### Build Edh interpreters

To build all **Haskell** exectuables (mosts are **Edh** interpreters with
different sets of batteries included) from installed **Edh** packages, you
can freely choose between [Cabal-install](https://www.haskell.org/cabal)
and [Stack](https://haskellstack.org) whichever you like.

- with **Cabal-install**

> The `epm run` subcommand treats `cabal install` specially, it adds
> `--overwrite-policy=always` and `--installdir=${EPM_HOME}/edh-universe/bin`
> to the actual command line.

```bash
$ epm run cabal install all:exes
```

<details><summary>...</summary>

```console
 >> Managing packages at EPM home [/Users/cyue/epm-home] <<
Wrote tarball sdist to
/Users/cyue/epm-home/edh-universe/dist-newstyle/sdist/edh-0.3.0.0.tar.gz
Wrote tarball sdist to
/Users/cyue/epm-home/edh-universe/dist-newstyle/sdist/lossless-decimal-0.1.1.0.tar.gz
Wrote tarball sdist to
/Users/cyue/epm-home/edh-universe/dist-newstyle/sdist/nedh-0.1.0.0.tar.gz
Resolving dependencies...
Up to date
Symlinking 'edhi'
Symlinking 'nedh'
$
```

</details>

- or with **Stack**

> **epm** sets `local-bin-path: ${EPM_HOME}/edh-universe/bin` in `stack.yaml`

```bash
$ stack install
```

<details><summary>...</summary>

```console
lossless-decimal> configure (lib)
lossless-decimal> Configuring lossless-decimal-0.1.1.0...
lossless-decimal> build (lib)
lossless-decimal> Preprocessing library for lossless-decimal-0.1.1.0..
lossless-decimal> Building library for lossless-decimal-0.1.1.0..
lossless-decimal> [1 of 1] Compiling Data.Lossless.Decimal
lossless-decimal> copy/register
lossless-decimal> Installing library in /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/lossless-decimal-0.1.1.0-HCYm1yn9Rt2Jeqs1sJLXPz
lossless-decimal> Registering library for lossless-decimal-0.1.1.0..
Building all executables for `edh' once. After a successful build of all of them, only specified executables will be rebuilt.
edh             > configure (lib + internal-lib + exe)
edh             > Configuring edh-0.3.0.0...
edh             > build (lib + internal-lib + exe)
edh             > Preprocessing library 'edh-internal' for edh-0.3.0.0..
edh             > Building library 'edh-internal' for edh-0.3.0.0..
edh             > [ 1 of 19] Compiling Language.Edh.Control
edh             > [ 2 of 19] Compiling Language.Edh.Details.PkgMan
edh             > [ 3 of 19] Compiling Language.Edh.Details.RtTypes
edh             > [ 4 of 19] Compiling Language.Edh.Details.CoreLang
edh             > [ 5 of 19] Compiling Language.Edh.Details.Utils
edh             > [ 6 of 19] Compiling Language.Edh.Event
edh             > [ 7 of 19] Compiling Language.Edh.Parser
edh             > [ 8 of 19] Compiling Language.Edh.Details.Evaluate
edh             > [ 9 of 19] Compiling Language.Edh.Details.Tx
edh             > [10 of 19] Compiling Language.Edh.Batteries.Vector
edh             > [11 of 19] Compiling Language.Edh.Batteries.Reflect
edh             > [12 of 19] Compiling Language.Edh.Batteries.Math
edh             > [13 of 19] Compiling Language.Edh.Batteries.Evt
edh             > [14 of 19] Compiling Language.Edh.Batteries.Data
edh             > [15 of 19] Compiling Language.Edh.Batteries.Ctrl
edh             > [16 of 19] Compiling Language.Edh.Batteries.Console
edh             > [17 of 19] Compiling Language.Edh.Batteries.Assign
edh             > [18 of 19] Compiling Language.Edh.Runtime
edh             > [19 of 19] Compiling Language.Edh.Batteries
edh             > Preprocessing library for edh-0.3.0.0..
edh             > Building library for edh-0.3.0.0..
edh             > [1 of 1] Compiling Language.Edh.EHI
edh             > Preprocessing executable 'edhi' for edh-0.3.0.0..
edh             > Building executable 'edhi' for edh-0.3.0.0..
edh             > [1 of 2] Compiling Repl
edh             > [2 of 2] Compiling Main
edh             > Linking .stack-work/dist/x86_64-osx/Cabal-3.0.1.0/build/edhi/edhi ...
edh             > copy/register
edh             > Installing internal library edh-internal in /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/edh-0.3.0.0-73PuCsmdUcIHXX9IKK7eJA-edh-internal
edh             > Installing library in /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/edh-0.3.0.0-AIDEnedhsqmDPELtxqIvBW
edh             > Installing executable edhi in /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/bin
edh             > Registering library 'edh-internal' for edh-0.3.0.0..
edh             > Registering library for edh-0.3.0.0..
Building all executables for `nedh' once. After a successful build of all of them, only specified executables will be rebuilt.
nedh            > configure (lib + internal-lib + exe)
nedh            > Configuring nedh-0.1.0.0...
nedh            > build (lib + internal-lib + exe)
nedh            > Preprocessing library 'nedh-internal' for nedh-0.1.0.0..
nedh            > Building library 'nedh-internal' for nedh-0.1.0.0..
nedh            > [1 of 7] Compiling Language.Edh.Net.Addr
nedh            > [2 of 7] Compiling Language.Edh.Net.MicroProto
nedh            > [3 of 7] Compiling Language.Edh.Net.Peer
nedh            > [4 of 7] Compiling Language.Edh.Net.Client
nedh            > [5 of 7] Compiling Language.Edh.Net.Server
nedh            > [6 of 7] Compiling Language.Edh.Net.Sniffer
nedh            > [7 of 7] Compiling Language.Edh.Net.Advertiser
nedh            > Preprocessing library for nedh-0.1.0.0..
nedh            > Building library for nedh-0.1.0.0..
nedh            > [1 of 1] Compiling Language.Edh.Net
nedh            > Preprocessing executable 'nedh' for nedh-0.1.0.0..
nedh            > Building executable 'nedh' for nedh-0.1.0.0..
nedh            > [1 of 2] Compiling Repl
nedh            > [2 of 2] Compiling Main
nedh            > Linking .stack-work/dist/x86_64-osx/Cabal-3.0.1.0/build/nedh/nedh ...
nedh            > copy/register
nedh            > Installing internal library nedh-internal in /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/nedh-0.1.0.0-IB11KjcvZDCA4St0hQLCbM-nedh-internal
nedh            > Installing library in /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/nedh-0.1.0.0-ILXJZuI6ug3CgbFjo1OY5g
nedh            > Installing executable nedh in /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/bin
nedh            > Registering library 'nedh-internal' for nedh-0.1.0.0..
nedh            > Registering library for nedh-0.1.0.0..
Completed 3 action(s).
Copying from /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/bin/edhi to /Users/cyue/epm-home/edh-universe/bin/edhi
Copying from /Users/cyue/epm-home/edh-universe/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/bin/nedh to /Users/cyue/epm-home/edh-universe/bin/nedh

Copied executables to /Users/cyue/epm-home/edh-universe/bin:
- edhi
- nedh

Warning: Installation path /Users/cyue/epm-home/edh-universe/bin not found on the PATH environment variable.
$
```

</details>

Then you can run any of them:

<details><summary>

```bash
$ epm run edhi
```

</summary>

```bash
 >> Managing packages at EPM home [/Users/cyue/epm-home] <<
>> Bare Đ (Edh) Interpreter <<
* Blank Screen Syndrome ? Take the Tour as your companion, checkout:
  https://github.com/e-wrks/edh/tree/master/Tour
Đ: dir
/Users/cyue/epm-home/edh_modules/repl/__main__.edh:1:1
  __name__=/Users/cyue/epm-home/edh_modules/repl
  __repr__=module:/Users/cyue/epm-home/edh_modules/repl
  __file__=/Users/cyue/epm-home/edh_modules/repl/__main__.edh
Đ:
```

</details>

<details><summary>

```bash
$ epm run nedh
```

</summary>

```bash
 >> Managing packages at EPM home [/Users/cyue/epm-home] <<
>> Networked Edh <<
* Blank Screen Syndrome ? Take the Tour as your companion, checkout:
  https://github.com/e-wrks/nedh/tree/master/Tour
(net)Đ: dir
/Users/cyue/epm-home/edh_modules/net/__main__.edh:1:1
  sendData=@sendData
  dataChan=dataChan := "data"
  __name__=/Users/cyue/epm-home/edh_modules/net
  sendConMsg=@sendConMsg
  Advertiser=Advertiser
  Server=Server
  conin=conin := 0
  __repr__=module:/Users/cyue/epm-home/edh_modules/net
  sendConOut=@sendConOut
  sendCmd=@sendCmd
  __file__=/Users/cyue/epm-home/edh_modules/net/__main__.edh
  Client=Client
  consoleTo=consoleTo
  conout=conout := 1
  dataSink=@dataSink
  Peer=Peer
  netPeer=@netPeer
  Addr=Addr
  conmsg=conmsg := 2
  Sniffer=Sniffer
  consoleOn=consoleOn
  errChan=errChan := "err"
(net)Đ:
```

</details>

## Roadmap

Features of priority to come next for **EPM**:

- Automatic dependency installation

- Validation, resolution, and automated settlement of versions of dependency

- Content-addressable local cache
