---
layout: post
title: "Fix monitor with broken EDID"
---
### Issue description
Monitor's EDID is damaged and Ubuntu is running at lower resolution

### How to fix
1. Read timing from a working monitor (same mode)
   ```sh
   sudo get-edid | parse-edid
   ```
2. Create a new script `/etc/lightdm/video-mode` with desired timing
   ```sh
   #!/bin/sh

   /usr/bin/xrandr --newmode FHD 148.50 1920 2008 2052 2200 1080 1084 1089 1125 +hsync +vsync
   /usr/bin/xrandr --addmode DisplayPort-0 FHD
   ```
3. Add the following line at the end of `/etc/lightdm/lightdm.conf` to autoload the timing
```
display-setup-script=/etc/lightdm/video-mode
```
