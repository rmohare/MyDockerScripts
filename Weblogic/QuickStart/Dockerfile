#
# This Dockerfile will install Weblogic on top of Oracle Linux with JRE installed
# Note: this is a Weblogic binary installation only, no domain will be created
#
# (This Dockerfile has been been built using oracle/docker-images as the starting point)
#

# Use JRE image (which pulls oraclelinux:latest)
# NOTE: Update to reflect the image to use
FROM rmohare/jre:8u102

# Maintained by Ryan O'Hare, Manager at Accenture specializing in Oracle Technology
MAINTAINER Ryan O'Hare <ryan.ohare@accenture.com>

# Set environment variables
# NOTE: Update the FMW_PKG and FMW_JAR (the .jar file inside the FMW_PKG .zip file) to reflect the name of the downloaded version
ENV FMW_PKG=fmw_12.2.1.1.0_wls_quick_Disk1_1of1.zip \
    FMW_JAR=fmw_12.2.1.1.0_wls_quick.jar \
    ORACLE_HOME=/u01/oracle \
    USER_MEM_ARGS="-Djava.security.egd=file:/dev/./urandom" \
    DEBUG_FLAG=true\
    PRODUCTION_MODE=dev\
    PATH=$PATH:/u01/oracle/oracle_common/common/bin

# Copy the install package .zip and the associated install.file, oraInst.loc to the container in /u01/
COPY $FMW_PKG install.file oraInst.loc /u01/

# Create the needed users/groups
RUN chmod a+xr /u01 && \
    useradd -b /u01 -m -s /bin/bash oracle && \
    echo oracle:oracle | chpasswd && \
    # extract contents of the FMW_PKG
    cd /u01 && $JAVA_HOME/bin/jar xf /u01/$FMW_PKG && cd - && \
    # Switch user to oracle and run the install from command line
    # Note: $JAVA_HOME is set by the oracle/jre:<version> image
    # -force and -novalidation eliminate user inputs required in the install
    su -c "$JAVA_HOME/bin/java -jar /u01/$FMW_JAR -invPtrLoc /u01/oraInst.loc -jreLoc $JAVA_HOME -ignoreSysPrereqs -force -novalidation ORACLE_HOME=$ORACLE_HOME" - oracle && \
    # change ownership of the /u01 folder and contents to oracle:oracle
    chown oracle:oracle -R /u01 && \
    # cleanup
    rm /u01/$FMW_JAR /u01/$FMW_PKG /u01/oraInst.loc /u01/install.file

# Change user to oracle user and set working directory
USER oracle
WORKDIR $ORACLE_HOME

# Define default command to start bash
CMD ["bash"]
