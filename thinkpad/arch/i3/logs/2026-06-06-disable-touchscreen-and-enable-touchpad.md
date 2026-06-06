## what

- Configured automated touchpad tap-to-click functionality on system initialization.
- Disabled the faulty internal laptop touchscreen device completely at the X11 server layer.

## why

- Touchpad: The system defaults to disabling tap-to-click on boot, requiring manual xinput property changes on every session launch.
- Touchscreen: The ELAN touchscreen controller was throwing broken, empty IRQ interrupt flags into the system bus. This caused a race condition that would periodically lock the main physical keyboard driver into an un-jammed "infinity repeat mode" until rebooted. Ignoring the device completely stabilizes the hardware line.

## Command

```diff
--- a/arch/i3wm/.config/i3/config
+++ b/arch/i3wm/.config/i3/config
@@ -1,3 +1,6 @@
 # i3 config file (v4)

--- /dev/null
+++ b/etc/X11/xorg.conf.d/30-touchpad.conf
@@ -0,0 +1,7 @@
+Section "InputClass"
+    Identifier "Synaptics Touchpad Tapping"
+    MatchIsTouchpad "on"
+    Driver "libinput"
+    Option "Tapping" "on"
+EndSection

--- /dev/null
+++ b/etc/X11/xorg.conf.d/99-disable-touchscreen.conf
@@ -0,0 +1,7 @@
+Section "InputClass"
+    Identifier "Block Broken Touchscreen"
+    MatchIsTouchscreen "on"
+    Driver "libinput"
+    Option "Ignore" "on"
+EndSection
```

## Output

- xinput list: The touchscreen device ELAN901C no longer registers or spawns device handlers in the system user space interface.
- Touchpad Behavior: Tap-to-click is fully operational immediately after loading into the i3 workspace layout.
- Keyboard Stability: The typematic keyboard buffer lines no longer experience packet drops or infinite loop lockups during prolonged system uptime.
