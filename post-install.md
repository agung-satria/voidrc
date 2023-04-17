# post installation notes

```
sudo xbps-install -S
sudo xbps-install xbps
sudo xbps-install -Syu
sudo xbps-install -Rs void-repo-nonfree # add non-free repo
sudo xbps-install -Rs void-repo-multilib
sudo xbps-install -Rs void-repo-multilib-nonfree
```

# setting time using chrony!

source: [https://www.tecmint.com/synchronize-time-with-ntp-in-linux/](https://www.tecmint.com/synchronize-time-with-ntp-in-linux/)

- install: `sudo xbps-install chrony`
- enable service: `sudo ln -s /etc/sv/chronyd/ /var/service/`
- check service: `sudo sv status chronyd`
- configuration: `sudo nvim /etc/chrony.conf`
- setting:

This is default config, edit this two config:

```
# Use public NTP servers from the pool.ntp.org project.
# pool pool.ntp.org iburst (default before) #1 <======= comment this line

# agstr (add this line) see: https://www.ntppool.org/zone/asia
pool id.pool.ntp.org iburst #2 <======= add this line

# Record the rate at which the system clock gains/losses time.
driftfile /var/lib/chrony/drift

# Allow the system clock to be stepped in the first three updates
# if its offset is larger than 1 second.
makestep 1.0 3

# Enable kernel synchronization of the real-time clock (RTC).
rtcsync
```
- restart service: `sudo sv restart chronyd`
- finally done!

# install and set pipewire

```
sudo xbps-install -S pipewire libspa-bluetooth
sudo ln -s /etc/sv/pipewire /var/service/
sudo ln -s /etc/sv/pipewire-pulse /var/service/
sudo usermod -aG _pipewire,pulse,pulse-access $USER
sudo xbps-install xfce4-pulseaudio-plugin (optional in XFCE, and add it to xfce4-panel), it work also for pipewire
```

- reboot your session then login again
- check your pipewire is activated using `pactl`
- `pactl info`

# essential packages

```
sudo xbps-install git neovim xclip vlc
sudo xbps-install gpick libnotify-bin gpick ImageMagick # some binary dependencies
sudo xbps-install galculator maim
```

# for mounting?

```
sudo xbps-install -Rs ntfs-3g udisks2 gvfs mtpfs gvfs-mtp gvfs-gphoto2
```

# fonts

- Noto fonts:

```
sudo xbps-install -Rs noto-fonts-emoji noto-fonts-ttf noto-fonts-ttf-extra
```

- Microsoft fonts:

```
git clone https://github.com/void-linux/void-packages
cd void-packages
./xbps-src binary-bootstrap
echo "XBPS_ALLOW_RESTRICTED=yes" >> etc/conf
```

installation: 

```
./xbps-src pkg -f msttcorefonts
xi msttcorefonts
```

- Set better font for firefox

```
sudo ln -s /usr/share/fontconfig/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/
sudo xbps-reconfigure -f fontconfig
```

# Keybinding

```
sudo xbps-install sxhkd
```
