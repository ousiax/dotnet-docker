FROM mcr.microsoft.com/dotnet/sdk:6.0
LABEL maintainer="ROY <qqbuby@gmail.com>"

# set java runtime environemnt
RUN mkdir -p mkdir -p /usr/share/man/man1 \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        openjdk-11-jre-headless \
    && rm -rf /var/lib/apt/lists/*

# set dotnet global tool dotnet-sonarscanner
RUN dotnet tool install dotnet-sonarscanner --tool-path "/usr/local/bin"
