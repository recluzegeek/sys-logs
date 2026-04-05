## what
* Added `xrandr` and brightness settings to i3 config
* Installed `stow` for dotfiles management and `feh` for wallpapers; downloaded wallpapers for customization
* Set up a Pacman hook to auto-update `pkg-explicit.txt` inside the dotfiles repo
* Add new fonts packages, `ttf-font-awesome`, `ttf-ubuntu-font-family`, and set their font-size to 14 in the i3 config.
* Customized i3status bar with nerd font icons (battery, wifi, clock), and font-size

## why
* Ensure system brightness is set to 30% and Night Light filter via `xrandr` is applied on each reload or reboot
* Keep dotfiles, scripts, and package list automatically versioned and up-to-date

## Command

```bash
xrandr --output eDP-1 --gamma 1:0.8:0.7
brightnessctl set 30%
```

* For Pacman hook, scripts, and wallpapers, see dotfiles repo

## Output
* Commands executed successfully; settings applied as expected
