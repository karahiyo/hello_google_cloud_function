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

## Test

```
gcloud functions call hello_cloud_scheduler --data='{}'
```

## Run

set cron schedule

```
gcloud scheduler jobs create pubsub hello_cloud_scheduler_cron \
  --schedule "*/5 * * * *" \
  --topic hello_cloud_scheduler \
  --message-body "Wiwi"
```

list scheduler resources
```
$ gcloud scheduler jobs list
ID                          LOCATION     SCHEDULE (TZ)          TARGET_TYPE  STATE
hello_cloud_scheduler_cron  us-central1  */5 * * * * (Etc/UTC)  Pub/Sub      ENABLED
```

describe scheduler resource
```
gcloud scheduler jobs describe hello_cloud_scheduler_cron
```

get logs

```
gcloud functions logs read hello_cloud_scheduler --limit 50
```

## Clean up

pause job
```
$ gcloud scheduler jobs pause hello_cloud_scheduler_cron
Job has been paused.
```
