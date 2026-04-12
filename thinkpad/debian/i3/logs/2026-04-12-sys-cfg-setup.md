## what

- configured system for development
  - installed: terminator, podman, git, [git-ecosystem/git-credential-manager](https://github.com/git-ecosystem/git-credential-manager), spice-vdagent, firefox, dmenu, dunst, vscode, feh, stow, pcmanfm
- enabled contrib/non-free repos for additional packages (ubuntu-fonts)
- installed JetBrainsMono nerd font for i3status
- cloned dotfiles repo and applied via stow (minor tweaks for debian)

## why

- bootstrap minimal dev environment
- enable rootless container workflow (podman)
- ensure consistent config via dotfiles
- fix font/icons for status bar rendering
- enable secure git auth via GCM

## Command

- enabled repos for ubuntu-fonts
```bash
sudo sed -i 's/main non-free-firmware/main contrib non-free non-free-firmware/g' /etc/apt/sources.list
````

* install deb packages via apt

```bash
sudo apt update 
sudo apt install firefox terminator podman git spice-vdagent dmenu dunst feh stow pcmanfm

podman run hello-world
```

* downloaded [vscode debian pkg](https://code.visualstudio.com/download)

```bash
sudo apt install ./code_1.115.0-1775600353_amd64.deb
```

* downloaded jetbrains mono symbol font and refreshed font cache

```bash
wget -P ~/.local/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/JetBrainsMono.zip && cd ~/.local/share/fonts && unzip JetBrainsMono.zip && rm JetBrainsMono.zip && fc-cache -fv
```

* downloaded the git credentials manager deb package and configured

```bash
sudo apt install ./gcm-linux-x64-2.7.3.deb 
git-credential-manager configure
git config --global credential.credentialStore secretservice
```

* setup podman with docker compose (no podman-compose)

```bash
sudo mkdir -p /usr/local/lib/docker/cli-plugins

sudo cp Downloads/docker-compose /usr/local/lib/docker/cli-plugins/

sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose

systemctl --user enable --now podman.socket

export DOCKER_HOST=unix://$XDG_RUNTIME_DIR/podman/podman.sock

podman compose up
```

## Output

* apt update/install → OK
* podman hello-world → OK
* fonts installed + cache refreshed → OK
* GCM install/config → OK
* dotfiles stowed → OK
* podman socket → active
* docker-compose (podman backend) → not verified
* vscode → installed
