# Sep

Quick and dirty python program to separate strings using a CLI

# Nix

This project is my first nix package? flake? so that I could learn how to integrate various parts of the Nix ecosystem.

## Use with NixOS

We can use this package in our NixOS configuration if we have enabled flakes with the following:

```nix
{
  description = "My NixOS Configuration";

  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
    myPackage.url = "github:ejovo13/sepstring";
  };

  outputs = { self, nixpkgs, myPackage }: {
    nixosConfigurations = {
      mySystem = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix
          { environment.systemPackages = [ myPackage.defaultPackage.x86_64-linux ]; }
        ];
      };
    };
  };
}

```
