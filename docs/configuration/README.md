# Configuration options
The following settings can be specified at runtime using the `docker -e`
argument:

* `VNC_SERVER_PASSWORD`: Specifies the VNC server password. This is the password
that will be needed when connecting to x11vnc using a VNC viewer. If this is
not set, it defaults to no password.
* `XVFB_RESOLUTION`: Specifies the resolution to use for the Xvfb program. If
this is not set, it defaults to `1280x1024x24`.
* `XVFB_DISPLAY`: Specifies the X11 display value for the Xvfb program. If this
is not set, it defaults to `:1`.
* `XVFB_SCREEN`: Specifies the screen ID for the Xvfb program. If this is not
set, it defaults to `0`.
* `XVFB_TIMEOUT`: Specifies the Xvfb timeout value, which is how long it waits
to allow Xvfb to startup before timing out. If this is not set, it defaults
to `5` seconds.
