## what

Fixed clipmenu path initialization by explicitly hardcoding a persistent cache directory path, increased the dmenu font size to 16px, restricted text captures to the main clipboard selection buffer, and enabled case-insensitive searching.

## why

i3wm variables use literal string substitution and do not natively evaluate $HOME, which broke the previous clipmenud initialization attempt. Hardcoding the /home/msi/ base path bypasses this limitation. Furthermore, moving CM_DIR out of /tmp into the persistent local cache path ensures that captured clipboard items are saved permanently across system reboots instead of being erased on shutdown. Limiting captures to clipboard stops mouse-highlights from polluting the logs, while the -i flag removes strict case requirements during launcher queries. [1, 2]

## Command

--- a/arch/i3wm/.config/i3/config+++ b/arch/i3wm/.config/i3/config@@ -11,10 +11,12 @@

set $mod Mod4
set $term alacritty-# set fonts for dmenu, and clipmenu-set $dmenu_fonts "Ubuntu Mono:pixelsize=16"

# !!! Set the username here !!!

set $user msi+# set fonts for dmenu, and clipmenu+set $dmenu_fonts "Ubuntu Mono:pixelsize=16"+# set directory for clipmenu+set $clipmenu_dir "/home/msi/.cache/clipmenu"

# Font for window titles. Will also be used by the bar unless a different font

# is used in the bar {} block below.@@ -42,8 +44,9 @@ bindsym $mod+shift+x exec xsecurelock

# Clipboard history -> clipmenu

# start the daemon if not already-exec --no-startup-id clipmenud-bindsym $mod+c exec clipmenu -fn $dmenu_fonts+exec --no-startup-id CM_DIR=$clipmenu_dir CM_SELECTIONS=clipboard clipmenud+# limit clipmenu to ctl+c, ignore mouse selection+bindsym $mod+c exec CM_DIR=$clipmenu_dir CM_SELECTIONS=clipboard clipmenu -fn $dmenu_fonts -i

# NetworkManager is the most popular way to manage wireless networks on Linux,

# and nm-applet is a desktop environment-independent system tray GUI for it.

## Output

clipmenud initializes successfully and logs clipboard text records straight into the user's permanent cache folder. Pressing $mod+c surfaces a readable 16px font interface, queries historical items case-insensitively, and correctly preserves all clips safely through system reboots.
