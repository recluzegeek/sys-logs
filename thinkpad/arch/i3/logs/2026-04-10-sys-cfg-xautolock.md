## what
- screen lock when idle or lid closed (X server), i opted for xautolock with xsecurelock, over xss-lock with i3lock. Since, I was already using xsecurelock, and wants less work for the systemd :) so I'm going with xautolock.
- followed this guide: (securing your workspace by civicactions.com)[https://guidebook.civicactions.com/en/latest/common-practices-tools/security/securing-your-workspace/#screen-lock-with-xautolock]

## why
- had to install base-devel to build packages
- had to install dunst and libnotify for notification system
- running `dunst` and `xautolock` on X login, and is done via i3 config change.

## Command
sudo pacman -S base-devel

git clone https://aur.archlinux.org/xautolock.git
cd xautolock
mkpkg -si

sudo pacman -S dunst libnotify

-- added this line in i3 config

```diff
+ ## Start notification system
+ exec_always --no-startup-id dunst

+ ## autolocks via xsecurelock after 20 mins of inactivity, and suspend after 10 mins afterwards
+ exec_always --no-startup-id xautolock -detectsleep -time 20 -corners -000 -locker "/usr/bin/xsecurelock auth_pam_x11 saver_blank" -killtime 10 -killer "systemctl suspend" -notify 20 -notifier "notify-send -- 'Locking screen in 20 seconds'"
```

## Output
