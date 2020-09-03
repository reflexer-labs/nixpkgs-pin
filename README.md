# Nix Packages

`nixpkgs` is a Nix package set with common GEB tools.

## Usage

### Adding binary cache

Add the Nix build cache for faster install times:

```sh
nix run nixpkgs-pin.cachix -c cachix use reflexer
```

### Installing a program from nixpkgs-pin

List `nixpkgs` specific packages:

```sh
nix-env -f https://github.com/reflexer-labs/nixpkgs-pin/tarball/master --description \
  -qaPA nixpkgs-pin
```

Search for a package:

```sh
nix search -f https://github.com/reflexer-labs/nixpkgs-pin/tarball/master seth
```

Installing `seth` from `nixpkgs-pin`:

```sh
nix-env -f https://github.com/reflexer-labs/nixpkgs-pin/tarball/master -iA seth
```

List available `dapptools` versions:

```sh
nix-env -f https://github.com/reflexer-labs/nixpkgs-pin/tarball/master --description \
  -qaPA dappSources
```

Versions are then available under the path `dappPkgsVersions.<version>`.

Installing `seth` from `dapptools` version `0.26.0`:

```sh
nix-env -f https://github.com/reflexer-labs/nixpkgs-pin/tarball/master \
  -iA dappPkgsVersions.dapp-0_26_0.seth
```

### Using nixpkgs in another Nix expression

Put the following at the top of your `default.nix`:

```nix
{ pkgs ? import (fetchGit "https://github.com/reflexer-labs/nixpkgs-pin") {}
}:
```

**Recommended**: Pin a package set at a certain revision by specifying `rev`
with the commit hash you wish to pin it at:

```nix
{ pkgs ? import (fetchGit {
    url = "https://github.com/reflexer-labs/nixpkgs-pin";
    rev = "86958dbb74d0f2e5a22bc0f397fe943140dfef41";
  }) {}
}:
```

You can also specify `ref` to point to a GIT branch or tag in combination with
or without `rev`.
