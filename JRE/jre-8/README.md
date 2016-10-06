Oracle JDK on Docker
====
This Dockerfile will take the JRE tar.gz file included in the folder and create an image on top of the latest Oracle Linux image

## Downloading required files
[Download](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) the desired JRE image for Oracle Linux (Linux x64) in the `.tar.gz` version and put it inside this `jre-8` folder.

## Modify Dockerfile as needed
In the `jre-8` directory, modify the Dockerfile to reflect the downloaded

## Build the image
Run the following commands to build the image, replacing <version> with the downloaded version:

```
$ docker build -t oracle/jre:<version>
```

Important: Proper version naming is crucial to maintaining a working Docker image repository. Using the above command and building an image for JRE version 8 update 102 (latest as of writing), the following command should be used to build the image:

```
$ docker build -t oracle/jre:8u102
```

After the image is built, you can verify the creation using `docker images` which should return an output similar to the following:

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
oracle/jre          8u102               cce84c1e7ea0        2 minutes ago       592.4 MB
oraclelinux         latest              1988eb5b3fc6        2 minutes ago       278.2 MB
```
