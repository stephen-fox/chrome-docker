# Chrome Docker
## What is it?
A Docker image that can run Google Chrome.

## How does it work?
The Docker image includes a VNC server which provides graphical access to the
virtual display running in the container.

## How do I run it?
First, start the container and its VNC server:
```
docker run -p 5900:5900 --user apps --privileged <image-name>
```

**Note**: The macOS VNC client will not be able to login unless you set a
password for the VNC server. The instructions for setting a VNC password can be
found below.

By default, the VNC server is started without a password. If you would like to
specify a password for the VNC server, do the following:
```
docker run -p 5900:5900 -e VNC_SERVER_PASSWORD=some-password --user apps --privileged <image-name>
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

## Running as a non-root user
Some applications (such as Google Chrome) will not run under the root user. A
non-root user named `apps` is included for such scenarios.

## Additional settings
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

## Security concerns
This image starts a X11 VNC server which spawns a framebuffer. Google Chrome
also requires that the image be run with the `--privileged` flag set. This flag
disables security labeling for the resulting container. Be very careful if you
run the container on a non-firewalled host.

## How do I build it?
An included `Gradle` project orchestrates the creation of the Docker image. You
can interact with the project using the included Gradle wrapper (`gradlew`)
script. If you do not want to use Gradle, you can also use the standard `docker
 build` command.

### Required dependencies
The following dependencies are required to build the image:
1. [Docker](https://docs.docker.com/engine/installation/)
2. [Java](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)
    (+) Only required if you want to use Gradle to build the image

### Build command
**Note**: In the future, additional operating systems may be supported. Please
use the following documentation for reference.

To build the build environment image, execute the following:
```
./gradlew buildImage
```

### How do I push it to a registry?
To build and push the image to a Docker registry, execute the following:
```
./gradlew pushImage -PexternalVersion=1.0.0
```
By default, Gradle deploys to the registry specified in `gradle.properties`.
You can change this value in the properties file, or specify it on the command
line using `-PdeployRepoUrl=some.other.place:5000`
