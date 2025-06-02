# openshift-mlflow

Experiment Tracking using MLFlow.

## Build image

Build + tag, push image

```bash
make podman-push-mlflow
```

## Deploy

Deploy to OpenShift

Create a secret, replace as necessary (see the `mlflow-dc-oauth.yaml` deployment if you need it, else unauthenticated)

```bash
export PROVIDER=""
export CLIENT_ID=""
export CLIENT_SECRET=""
export COOKIE_SECRET=""
export OIDC_ISSUER_URL=""
export ALLOWED_ROLE=""
export ARTIFACTS_DESTINATION="s3://mlflow-data"
export ENDPOINT_URL="http://minio.minio.svc.cluster.local:9000"
export AWS_ACCESS_KEY_ID="minio"
export AWS_SECRET_ACCESS_KEY="password"
export AWS_BUCKET_NAME="mlflow-data"
export POSTGRESQL_ADMIN_PASSWORD="password"
export POSTGRESQL_USER="postgres"
export POSTGRESQL_PASSWORD="password"
export POSTGRESQL_DATABASE="postgres"

oc new-project mlflow
cat chart/mlflow-secret.yaml | envsubst | oc apply -f-
```

Create mlflow from chart

```bash
helm template chart/mlflow | oc apply -f-
```
