# Cloud Function examples - hello Cloud Scheduler

## Create Pub/Sub

create Pub/Sub
```
gcloud pubsub topics create hello_cloud_scheduler
```

list topics
```
gcloud pubsub topics list
```

## Deploy Cloud Function

create Cloud Function, specify Pub/Sub topic.

```sh
gcloud functions deploy hello_cloud_scheduler \
  --runtime python38 \
  --trigger-topic hello_cloud_scheduler
```

```
$ gcloud functions list
```

## Run

set cron schedule

```
gcloud scheduler jobs create pubsub hello_cloud_scheduler \
  --schedule "*/5 * * * *" \
  --topic hello_cloud_scheduler \
  --message-body "Wiwi"
```

get logs

```
gcloud functions logs read hello_google_cloud_function_hello_cloud_scheduler --limit 50
```

get Pub/Sub messages

```
gcloud pubsub subscriptions pull cron-sub --limit 5
```
