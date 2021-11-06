## 🖥️ Display

#### Setting up VNC 
Vncserver is pre-installed, you can start it manually too instead of `startvnc`.
```
tigervncserver -geometry 2560x1080 -xstartup /usr/bin/xfce4-session -listen tcp :1 
```

#### Display over other devices
If you wanna run VNC Viewer on another device then connect both devices in same network (or hotspot from main device name). And then start vncserver like this manually.
```
tigervncserver -geometry 2560x1080 -localhost no -xstartup /usr/bin/xfce4-session -listen tcp :1 
```

And in another device use `WLAN IP:port` for connecting. ( use `ip a` in termux and copy the 192.168.xx.xx)

#### Setting up xRDP
RDP is another great way to get gui, even much better input and resolution setups automatically. For using it first install xRDP. (note it'll use VNC for backend and might bugs while rendering).
```
sudo apt install xRDP
```

Now need to configure a bit, first need to create xsession.
```
echo "xfce4-session > ~/.xsession
```

The second file we need to edit is the startup file for XRDP, so it will start the desktop.
```
nano /etc/xrdp/startwm.sh
```

Delete all the content there and paste this: #!/bin/sh
```
if [ -r /etc/default/locale ]; then
  . /etc/default/locale
  export LANG LANGUAGE
fi

xfce4-session 
```

Now start xRDP with
```
sudo service xrdp start
```
Connect it to `localhost:3389` with RDP client.


#### Setting up Xwayland
First in termux install xwayland
```
pkg install xwayland
```

Start wayland server with
``` 
Xwayland -ac :1 > /dev/null
```

And then start udroid manually with
```
proot-distro login udroid --shared-tmp --bind /dev/null:proc/sys/kernel/cap_last_cap
```

In it, launch desktop with
```
DISPLAY=:1 startxfce4
```