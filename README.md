# srtp-aks-deploy
This repo will be used to deploy all the SRTP services. It has a single pipeline where users can choose the environment and the service to deploy.
We have 3 environments under helm dir:
  - DEV
  - UAT
  - PROD

How can I add a new repo/service to deploy?

To add a repo, you need to create a dir under the environment where you want to deploy the service (e.g. rtp-ms-name) 

In this directory, you have to add a basic config file Chart.yaml

```yaml
apiVersion: v2
name: my-microservice
description: My microservice description
type: application
version: 1.0.0
appVersion: 1.0.0
dependencies:
- name: microservice-chart
  version: 7.1.1
  repository: "https://pagopa.github.io/aks-microservice-chart-blueprint"
```

After that, you must use this command to create the Chart.lock
```bash
helm dep build
```
It also creates a "charts" dir, you can delete it or you can leave it anyway this is included inside the gitignore file.

Now you have to add the values.yaml file with the values of your interest. You can check the other values files.

As the last thing you have to add a deploy.sh file with inside:

```bash
#!/bin/bash

../../../scripts/deploy.sh values.yaml <namespace> <aks-name> <service-name>
```

You have to do this stuff for each environment you need!