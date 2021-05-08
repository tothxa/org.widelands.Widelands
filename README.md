# widelands-flatpak

**Widelands** is a free (libre / open source) (GPLed), realtime-strategy game.

[Homepage](https://www.widelands.org)

This repo is only for the flatpak package definition ("manifest").


## Requirements

* [flatpak](https://flatpak.org/setup)
* [flatpak-builder](https://docs.flatpak.org/en/latest/first-build.html)
* [org.freedesktop.Sdk version 20.08 from flathub.org](#sdk-and-runtime)
* [org.freedesktop.Platform version 20.08 from flathub.org](#sdk-and-runtime)
* [check out submodules](#submodules)

See [below](#details) if you need help installing them.


## Quick Start

When the above are all set up, you can use the provided `compile` shell
script to build the program, the repo and the bundle (`widelands.flatpak`).
Once you have built it, you can test with the provided `run` shell script.

See [below](#build) for details on what they do.


## Details

### SDK and runtime

Add repository:

```
$ flatpak remote-add --if-not-exists "flathub" "https://dl.flathub.org/repo/flathub.flatpakrepo"
```

Install (you can also install systemwide if you have access by removing `--user`):

```
$ flatpak --user install "flathub" "org.freedesktop.Sdk//20.08"
$ flatpak --user install "flathub" "org.freedesktop.Platform//20.08"
```

### Submodules

Clone this repository, then check out the parts to the `shared-modules`
directory:

```
$ git submodule init
$ git submodule update
```

### Build

```
$ flatpak-builder --force-clean build --repo=repo org.widelands.Widelands.yaml
```

`build` is the directory name where flatpak-builder will copy the result.
`--repo=repo` tells flatpak-builder to also make a "repo" in the `repo`
directory. You will need this to create a "bundle", ie. the widelands.flatpak
single file package, but you can also skip it, because it takes a while to
generate after building.

### Test run without installing

```
$ flatpak-builder --run "build" "org.widelands.Widelands.yaml" "widelands"
```

### Debugging

You can enter the runtime environment of the package and run any command
(in this example a shell):

```
$ flatpak-builder --run "build" "org.widelands.Widelands.yaml" "sh"
```

### Build single-file bundle (flatpak package)

The `compile` script does it, but you may want to skip it first, because it
takes a while. You can do it separately with this command (`repo` is the
directory where you generated the repo):

```
$ flatpak build-bundle repo widelands.flatpak org.widelands.Widelands --runtime-repo="https://flathub.org/repo/flathub.flatpakrepo"
```

### Install single-file bundle

```
$ flatpak --user install "widelands.flatpak"
```

Again, you can also install systemwide if you have access by removing `--user`

### Run after installing

```
$ flatpak --user run "org.widelands.Widelands"
```

Without `--user` if installed systemwide.


## See also:

* [Widelands GitHub repo](https://github.com/widelands/widelands)
* [This GitHub repo (check out the local-build branch)](https://github.com/tothxa/org.widelands.Widelands)
* [GitHub repo of the Widelands package on flathub.org](https://github.com/flathub/org.widelands.Widelands)
* [Setting up flatpak](https://flatpak.org/setup)
* [Building your first Flatpak](http://docs.flatpak.org/en/latest/first-build.html)
* [Single-file bundles](http://docs.flatpak.org/en/latest/single-file-bundles.html#single-file-bundles)


## FAQ

### Does the game have access to the host file system?

No, it is sandboxed.

### Does flatpak-ed Widelands run as superuser?

[No](https://github.com/flatpak/flatpak/issues/1557). It is a
[MATE](https://github.com/mate-desktop)/[marco](https://github.com/mate-desktop/marco)
[issue](https://github.com/mate-desktop/marco/issues/301).

### Are you the author of Widelands?

No, I only updated the flatpak package for it starting from
[scx's repo](https://github.com/scx/widelands-flatpak)


## Thanks

Thank you to the Widelands team for creating the game and to scx and others
for creating the flatpak manifest.

