# Raspberry Pi as Digital Signage

**Note:** I do not claim to be a Linux expert, so some of these may not be the "proper" way of doing things, but they worked for me in a digital signage type project.

1) Make sure the pi automatically launches the DE. It may be beneficial to have it automatically log in on boot as well. You can do that via `sudo raspi-config` and following the graphical prompts.
2) To hide the mouse cursor after a period of time, you'll need the `unclutter` package: `sudo apt-get install unclutter`
3) Disable the automatic screen blanking due to input inactivity. [This HackLAB article](https://www.geeks3d.com/hacklab/20160108/how-to-disable-the-blank-screen-on-raspberry-pi-raspbian/) provides a few ways to do this depending on the version of raspbian you're running.
4) If you're planning on running the server locally, of course you'll need to install and configure that.
5) Configure `unclutter` to run when the user logs in to the desktop. Put the following desktop launcher (`unclutter.desktop`) in `~/.config/autostart` to hide the mouse pointer after one second of inactivity:

```
[Desktop Entry]
Type=Application
Name=Unclutter
Exec=/bin/bash unclutter -idle 1
```

6) Configure chromium to auto launch in kiosk mode to wherever you're hosting the web page. To do that after a ten second delay, put this `kiosk.desktop` in the same `~/.config/autostart` directory:

```
[Desktop Entry]
Type=Application
Name=Calendar Display
Exec=/bin/bash -c "sleep 10s && chromium-browser --kiosk http://yourserver.com"
```

7) I also installed [This Chrome Extension](https://chrome.google.com/webstore/detail/autorefresh-on-error/cacnfebiodkggmdjhecdkendmeimjioa) that my University's IT uses for their digital signage to automatically refresh the browser after one minute should anything but a `200 OK` status be received.

