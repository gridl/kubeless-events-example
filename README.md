# kubeless-events-example

A repo containing examples of how to manage kubernetes events with kubeless

This repo is designed to accompany [this]() blog post, explaining the thought process and how it works

# Running Locally

The events pipeline can be run locally, assuming you have a NATS cluster deployed to your cluster:

```
kubectl port-forward svc/nats-cluster 4222:4222 -n nats-io
python events.py -a localhost:4222
```

# Docker Image

A docker image for the event publishing code has been pushed to `jaxxstorm/kubernetes-events:latest`. You can run this using the manifest in the manifests directory.

# Kubeless Function

To run the Kubeless function, use the kubeless CLI and set the environment variables like so:

```
kubeless function deploy slack --runtime python3.6 --handler slack.slack_message --from-file functions/slack.py -n kubeless --env SLACK_TOKEN=<xoxb-token> --env SLACK_CHANNEL=<channel> --dependencies functions/requirements.txt
```
