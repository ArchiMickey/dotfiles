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
git clone https://aur.archlinux.org/yay.git ~/Collections/yay
cd ~/Collections/yay && makepkg -si
```
2. Install drivers:
NVIDIA:
```
yay -S cuda cuda-tools nvidia nvidia-utils lib32-nvidia-utils
```
Others:
```
yay -S mesa lib32-mesa vulkan-radeon amdvlk
```
3. Install gaming drivers:
```
yay -S wine-staging wine-gecko wine-mono pipewire-pulse lib32-libpulse lib32-alsa-lib lib32-alsa-plugins
```
4. Install daily apps and fonts:
```
yay -Syu zsh vim nano kitty google-chrome visual-studio-code-bin tmux btop whatsapp-nativefier signal-desktop spotify discord kuro-bin ulauncher
yay -S ttf-meslo-nerd noto-fonts-cjk
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
git clone git@github.com:conda-incubator/conda-zsh-completion.git ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/conda-zsh-completion
```

6. Download .ssh from Onedrive:
```
# Run after downloaded and extracted .ssh
sudo chmod 600 .ssh/*
```

7. Clone this repo and copy home config files
```
git clone git@github.com:ArchiMickey/dotfiles.git ~/dotfiles && cd ~/dotfiles
cp -r dot_home/. ~/
```

## Environment
Install micromamba:
```
curl micro.mamba.pm/install.sh | zsh
zsh
micromamba activate
micromamba install conda -c conda-forge
```

Install Rime:
1. Install packages:
```
yay -S ibus ibus-rime
```
2. Add environment variables to `/etc/environment`
```
GTK_IM_MODULE=ibus
QT_IM_MODULE=ibus
XMODIFIERS=@im=ibus
```

## Theme
### GTK and icon
```
yay -S catppuccin-gtk-theme-macchiato
git clone git@github.com:vinceliuice/Tela-icon-theme.git ~/Collections/Tela-icon-theme
cd ~/Collections/Tela-icon-theme && ./install.sh
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
### Ulauncher
```
cp -r dot_config/ulauncer/* ~/.config/ulauncher/
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
For 4K monitor, change the text size:
```
gsettings set org.gnome.desktop.interface text-scaling-factor 1.5
```
Install extension manager:
```
yay -S extension-manager
```
Disable extension gnome version check:
```
gsettings set org.gnome.shell disable-extension-version-validation true
```
## Extensions:
Setup Extensions Sync first, it will sync the extensions automatically.\
Laptop and desktop gists are separated now.\
[Extensions Sync](https://extensions.gnome.org/extension/1486/extensions-sync/)\
gist_id(desktop): 93e973b19d38f4e738cb5aed92048bc1 \
gist_id(laptop): 79c975baca86b82659994e055930334f \
gist_token: regenerate at [here](https://github.com/settings/tokens/1032391511)

### Using Extensions:
[BaBar Task Bar](https://extensions.gnome.org/extension/4000/babar/) \
[Blur my Shell](https://extensions.gnome.org/extension/3193/blur-my-shell/) \
[Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/) \
[Just Perfection](https://extensions.gnome.org/extension/3843/just-perfection/) \
[Media Controls](https://extensions.gnome.org/extension/4470/media-controls/) \
[Rounded Window Corners](https://extensions.gnome.org/extension/5237/rounded-window-corners/) \
[Tiling Assistant](https://extensions.gnome.org/extension/3733/tiling-assistant/) \
[Tray Icons: Reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)

## Mouse
### RGB for razer mouse:
```
yay -S linux-headers openrazer-meta
suod gpasswd -a $USER plugdev
yay -S polychromatic
```
Relogin to apply the changes.

### Logitech mouse:
```
yay -S solaar
```

## Nvidia
Nvidia sucks
```
sudo systemctl enable nvidia-suspend.service
sudo systemctl enable nvidia-hibernate.service
sudo cp nvidia/nvidia-power-management.conf /etc/modprobe.d/nvidia-power-management.conf
```
And add the kernel parameter `nvidia-drm.modeset=1` to `/etc/default/grub` and update grub. \
May need this for gdm:
```
ln -s /dev/null /etc/udev/rules.d/61-gdm.rules
```

## X11
```
sudo nvidia-xconfig --cool-bits=28
sudo cp nvidia/X11/Xwrapper.config /etc/X11/Xwrapper.config
```
