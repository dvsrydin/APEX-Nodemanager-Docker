FROM    adoptopenjdk/openjdk12:jdk-12.0.2_10-slim

ARG     GRADLE_VERSION
ARG     APP_PORT
ARG     CONF_NAME
ENV     APP_PORT ${APP_PORT}

RUN     apt-get update -y &&\
        apt-get install unzip -y &&\
        apt-get install git -y &&\
        apt-get install maven -y &&\
        apt-get install wget -y

RUN     cd /usr/local &&\
        curl -L https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o gradle-${GRADLE_VERSION}-bin.zip &&\
        unzip gradle-${GRADLE_VERSION}-bin.zip &&\
        rm gradle-${GRADLE_VERSION}-bin.zip

ENV     GRADLE_HOME=/usr/local/gradle-${GRADLE_VERSION}
ENV     PATH=$PATH:$GRADLE_HOME/bin

WORKDIR /root

RUN     git clone https://github.com/APEX-Network/APEX-Nodemanager.git &&\
        git clone https://github.com/APEX-Network/APEX-Blockchain-Core.git

RUN     wget -O settings.conf https://github.com/APEX-Network/APEX-Nodemanager-Docker/blob/master/testnet/conffiles/${CONF_NAME}?raw=true

CMD     mvn -f APEX-Nodemanager spring-boot:run -Dspring-boot.run.arguments=--server.port=${APP_PORT}