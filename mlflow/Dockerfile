FROM registry.access.redhat.com/ubi9/python-39:9.6-1747332104

ARG MLFLOW_VERSION="2.22.0"
#ADD pip.conf /etc/.

USER 1001

RUN pip install --upgrade pip
RUN pip install mlflow==$MLFLOW_VERSION
RUN pip install boto3
RUN pip install psycopg2-binary
RUN pip install certifi

USER root
#COPY cacerts.pem /opt/app-root/lib64/python3.8/site-packages/certifi/cacert.pem
#RUN chown 1001:1001 /opt/app-root/lib64/python3.8/site-packages/certifi/cacert.pem

USER 1001

ENV MLFLOW_HOME="/opt/app-root" \
    APP_VERSION=$MLFLOW_VERSION \
    APP_NAME="mlflow" \
    LANG="en_US.UTF-8" \
    LANGUAGE="en_US:en"
