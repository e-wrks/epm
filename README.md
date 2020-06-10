# Đ (Edh) Package Manager

## What is EPM

**epm** is a single [bash](https://www.gnu.org/software/bash/) script making
it easy to put together various [Đ (Edh)](https://github.com/e-wrks/edh)
packages from different parties, and work well.

**Edh** has localization of package dependencies in mind, **epm** is so far
semi-automatic in dealing with that, and ought to go fully automatic as it
evolves.

**EPM** may evolve to have some <b title="Graphical User Interface">GUI</b>
in the future, but stays merely the
<b title="Command Line Interface">CLI</b> **epm** at the moment.

- [What is EPM](#what-is-epm)
- [Prerequisite](#prerequisite)
  - [Operation System](#operation-system)
  - [UNIX Toolchain](#unix-toolchain)
- [Installation](#installation)
- [Usage](#usage)
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
To build Edh programs, you need
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

```console
$ epm --help
epm 0.1.6 >> Edh Package Manager <<

USAGE:
    epm [FLAGS] <SUBCOMMAND>

FLAGS:
    -v, --verbose         Enable verbose output
    -h, --help            Prints help information
    -V, --version         Prints version information
    -B, --base <URL>      URL prefix for upstream package repositories
                     default:  https://gogs.dw/e-wrks
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

## Usage

```bash
$ mkdir edh-home
$ cd edh-home
$ epm init edh nedh # and other packages you like
```

<details><summary>...</summary>

```bash
Installing edh to edh-universe/e-wrks/edh ...
Cloning into 'edh-universe/e-wrks/edh'...
remote: Counting objects: 3664, done.
remote: Compressing objects: 100% (677/677), done.
remote: Total 3664 (delta 2233), reused 3609 (delta 2211)
Receiving objects: 100% (3664/3664), 726.31 KiB | 11.17 MiB/s, done.
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
```

</details>

```bash
$ cabal run edhi
```

<details><summary>...</summary>

```bash
Resolving dependencies...
Build profile: -w ghc-8.8.3 -O1
In order, the following will be built (use -v for more details):
 - lossless-decimal-0.1.1.0 (lib) (first run)
 - edh-0.3.0.0 (lib:edh-internal) (first run)
 - edh-0.3.0.0 (lib) (first run)
 - edh-0.3.0.0 (exe:edhi) (first run)
Configuring library for lossless-decimal-0.1.1.0..
Preprocessing library for lossless-decimal-0.1.1.0..
Building library for lossless-decimal-0.1.1.0..
[1 of 1] Compiling Data.Lossless.Decimal ( src/Data/Lossless/Decimal.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/lossless-decimal-0.1.1.0/build/Data/Lossless/Decimal.o )
Configuring library 'edh-internal' for edh-0.3.0.0..
Preprocessing library 'edh-internal' for edh-0.3.0.0..
Building library 'edh-internal' for edh-0.3.0.0..
[ 1 of 19] Compiling Language.Edh.Control ( src/Language/Edh/Control.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/l/edh-internal/build/edh-internal/Language/Edh/Control.o )
[ 2 of 19] Compiling Language.Edh.Details.PkgMan ( src/Language/Edh/Details/PkgMan.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/l/edh-internal/build/edh-internal/Language/Edh/Details/PkgMan.o )
  ...
[18 of 19] Compiling Language.Edh.Runtime ( src/Language/Edh/Runtime.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/l/edh-internal/build/edh-internal/Language/Edh/Runtime.o )
[19 of 19] Compiling Language.Edh.Batteries ( src/Language/Edh/Batteries.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/l/edh-internal/build/edh-internal/Language/Edh/Batteries.o )
Configuring library for edh-0.3.0.0..
Preprocessing library for edh-0.3.0.0..
Building library for edh-0.3.0.0..
[1 of 1] Compiling Language.Edh.EHI ( pub/Language/Edh/EHI.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/build/Language/Edh/EHI.o )
Configuring executable 'edhi' for edh-0.3.0.0..
Preprocessing executable 'edhi' for edh-0.3.0.0..
Building executable 'edhi' for edh-0.3.0.0..
[1 of 2] Compiling Repl             ( repl/Repl.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/x/edhi/build/edhi/edhi-tmp/Repl.o )
[2 of 2] Compiling Main             ( repl/Main.hs, /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/x/edhi/build/edhi/edhi-tmp/Main.o )
Linking /home/cyue/edh-home/dist-newstyle/build/x86_64-osx/ghc-8.8.3/edh-0.3.0.0/x/edhi/build/edhi/edhi ...
```

</details>

```bash
>> Bare Đ (Edh) Interpreter <<
* Blank Screen Syndrome ? Take the Tour as your companion, checkout:
  https://github.com/e-wrks/edh/tree/master/Tour
Đ: dir
/home/cyue/edh-home/edh_modules/repl/__main__.edh:1:1
  __name__=/home/cyue/edh-home/edh_modules/repl
  __repr__=module:/home/cyue/edh-home/edh_modules/repl
  __file__=/home/cyue/edh-home/edh_modules/repl/__main__.edh
Đ:
```

```bash
$ stack run nedh
```

<details><summary>...</summary>

```bash
lossless-decimal> configure (lib)
lossless-decimal> Configuring lossless-decimal-0.1.1.0...
lossless-decimal> build (lib)
lossless-decimal> Preprocessing library for lossless-decimal-0.1.1.0..
lossless-decimal> Building library for lossless-decimal-0.1.1.0..
lossless-decimal> [1 of 1] Compiling Data.Lossless.Decimal
lossless-decimal> copy/register
lossless-decimal> Installing library in /home/cyue/edh-home/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/lossless-decimal-0.1.1.0-HCYm1yn9Rt2Jeqs1sJLXPz
lossless-decimal> Registering library for lossless-decimal-0.1.1.0..
edh             > configure (lib + internal-lib + exe)
edh             > Configuring edh-0.3.0.0...
edh             > build (lib + internal-lib + exe)
edh             > Preprocessing library 'edh-internal' for edh-0.3.0.0..
edh             > Building library 'edh-internal' for edh-0.3.0.0..
edh             > [ 1 of 19] Compiling Language.Edh.Control
edh             > [ 2 of 19] Compiling Language.Edh.Details.PkgMan
  ...
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
edh             > Installing internal library edh-internal in /home/cyue/edh-home/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/edh-0.3.0.0-73PuCsmdUcIHXX9IKK7eJA-edh-internal
edh             > Installing library in /home/cyue/edh-home/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/edh-0.3.0.0-AIDEnedhsqmDPELtxqIvBW
edh             > Installing executable edhi in /home/cyue/edh-home/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/bin
edh             > Registering library 'edh-internal' for edh-0.3.0.0..
edh             > Registering library for edh-0.3.0.0..
Building all executables for `nedh' once. After a successful build of all of them, only specified executables will be rebuilt.
nedh            > configure (lib + internal-lib + exe)
Configuring nedh-0.1.0.0...
nedh            > build (lib + internal-lib + exe)
Preprocessing library 'nedh-internal' for nedh-0.1.0.0..
Building library 'nedh-internal' for nedh-0.1.0.0..
[1 of 7] Compiling Language.Edh.Net.Addr
[2 of 7] Compiling Language.Edh.Net.MicroProto
[3 of 7] Compiling Language.Edh.Net.Peer
[4 of 7] Compiling Language.Edh.Net.Client
[5 of 7] Compiling Language.Edh.Net.Server
[6 of 7] Compiling Language.Edh.Net.Sniffer
[7 of 7] Compiling Language.Edh.Net.Advertiser
Preprocessing library for nedh-0.1.0.0..
Building library for nedh-0.1.0.0..
[1 of 1] Compiling Language.Edh.Net
Preprocessing executable 'nedh' for nedh-0.1.0.0..
Building executable 'nedh' for nedh-0.1.0.0..
[1 of 2] Compiling Repl
[2 of 2] Compiling Main
Linking .stack-work/dist/x86_64-osx/Cabal-3.0.1.0/build/nedh/nedh ...
nedh            > copy/register
Installing internal library nedh-internal in /home/cyue/edh-home/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/nedh-0.1.0.0-IB11KjcvZDCA4St0hQLCbM-nedh-internal
Installing library in /home/cyue/edh-home/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/lib/x86_64-osx-ghc-8.8.3/nedh-0.1.0.0-ILXJZuI6ug3CgbFjo1OY5g
Installing executable nedh in /home/cyue/edh-home/.stack-work/install/x86_64-osx/0654fccd5f476b2c5a8c0895b218cd844a1f8be9784b79bd15206177b5607fa2/8.8.3/bin
Registering library 'nedh-internal' for nedh-0.1.0.0..
Registering library for nedh-0.1.0.0..
Completed 3 action(s).
```

</details>

```bash
>> Networked Edh <<
* Blank Screen Syndrome ? Take the Tour as your companion, checkout:
  https://github.com/e-wrks/nedh/tree/master/Tour
(net)Đ: dir
/home/cyue/edh-home/edh_modules/net/__main__.edh:1:1
  sendData=@sendData
  dataChan=dataChan := "data"
  __name__=/home/cyue/edh-home/edh_modules/net
  sendConMsg=@sendConMsg
  Advertiser=Advertiser
  Server=Server
  conin=conin := 0
  __repr__=module:/home/cyue/edh-home/edh_modules/net
  sendConOut=@sendConOut
  sendCmd=@sendCmd
  __file__=/home/cyue/edh-home/edh_modules/net/__main__.edh
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

## Roadmap

Features of priority to come next:

- Automatic dependency installation

- Validation, resolution, and automated settlement of versions of dependency

- Content-addressable local cache
