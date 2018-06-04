FROM microsoft/dotnet:2.1-sdk
LABEL maintainer="ROY <qqbuby@gmail.com>"

# set up node
ENV NODE_VERSION 8.11.2
ENV NODE_DOWNLOAD_SHA 67dc4c06a58d4b23c5378325ad7e0a2ec482b48cea802252b99ebe8538a3ab79
ENV NODE_DOWNLOAD_URL https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz

RUN curl -sSL "$NODE_DOWNLOAD_URL" -o nodejs.tar.gz \
    && echo "$NODE_DOWNLOAD_SHA nodejs.tar.gz" | sha256sum -c - \
    && tar -xzf "nodejs.tar.gz" -C /usr/local --strip-components=1 \
    && rm nodejs.tar.gz \
&& ln -s /usr/local/bin/node /usr/local/bin/nodejs

# set up yarn, krb5, unixodbc
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        apt-transport-https \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        krb5-user \
        unixodbc \
        unixodbc-dev \
        yarn \
    && rm -rf /var/lib/apt/lists/*

# set up impala odbc connector for cloudea 
ENV IMPALA_ODBC_CONNECTOR_VERSION 2.5.42.1031
ENV IMPALA_ODBC_CONNECTOR_DOWNLOAD_URL https://downloads.cloudera.com/connectors/impala_odbc_$IMPALA_ODBC_CONNECTOR_VERSION/Debian/clouderaimpalaodbc_$IMPALA_ODBC_CONNECTOR_VERSION-2_amd64.deb

RUN curl -sSL "$IMPALA_ODBC_CONNECTOR_DOWNLOAD_URL" -o $clouderaimpalaodbc.deb \
    && dpkg -i clouderaimpalaodbc.deb \
    && rm clouderaimpalaodbc.deb

COPY ./files/cloudera.impalaodbc.ini /opt/cloudera/impalaodbc/lib/64/cloudera.impalaodbc.ini
COPY ./files/odbcinst.ini /etc/odbcinst.ini
