## what

Exported graphical environment variables to the systemd user session registry and automated the initialization handshake via the window manager config.

## why

Modern applications like Zed and web browsers rely on `xdg-desktop-portal-gtk` to draw system file/folder upload dialogs. Because i3 launches independently of a heavy desktop environment, the portal backend was crashing with a `cannot open display:` error on execution. Injecting the runtime variables tells the background service layer exactly where to draw the graphical interfaces.

## Command

```bash
nano ~/.config/i3/config
dbus-update-activation-environment --systemd DISPLAY XAUTHORITY XDG_CURRENT_DESKTOP
systemctl --user restart xdg-desktop-portal-gtk
```

```diff
--- a/home/msi/.config/i3/config
+++ b/home/msi/.config/i3/config
@@ -1,3 +1,6 @@
 # i3 config file (v4)

 # rest of the i3 configuration...

+# Sync environment variables with systemd user session for file dialogs
+exec --no-startup-id dbus-update-activation-environment --systemd DISPLAY XAUTHORITY XDG_CURRENT_DESKTOP
+
```
