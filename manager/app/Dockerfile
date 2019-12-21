FROM adoptopenjdk/openjdk12:jdk-12.0.1_12-slim

ARG     GRADLE_VERSION
ARG     APP_PORT
ARG     CORE_PORT

RUN     apt-get update -y && \
        apt-get install unzip -y && \
        apt-get install git -y && \
        apt-get install maven -y && \
        apt-get install wget -y

RUN     cd /usr/local && \
        curl -L https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o gradle-${GRADLE_VERSION}-bin.zip && \
        unzip gradle-${GRADLE_VERSION}-bin.zip && \
        rm gradle-${GRADLE_VERSION}-bin.zip

ENV     GRADLE_HOME=/usr/local/gradle-${GRADLE_VERSION}
ENV     PATH=$PATH:$GRADLE_HOME/bin

RUN     cd /root && \
        git clone https://github.com/APEX-Network/APEX-Nodemanager.git && \
        git clone https://github.com/APEX-Network/APEX-Blockchain-Core.git

WORKDIR "/root/APEX-Nodemanager"

CMD ["mvn", "spring-boot:run"]