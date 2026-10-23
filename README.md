# AUR pkgs

[![License][badge-1-img]][badge-1-link]

## About

This repo maintains packages for AUR (Arch Linux User Repository). 

## Packages

### Torresmo

> [homepage][1]

#### Installation

```sh
$AUR_HELPER -S torresmo
```

### TTFE

> [homepage][2]

#### Installation

```sh
$AUR_HELPER -S ttfe
```

### SuperHTML

> [homepage][3]

#### Installation

```sh
$AUR_HELPER -S superhtml-git
```

## Publishing

Every package lives in its own folder and is pushed to its AUR repository with
`git subtree`. Run these steps on an Arch machine, inside the package folder.

First, update `PKGBUILD`'s `pkgver` and `pkgrel` to the correct version. Then:

```sh
updpkgsums                              # from pacman-contrib
```

Packaging-only change (same upstream version): bump `pkgrel` instead, and skip
`updpkgsums`.

Then, for both cases:

```sh
makepkg -sfi                                           # build, run the tests, install
namcap PKGBUILD $pkg-$pkgver-$pkgrel-$arch.pkg.tar.zst # lint, should print nothing
makepkg --printsrcinfo > .SRCINFO
git add PKGBUILD .SRCINFO
git commit
cd ..
git push
git remote add aur-$pkg ssh://aur@aur.archlinux.org/$pkg.git # optional
git subtree push --prefix $pkg aur-$pkg master
```

## Source code

The main repository is on [SourceHut][source-srht]. Mirrors exist on
[Codeberg][source-codeberg] and [GitHub][source-github] for convenience, but
they might occasionally be outdated.

### License and contribution

This project's code is in the public domain. See the
[LICENSE file][source-license].

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you shall be in the public domain, without any
additional terms or conditions.

[1]: https://sr.ht/~paemuri/torresmo
[2]: https://sr.ht/~paemuri/ttfe
[3]: https://github.com/kristoff-it/superhtml

[badge-1-img]: https://img.shields.io/badge/license-Unlicense-green?style=flat-square
[badge-1-link]: ./LICENSE

[source-srht]: https://git.sr.ht/~paemuri/aur-pkgs
[source-codeberg]: https://codeberg.org/paemuri/aur-pkgs
[source-github]: https://github.com/paemuri/aur-pkgs
[source-license]: ./LICENSE
