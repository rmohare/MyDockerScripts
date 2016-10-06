#Creating Weblogic Docker Image
====
The Dockerfile in this directory will install Weblogic binaries

This install is based on the QuickStart version of Weblogic. This should be used for PoCs and local development only.

## Downloading required files
[Download](http://www.oracle.com/technetwork/middleware/weblogic/downloads/wls-main-097127.html) the desired Weblogic QuickStart install ZIP file to the `QuickStart` folder. (Look for "Quick Installer intended for Oracle WebLogic Server and Oracle Coherence development only" on the download page to get the right file.). The filename downloaded should be in the format `fmw_<version>_wls_quick_Disk1_1of1.zip`.

## Modify the Dockerfile as needed
At the time of script writing, the latest Weblogic version was 12.2.1.1, so the Dockerfile is set up to use that version. In order to build the version of Weblogic that has been downloaded, you must update the FMW_PKG and FMW_JAR environment variables to match the version you have downloaded.

## Build the image
Run the following commands, replacing <repository> with your own repository name and <version> with the version of Weblogic that you downloaded:

```
$ docker build -t <repository>/wls:<version> .
```

Important: Proper version naming is crucial to maintaining a working Docker image repository. Using the above command and building an image for Weblogic 12.2.1.1 (latest as of writing), the following command should be used to build the image:

```
$ docker build -t rmohare/wls:12.2.1.1 .
```

After the image is built, you can verify the creation using `docker images` which should return an output similar to the following (Image IDs masked for security):

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
rmohare/wls         12.2.1.1            xxxxxxxxxxxx        13 minutes ago      1.446 GB
rmohare/jre         8u102               xxxxxxxxxxxx        50 minutes ago      592.4 MB
oraclelinux         latest              xxxxxxxxxxxx        11 weeks ago        278.2 MB
```

## Using public Docker image
Coming soon!
