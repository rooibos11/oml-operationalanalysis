
FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

# 必要なツールをインストール
RUN apt-get update && apt-get install -y \
    curl wget unzip git \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Java 21をインストール（OpenJDK）
RUN apt-get update && apt-get install -y openjdk-21-jdk \
    && java -version

# 環境変数設定
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH

