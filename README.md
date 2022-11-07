# Configuration for my Arch Desktop
## Configure system
Configure pacman:
```
sudo vim /etc/pacman.conf
```
Enable `Color`, `multilib` and `ParallelDownloads`
1. Install yay:
```
sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si
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
yay -Syu zsh vim nano google-chrome visual-studio-code-bin tmux btop noto-cjk-fonts nerd-fonts-complete whatsapp-nativefier signal-desktop
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
Edit `.zshrc`:
```
ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(git zsh-autosuggestions zsh-syntax-highlighting sudo copypath z zsh-autocomplete)
```
Replace `.p10k.zsh`

## GNOME
### Extensions:
[BaBar Task Bar](https://extensions.gnome.org/extension/4000/babar/) \
[Blur my Shell](https://extensions.gnome.org/extension/3193/blur-my-shell/) \
[Dash to Dock for COSMIC](https://extensions.gnome.org/extension/5004/dash-to-dock-for-cosmic/) \
[GTK Title Bar](https://extensions.gnome.org/extension/1732/gtk-title-bar/) \
[Just Perfection](https://extensions.gnome.org/extension/3843/just-perfection/) \
[Media Controls](https://extensions.gnome.org/extension/4470/media-controls/) \
[Tray Icons: Reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)