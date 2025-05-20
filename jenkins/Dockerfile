FROM jenkins/jenkins:lts-jdk17

USER root

ARG DOCKER_GID=999  # แก้เป็น GID docker group บน host

RUN apt-get update && apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list && \
    apt-get update && apt-get install -y docker-ce-cli docker-compose-plugin

RUN groupadd -g ${DOCKER_GID} docker || true && \
    usermod -aG docker jenkins

USER jenkins
