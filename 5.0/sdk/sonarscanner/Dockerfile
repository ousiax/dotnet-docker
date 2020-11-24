FROM mcr.microsoft.com/dotnet/core/sdk:5.0
LABEL maintainer="ROY <qqbuby@gmail.com>"

# set java runtime environemnt
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        openjdk-11-jre-headless \
    && rm -rf /var/lib/apt/lists/*

# set dotnet global tool dotnet-sonarscanner
RUN dotnet tool install dotnet-sonarscanner --tool-path "/usr/local/bin"
