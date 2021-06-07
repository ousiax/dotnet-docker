FROM mcr.microsoft.com/dotnet/aspnet:5.0
LABEL maintainer="ROY <qqbuby@gmail.com>"

# set curl
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        curl \
    && rm -rf /var/lib/apt/lists/*

# set up impala odbc connector for cloudea
ENV IMPALA_ODBC_CONNECTOR_VERSION 2.6.5.1005
ENV IMPALA_ODBC_CONNECTOR_RELEASE 2
ENV IMPALA_ODBC_CONNECTOR_DOWNLOAD_URL https://downloads.cloudera.com/connectors/ClouderaImpala_ODBC_${IMPALA_ODBC_CONNECTOR_VERSION}/Debian/clouderaimpalaodbc_${IMPALA_ODBC_CONNECTOR_VERSION}-${IMPALA_ODBC_CONNECTOR_RELEASE}_amd64.deb

RUN curl -sSL "$IMPALA_ODBC_CONNECTOR_DOWNLOAD_URL" -o /tmp/clouderaimpalaodbc.deb

FROM mcr.microsoft.com/dotnet/aspnet:5.0
LABEL maintainer="ROY <qqbuby@gmail.com>"

# set up krb5, unixodbc
ENV KRB5_USER_VERSION=1.17-3+deb10u1
ENV UNIXODBC_VERSION=2.3.6-0.1
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        krb5-user=${KRB5_USER_VERSION} \
        unixodbc=${UNIXODBC_VERSION} \
    && rm -rf /var/lib/apt/lists/*

COPY --from=0 /tmp/clouderaimpalaodbc.deb .

RUN dpkg -i clouderaimpalaodbc.deb \
    && rm clouderaimpalaodbc.deb

COPY ./files/odbcinst.ini /etc/odbcinst.ini
COPY ./files/cloudera.impalaodbc.ini /opt/cloudera/impalaodbc/lib/64/cloudera.impalaodbc.ini
