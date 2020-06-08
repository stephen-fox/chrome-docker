# Chrome Docker (unmaintained)
A Docker image that can run Google Chrome.

Please note, this project is no longer maintained. I am currently focused on
other projects, and do not have the required time to support this. Pease feel
free to fork it.

Thank you for using it. I hope that it helped :)

## How does it work?
The Docker image includes a VNC server which provides graphical access to the
virtual display running in the container.

## How do I build it?
Refer to the [building documentation](docs/building).

## How do I run it?
First, start the container and its VNC server:
```
docker run -p 5900:5900 --name chrome --user apps --privileged <image-name>
```

**Note**: The macOS VNC client will not be able to login unless you set a
password for the VNC server. The instructions for setting a VNC password can be
found below.

By default, the VNC server is started without a password. If you would like to
specify a password for the VNC server, do the following:
```
docker run -p 5900:5900 -e VNC_SERVER_PASSWORD=some-password --name chrome \
    --user apps --privileged <image-name>
```

Once the container is running, you can VNC into it at `127.0.0.1` and run Chrome
from a terminal window by running:
```
google-chrome
```

You can also start Google Chrome by right-clicking the Desktop and selecting:
```
Applications > Network > Web Browsing > Google Chrome
```

## Additional settings
Refer to the [configuration documentation](docs/configuration).

## Security concerns
This image starts a X11 VNC server which spawns a framebuffer. Google Chrome
also requires that the image be run with the `--privileged` flag set. This flag
disables security labeling for the resulting container. Be very careful if you
run the container on a non-firewalled host.

Some applications (such as Google Chrome) will not run under the root user. A
non-root user named `apps` is included for such scenarios.
