# AUR pkgs

## About

This repo maintains packages for AUR (Arch Linux User Repository). 

## Packages

### Torresmo

> [homepage][1] | [repository][2]

#### Installation

```sh
$AUR_HELPER -S torresmo
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
makepkg -sfi                            # build, run the tests, install
namcap PKGBUILD *.pkg.tar.zst           # lint, should print nothing
makepkg --printsrcinfo > .SRCINFO
git add PKGBUILD .SRCINFO
git commit
cd ..
git push
git subtree push --prefix <package> aur-<package> master
```

## License

This project code is in the public domain. See the [LICENSE file][3].

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you shall be in the public domain, without any
additional terms or conditions.

[1]: https://sr.ht/~paemuri/torresmo
[2]: https://git.sr.ht/~paemuri/torresmo
[3]: ./LICENSE