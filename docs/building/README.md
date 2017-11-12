# Build documentation
An included `Gradle` project orchestrates the creation of the Docker image. You
can interact with the project using the included Gradle wrapper (`gradlew`)
script. If you do not want to use Gradle, you can also use the standard `docker
build` command.

## Building with `docker` command line
Execute the following on the command line:
```
cd <repository-path>/image
docker build -t local/chrome:0.0.1 .
```

## Building with Gradle

#### Required dependencies
The following dependencies are required to build the image:
1. [Docker](https://docs.docker.com/engine/installation/)
2. [Java](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)
    (+) Only required if you want to use Gradle to build the image

#### Build command
**Note**: In the future, additional operating systems may be supported. Please
use the following documentation for reference.

To build the build environment image, execute the following:
```
./gradlew buildImage
```
