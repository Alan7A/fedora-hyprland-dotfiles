# Fedora Hyprland dotfiles

This is a collection of dotfiles for Fedora Hyprland.

## Enable DNF fastest mirror and update

- Edit `/etc/dnf/dnf.conf` and append the following lines
  ```sh
  fastestmirror=true
  deltarpm=true
  ```
- Run
  ```sh
  sudo dnf up
  ```

## Install packages

1. Enable extra repositories
   ```bash
   sudo rpm -Uvh https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
   sudo rpm -Uvh https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
   flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
   sudo dnf copr enable solopasha/hyprland
   ```
1. Install packages
   ```bash
   sudo dnf install vim kitty hyprland hyprpicker hyprshot hyprlock hypridle hyprpaper hyprcursor waypaper pipewire wireplumber rofi-wayland playerctl mpv grim slurp jq bc xdg-desktop-portal-hyprland wl-clipboard socat cliphist nm-connection-editor dictd blueman bluez wlogout brightnessctl neofetch solaar breeze-cursor-theme numix-icon-theme-circle meson rustc glib glib2-devel sassc cargo gtk3 gtk3-devel systemd-devel gtk-layer-shell-devel libevdev-devel libinput-devel openssl
   ```
1. Install vscode
   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
   sudo dnf check-update
   sudo dnf install -y code
   ```
1. Install flatpak apps
   ```bash
   flatpak install flathub io.github.zen_browser.zen
   flatpak install flathub com.google.Chrome
   flatpak install flathub org.gnome.Geary
   flatpak install flathub com.discordapp.Discord
   flatpak install flathub dev.vencord.Vesktop
   flatpak install flathub io.github.celluloid_player.
   flatpak install flathub com.github.PintaProject.Pinta
   flatpak install flathub io.missioncenter.MissionCenter
   flatpak install flathub com.github.tchx84.Flatseal
   flatpak install flathub com.github.wwmm.easyeffects
   flatpak install flathub md.obsidian.Obsidian
   flatpak install flathub org.gnome.Extensions
   ```

## Setup ZSH

- Install ZSH and set as default shell

  ```sh
  sudo dnf install -y zsh
  sudo chsh -s $(which zsh)
  echo $SHELL
  # The trailing should change from $ to %
  ```

- Install [Oh My Zsh](https://ohmyz.sh/#install)
  ```sh
  sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
  ```
- Install plugin [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  ```sh
  git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
  ```
- Install plugin [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  ```sh
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
  ```
- Install [Powerlevel10k](https://github.com/romkatv/powerlevel10k) theme
  ```sh
  git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
  ```
- Replace the files `.p10k.zsh` and `.zshrc` into the `Home` folder

## Download and install fonts

- Meslo Nerd Font, download these four ttf files and double click on them:

  - [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
  - [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
  - [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
  - [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)

## Copy config files and restart

- Copy the contents of `.config` folder to `~/.config`
- Copy other files to `~/`
- Restart and select **Hyprland** in login screen

## Install other packages

- [HyprPanel](https://hyprpanel.com/getting_started/installation.html#fedora)
- [Hyprshade](https://github.com/loqusion/hyprshade)
- [overskride](https://github.com/kaii-lb/overskride)

## Extras

### Set gkt theme

```sh
gsettings set org.gnome.desktop.interface gtk-theme "Tokyonight-Dark"
```

### Git configurations

```sh
git config --global init.defaultBranch main
git config --global core.editor "vim"
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

## FAQ

#### Styles not applied to HyprPanel on startup

You need to create a symlink for sass from ~/.bun/bin/sass to /usr/bin/sass and create a symlink for bun from ~/.bun/bin/bun to /usr/bin/bun

```bash
sudo ln -s ~/.bun/bin/sass /usr/bin/sass
sudo ln -s ~/.bun/bin/bun /usr/bin/bun
```
