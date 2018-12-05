FROM microsoft/dotnet:2.2-sdk
LABEL maintainer="ROY <qqbuby@gmail.com>"

# set java runtime environemnt
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        openjdk-8-jre-headless \
    && rm -rf /var/lib/apt/lists/*

# set dotnet global tool dotnet-sonarscanner
RUN dotnet tool install dotnet-sonarscanner --tool-path "/usr/local/bin"
