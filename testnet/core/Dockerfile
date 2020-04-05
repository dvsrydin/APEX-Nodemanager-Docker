FROM adoptopenjdk/openjdk12:jdk-12.0.2_10-slim

ARG     GRADLE_VERSION
ARG     CORE_VERSION
ARG     CORE_BRANCH
ARG     CONF_NAME

RUN     mkdir -p /apex
WORKDIR /apex

RUN     apt-get update -y && \
        apt-get install unzip -y && \
        apt-get install git -y && \
        apt-get install wget

RUN     cd /usr/local && \
        curl -L https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o gradle-${GRADLE_VERSION}-bin.zip && \
        unzip gradle-${GRADLE_VERSION}-bin.zip && \
        rm gradle-${GRADLE_VERSION}-bin.zip

ENV     GRADLE_HOME=/usr/local/gradle-${GRADLE_VERSION}
ENV     PATH=$PATH:$GRADLE_HOME/bin

RUN     cd /apex && \
        git clone https://github.com/APEX-Network/APEX-Blockchain-Core.git && \
        cd APEX-Blockchain-Core && \
        git checkout ${CORE_BRANCH} && \
        gradle shadowJar && \
        cp build/libs/APEX-Blockchain-Core-${CORE_VERSION}.jar /apex/apex-blockchain-core.jar

RUN     wget -O settings.conf https://github.com/APEX-Network/APEX-Nodemanager-Docker/blob/master/testnet/conffiles/${CONF_NAME}?raw=true

CMD     ["java", "-jar", "/apex/apex-blockchain-core.jar"]