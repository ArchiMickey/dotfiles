# Configuration for my Arch Desktop
## Configure system
Configure pacman:
```
sudo vim /etc/pacman.conf
```
Enable `Color`, `multilib` and `ParallelDownloads`
1. Install yay:
```
mkdir ~/Collections
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git ~/Collections/
cd ~/Collections/yay && makepkg -si
```
2. Install drivers:
NVIDIA:
```
yay -S cuda cuda-tools nvidia nvidia-utils lib32-nvidia
```
Others:
```
yay -S mesa lib32-mesa vulkan-radeon amdvlk
```
3. Install gaming drivers:
```
yay -S wine-staging wine-gecko wine-mono pipewire-pulse lib32-libpulse lib32-alsa-lib lib32-alsa-plugins
```
4. Install daily apps:
```
yay -Syu zsh vim nano kitty google-chrome visual-studio-code-bin tmux btop noto-fonts-cjk nerd-fonts-complete whatsapp-nativefier signal-desktop spotify
flatpak install discord
```

5. Configure zsh
```
# Install oh-my-zsh
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```
```
# Install p10k theme
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# install plugin
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-autocomplete
```

6. Download .ssh from Onedrive:
```
# Run after downloaded and extracted .ssh
sudo chmod 600 .ssh/*
```

7. Clone this repo and copy home config files
```
git clone git@github.com:ArchiMickey/dotfiles.git ~/ && cd ~/dotfiles
cp -r dot_home/. ~/
```
## Theme
### GTK and icon
```
yay -S catppuccin-gtk-theme-macchiato
git clone git@github.com:vinceliuice/Tela-icon-theme.git ~/Collections/
cd Collections/Tela-icon-theme && ./install.sh
```
Change the theme and icons in gnome tweaks
### background
```
cp background/* ~/.local/share/background/
```
### btop
```
cp dot_config/btop/catppuccin_macchiato.theme ~/.config/btop/themes/
```
Change the theme in btop options.
### grub
```
sudo cp -r grub_theme/catppuccin_macchiato /usr/share/grub/themes/
```
Uncomment and edit following line in `/etc/default/grub` to selected theme:
```
GRUB_THEME="/usr/share/grub/themes/catppuccin-macchiato-grub-theme/theme.txt"
```
Update grub:
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
### Kitty
```
cp -r dot_config/kitty/* ~/.config/kitty/
```
### spicetify
Run spotify once before executing the below command.
```
yay -S spicetify-cli
sudo chmod a+wr /opt/spotify
sudo chmod a+wr /opt/spotify/Apps -R
cp -r dot_config/spicetify/catppuccin-macchiato ~/.config/spicetify/Themes/
cp dot_config/spicetify/catppuccin-macchiato.js ~/.config/spicetify/Extensions/
spicetify config current_theme catppuccin-macchiato
spicetify config color_scheme lavender
spicetify config inject_css 1 replace_colors 1 overwrite_assets 1
spicetify config extensions catppuccin-macchiato.js
spicetify backup apply
```

## GNOME
Install extension manager:
```
yay -S extension-manager
```
### Extensions:
Setup Extensions Sync first, it will sync the extensions automatically\
[Extensions Sync](https://extensions.gnome.org/extension/1486/extensions-sync/)\
gist_id: be6312204bc74a3b2596394ce24123ce \
gist_token: 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 \
#### Using Extensions:
[BaBar Task Bar](https://extensions.gnome.org/extension/4000/babar/) \
[Blur my Shell](https://extensions.gnome.org/extension/3193/blur-my-shell/) \
[Dash to Dock for COSMIC](https://extensions.gnome.org/extension/5004/dash-to-dock-for-cosmic/) \
[GTK Title Bar](https://extensions.gnome.org/extension/1732/gtk-title-bar/) \
[Just Perfection](https://extensions.gnome.org/extension/3843/just-perfection/) \
[Media Controls](https://extensions.gnome.org/extension/4470/media-controls/) \
[Tray Icons: Reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)
