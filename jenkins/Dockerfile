FROM jenkins/jenkins:lts

USER root

# ติดตั้ง Docker CLI และเครื่องมืออื่น ๆ
RUN apt-get update && apt-get install -y \
    docker.io \
    curl \
    gnupg \
    lsb-release \
    apt-transport-https \
    ca-certificates \
    software-properties-common

# ติดตั้ง Node.js v18 และ Firebase CLI
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs && \
    npm install -g firebase-tools

# ให้สิทธิ์ Jenkins รัน docker
RUN usermod -aG docker jenkins
RUN getent group docker || groupadd docker && usermod -aG docker jenkins

USER jenkins
