# .NET Core Docker

[![](https://images.microbadger.com/badges/version/qqbuby/dotnet:2.2-sdk-clouderaimpalaodbc.svg)](https://microbadger.com/images/qqbuby/dotnet:2.2-sdk-clouderaimpalaodbc "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/qqbuby/dotnet:2.2-sdk-clouderaimpalaodbc.svg)](https://microbadger.com/images/qqbuby/dotnet:2.2-sdk-clouderaimpalaodbc "Get your own image badge on microbadger.com")

[![](https://images.microbadger.com/badges/version/qqbuby/dotnet:2.2-aspnetcore-runtime-clouderaimpalaodbc.svg)](https://microbadger.com/images/qqbuby/dotnet:2.2-aspnetcore-runtime-clouderaimpalaodbc "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/qqbuby/dotnet:2.2-aspnetcore-runtime-clouderaimpalaodbc.svg)](https://microbadger.com/images/qqbuby/dotnet:2.2-aspnetcore-runtime-clouderaimpalaodbc "Get your own image badge on microbadger.com")

```dockerfile
FROM microsoft/dotnet:2.2-aspnetcore-runtime
LABEL maintainer="ROY <qqbuby@gmail.com>"

# set up krb5, unixodbc
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        unixodbc \
        krb5-user \
    && rm -rf /var/lib/apt/lists/*

# set up impala odbc connector for cloudea 
ENV IMPALA_ODBC_CONNECTOR_VERSION 2.6.0.1000
ENV IMPALA_ODBC_CONNECTOR_RELEASE 2
ENV IMPALA_ODBC_CONNECTOR_DOWNLOAD_URL https://downloads.cloudera.com/connectors/impala_odbc_${IMPALA_ODBC_CONNECTOR_VERSION}/Debian/clouderaimpalaodbc_${IMPALA_ODBC_CONNECTOR_VERSION}-${IMPALA_ODBC_CONNECTOR_RELEASE}_amd64.deb

RUN curl -sSL "$IMPALA_ODBC_CONNECTOR_DOWNLOAD_URL" -o clouderaimpalaodbc.deb \
    && dpkg -i clouderaimpalaodbc.deb \
    && rm clouderaimpalaodbc.deb

COPY ./files/odbcinst.ini /etc/odbcinst.ini
COPY ./files/cloudera.impalaodbc.ini /opt/cloudera/impalaodbc/lib/64/cloudera.impalaodbc.ini
```
