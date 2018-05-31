FROM microsoft/dotnet:2.1-sdk
LABEL maintainer="ROY <qqbuby@gmail.com>"

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

RUN curl -sSL https://downloads.cloudera.com/connectors/impala_odbc_2.5.40.1025/Debian/clouderaimpalaodbc_2.5.40.1025-2_amd64.deb \
        -o /tmp/clouderaimpalaodbc_2.5.40.1025-2_amd64.deb \
    && dpkg -i /tmp/clouderaimpalaodbc_2.5.40.1025-2_amd64.deb \
    && rm /tmp/clouderaimpalaodbc_2.5.40.1025-2_amd64.deb

COPY ./files/cloudera.impalaodbc.ini /opt/cloudera/impalaodbc/lib/64/cloudera.impalaodbc.ini
COPY ./files/odbcinst.ini /etc/odbcinst.ini
