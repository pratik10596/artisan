#
#  Onix Config Manager - SonarQube Scanner Artisan Package Runtime Image
#  Copyright (c) 2018-2021 by www.gatblau.org
#  Licensed under the Apache License, Version 2.0 at http://www.apache.org/licenses/LICENSE-2.0
#
#  Contributors to this project, hereby assign copyright in this code to the project,
#  to be licensed under the same terms as the rest of the code.
#
FROM alpine as builder

ENV SONAR_ZIP_FILE=sonar-scanner-cli-3.3.0.1492-linux.zip
ENV SONAR_FOLDER=sonar-scanner-3.3.0.1492-linux

WORKDIR /app/

RUN apk add zip && \
    wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/${SONAR_ZIP_FILE} && \
    unzip ${SONAR_ZIP_FILE} && \
    mv ${SONAR_FOLDER} /sonar && \
    rm ${SONAR_ZIP_FILE}

FROM quay.io/artisan/ubi-min

ARG UNAME=runtime

ENV PATH $PATH:/sonar/bin

WORKDIR /app/

COPY --from=builder /sonar /sonar
COPY run.sh /app/

RUN chmod -R a+rwx /app/ && chmod -R a+rwx /sonar/

USER $UNAME
