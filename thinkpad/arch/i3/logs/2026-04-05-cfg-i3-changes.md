## what
add xrandr, and brightness to the i3 config

## why
so on each reload/reboot, system has 30% brightness set + night light filter via xrandr

## Command
xrandr --output eDP-1 --gamma 1:0.8:0.7
brightnessctl set 30%

## Output
successful operation
