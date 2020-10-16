# Cloud Function examples - hello pubsub

## Create Pub/Sub topic

```
gcloud pubsub topics create hello_google_cloud_function_hello_pubsub
```

## Deploy

```sh
gcloud functions deploy hello_pubsub \
  --runtime python38 \
  --trigger-topic hello_google_cloud_function_hello_pubsub
```

```
gcloud functions list
NAME          STATUS  TRIGGER        REGION
hello_pubsub  ACTIVE  Event Trigger  us-central1
```

## Test

publish message

```
gcloud pubsub topics publish hello_google_cloud_function_hello_pubsub --message YOUR_NAME
```

get logs

```
gcloud functions logs read hello_google_cloud_function_hello_pubsub --limit 50
```
