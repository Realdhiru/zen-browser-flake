# Zen Browser Nix Flake

Declarative Nix flake packaging the official [Zen Browser](https://zen-browser.app) desktop application for NixOS and Linux systems.

## Features
- **Official Binaries**: Packages the official Linux releases with hardware acceleration and Wayland integration.
- **Dual Architecture**: Supports `x86_64-linux` and `aarch64-linux`.
- **Automated Upstream Sync**: Configured with automated CI workflows checking for new upstream releases.
- **Firefox Policies**: Unnecessary in-app update checks disabled by default to conform with Nix immutability.

## Installation

### In NixOS Flake (`flake.nix`)

Add `zen-browser-flake` to your `inputs`:

```nix
inputs = {
  nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";

  zen-browser = {
    url = "github:Realdhiru/zen-browser-flake";
    inputs.nixpkgs.follows = "nixpkgs";
  };
};
```

Then add the package to your `environment.systemPackages` or Home Manager `home.packages`:

```nix
environment.systemPackages = [
  inputs.zen-browser.packages.${pkgs.system}.default
];
```

### Direct CLI Install

```bash
nix profile install github:Realdhiru/zen-browser-flake
```

## Maintenance

To manually check for updates and update source hashes locally:

```bash
nix run .#update
```

## License

Upstream packaging derivation licensed under the Unlicense / MIT. Zen Browser belongs to the Zen Browser team.
