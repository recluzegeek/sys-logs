## what

- Replaced Alacritty terminal emulator with WezTerm.
- Changed default system shell from Bash to Zsh.
- Installed Starship cross-shell prompt for Zsh customization.
- Added Noto Fonts Emoji for proper terminal emoji rendering.
- Pushed configuration dotfiles for WezTerm, Zsh, and Starship.

## why

- WezTerm: Provides built-in multiplexing, ligatures, and better font configuration options than Alacritty.
- Zsh & Starship: Enhances terminal productivity with advanced auto-completion, speed, and a highly customizable, modern prompt interface.
- Noto Fonts: Resolves broken or missing emoji rendering across CLI tools and prompt themes.

## Command

```bash
# Install WezTerm, Zsh, Starship, and Noto Emoji font

sudo apt install wezterm zsh fonts-noto-color-emoji -y
curl -sS https://starship.rs | sh

# Change the default shell to Zsh

chsh -s $(which zsh)
```

## Output

````bash
$ echo $SHELL
/usr/bin/zsh

$ wezterm --version
wezterm 20240203-110809-5046fc22

$ starship --version
starship 1.25.1
tag:v1.25.1
commit_hash:8758daa77
build_time:2026-04-30 20:16:14 +00:00
build_env:rustc 1.95.0 (59807616e 2026-04-14) (Arch Linux rust 1:1.95.0-1),

# Terminal prompt successfully loads Starship theme with proper emoji rendering:

🚀 msi in 📁 ~/dotfiles .............................................................................................................................. main```
````
