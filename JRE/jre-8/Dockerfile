#
# This Dockerfile will create an image including a JRE using a downloaded .tar.gz in the same directory as this Dockerfile.
# Requires latest Oracle Linux image (from public repository)
#

# Build from the latest Oracle Linux public image
FROM oraclelinux:latest

# Maintained by Ryan O'Hare, Manager at Accenture specializing in Oracle Technology
MAINTAINER Ryan O'Hare <ryan.ohare@accenture.com>

# Set required environment variables
# Note: update the JAVA_PKG variable to match the downloaded JRE .tar.gz filename
ENV JAVA_PKG=server-jre-8u102-linux-x64.tar.gz \
    JAVA_HOME=/usr/java/default \
    PATH=$PATH:/usr/java/default/bin

# Add the JAVA_PKG file to the container in /usr/java location
# NOTE: The ADD command also unzips the .tar.gz file to this location
ADD $JAVA_PKG /usr/java

# Move the unzipped JRE to the JAVA_HOME location in the container
RUN mv $(ls -1 -d /usr/java/*) $JAVA_HOME && \
    echo "JRE successfully installed - contents of $JAVA_HOME:" && \
    ls $JAVA_HOME
