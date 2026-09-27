# Gaming video

## enabling opengpl and GPU drivers

```nix
# configuration.nix

{ pkgs, ... }:

{

  hardware.graphics = {
    enable = true;
    enable32Bit = true;
  };

  #         \/\/\/ this DOES also do wayland
  services.xserver.videoDrivers = ["amdgpu"];

}
```

## getting ids

```bash
nix shell nixpkgs#pciutils -c lspci | grep ' VGA '"
```

## wrappers

```nix
# configuration.nix

{ pkgs, ... }:

{

  programs.steam.enable = true;
  programs.steam.gamescopeSession.enable = true;

  environment.systemPackages = with pkgs; [
    mangohud
  ];

  programs.gamemode.enable = true;

}
```


## protonup

```nix
# configuration.nix

{ pkgs, ... }:

{

  environment.systemPackages = with pkgs; [
    protonup
  ];
  
  environment.sessionVariables = {
    STEAM_EXTRA_COMPAT_TOOLS_PATHS =
      "\${HOME}/.steam/root/compatibilitytools.d";
  };

}
```

```nix
# home.nix

{ pkgs, ... }:

{

  home.packages = with pkgs; [
    protonup
  ];

  home.sessionVariables = {
    STEAM_EXTRA_COMPAT_TOOLS_PATHS =
      "\\\${HOME}/.steam/root/compatibilitytools.d";
  };

}
```

```bash
protonup -d "~/.steam/root/compatibilitytools.d/"
```

## nixos-hardware

https://github.com/NixOS/nixos-hardware
