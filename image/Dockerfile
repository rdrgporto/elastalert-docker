# Alpine image
FROM alpine

# Docker labels
LABEL maintainer="https://github.com/rdrgporto" \
      description="Elastalert on Docker & Kubernetes"

# URL from which to download Elastalert
ENV ELASTALERT_URL https://github.com/Yelp/elastalert/archive/v0.1.39.zip
# Directory holding configuration for Elastalert and Supervisor
ENV CONFIG_DIR /opt/config
# Elastalert rules directory
ENV RULES_DIRECTORY /opt/rules
# Directory to which Elastalert and Supervisor logs are written
ENV LOG_DIR /opt/logs
# Elastalert home directory full path
ENV ELASTALERT_HOME /opt/elastalert
# Elastalert timezone
ENV TZ Europe/Madrid

# Move to /opt
WORKDIR /opt

# Install dependencies
RUN apk update && apk add \
  bzr \
  cvs \
  git \
  mercurial \
  ca-certificates \
  openssl-dev \
  libffi-dev \
  python2 \
  python2-dev \
  py2-pip \
  py2-yaml \
  gcc \
  musl-dev \
  tzdata \
  openntpd \
  libmagic \
  wget

# Download Elastalert
RUN wget -O elastalert.zip "${ELASTALERT_URL}" && \
  unzip elastalert.zip && \
  rm elastalert.zip && \
  mv e* "${ELASTALERT_HOME}"

# Move to Elastalert home
WORKDIR "${ELASTALERT_HOME}"

# Install dateutil & jira
# https://github.com/Yelp/elastalert/issues/1603
# https://github.com/Yelp/elastalert/issues
RUN pip install \
    python-dateutil==2.6.1 \
    jira==1.0.15

# Install Elastalert.
RUN python setup.py install && \
  pip install -e . && \
  pip uninstall twilio --yes && \
  pip install twilio==6.0.0

# Install Supervisor.
RUN easy_install supervisor

# Create directories. The /var/empty directory is used by openntpd.
RUN mkdir -p \
  "${CONFIG_DIR}" \
  "${RULES_DIRECTORY}" \
  "${LOG_DIR}" \
  /var/empty

# Clean up.
RUN apk del \
  python2-dev \
  musl-dev \
  gcc \
  openssl-dev \
  libffi-dev

# Clean cache
RUN rm -rf /var/cache/apk/*

# Define mount points.
VOLUME [ "${CONFIG_DIR}", "${RULES_DIRECTORY}", "${LOG_DIR}"]

# Copy configuration files and rule example
COPY config/elastalert_config.yaml ${CONFIG_DIR}
COPY config/elastalert_supervisord.conf ${CONFIG_DIR}
COPY rules/example-rule.yaml ${RULES_DIRECTORY}

# Start Elastalert
CMD ["/usr/bin/supervisord","-c","/opt/config/elastalert_supervisord.conf","-n"]