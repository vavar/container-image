FROM jenkins/jenkins:2.277.3
USER root
COPY ./ca.crt /usr/share/ca-certificates
RUN keytool -keystore $JAVA_HOME/jre/lib/security/cacerts -importcert -file /usr/share/ca-certificates/ca.crt -alias ca \
        -noprompt -storepass changeit \
    && echo "ca.crt" | tee -a /etc/ca-certificates.conf \
    && update-ca-certificates

USER jenkins
RUN jenkins-plugin-cli --plugins kubernetes \ 
    workflow-aggregator git configuration-as-code greenballs \
    gitlab-branch-source gitlab-logo pipeline-utility-steps \
    ansicolor matrix-auth authorize-project ws-cleanup job-dsl
