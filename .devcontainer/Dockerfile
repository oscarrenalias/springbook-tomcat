# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.140.1/containers/java/.devcontainer/base.Dockerfile

# [Choice] Java version: 11, 14
ARG VARIANT="14"
FROM mcr.microsoft.com/vscode/devcontainers/java:0-${VARIANT}

# [Option] Install Maven
ARG INSTALL_MAVEN="false"
ARG MAVEN_VERSION=""

# [Option] Install Gradle
ARG INSTALL_GRADLE="false"
ARG GRADLE_VERSION=""
RUN if [ "${INSTALL_MAVEN}" = "true" ]; then su vscode -c "source /usr/local/sdkman/bin/sdkman-init.sh && sdk install maven \"${MAVEN_VERSION}\""; fi \
    && if [ "${INSTALL_GRADLE}" = "true" ]; then su vscode -c "source /usr/local/sdkman/bin/sdkman-init.sh && sdk install gradle \"${GRADLE_VERSION}\""; fi

# [Option] Install Node.js
ARG INSTALL_NODE="false"
ARG NODE_VERSION="lts/*"
RUN if [ "${INSTALL_NODE}" = "true" ]; then su vscode -c "source /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# Install Tomcat
# https://mirror-2.hosthink.net/apache/tomcat/tomcat-9/v9.0.41/bin/apache-tomcat-9.0.41.zip
ARG INSTALL_TOMCAT="true"
ARG TOMCAT_VERSION="9.0.41"
#RUN if [ "${INSTALL_TOMCAT}" = "true" ]; then "cd /tmp && wget https://www.nic.funet.fi/pub/mirrors/apache.org/tomcat/tomcat-9/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.zip && unzip /tmp/apache-tomcat-${TOMCAT_VERSION}.zip -d /opt && ln -s /opt/apache-tomcat-${TOMCAT_VERSION} /opt/apache-tomcat"; fi 
RUN if [ "${INSTALL_TOMCAT}" = "true" ]; then su vscode -c "cd /tmp && wget https://www.nic.funet.fi/pub/mirrors/apache.org/tomcat/tomcat-9/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.zip && sudo unzip /tmp/apache-tomcat-${TOMCAT_VERSION}.zip -d /opt && sudo ln -s /opt/apache-tomcat-${TOMCAT_VERSION} /opt/apache-tomcat"; fi 

# Install PostgreSQL
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends postgresql-11

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1