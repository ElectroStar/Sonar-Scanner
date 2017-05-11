FROM java:alpine  
ENV SONAR_SCANNER_VERSION 3.0.2.768

RUN apk add --no-cache wget && \  
    wget https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}.zip && \  
    unzip sonar-scanner-cli-${SONAR_SCANNER_VERSION} && \  
    cd /usr/bin && ln -s /sonar-scanner-${SONAR_SCANNER_VERSION}/bin/sonar-scanner sonar-scanner && \  
    apk del wget
