# AsciiArtify

## Kubernetes Manifests

Created with https://github.com/sozercan/kubectl-ai

| NAME                    | PROMPT                   | DESCRIPTION                                                                      | EXAMPLE                                                 |
|-------------------------|--------------------------|----------------------------------------------------------------------------------|---------------------------------------------------------|
| app.yaml                | create application       | YAML config defines a Pod with a container using the "my-app-image" Docker image | [app.yaml](yaml/app.yaml)                               |
| app-livenessProbe.yaml  | create livenessProbe     | Defines a Pod with a container, liveness probe for health checking               | [app-livenessProbe.yaml](yaml/app-livenessProbe.yaml)   |
| app-readinessProbe.yaml | create readinessProbe    | Pod with container, readiness probe at "/health" on port 8080                    | [app-readinessProbe.yaml](yaml/app-readinessProbe.yaml) |
| app-volumeMounts.yaml   | create volumeMounts      | Pod with Nginx container, mounting an empty volume at "/data"                    | [app-volumeMounts.yaml](yaml/app-volumeMounts.yaml)     |
| app-cronjob.yaml        | create cronjob           | CronJob "my-cronjob" runs "my-container" echoing "Hello World!" every minute     | [app-cronjob.yaml](yaml/app-cronjob.yaml)               |
| app-job.yaml            | create job               | Job "my-job" runs "my-container" once with a non-restart policy                  | [app-job.yaml](yaml/app-job.yaml)                       |
| app-multicontainer.yaml | create multicontainer    | Pod "multicontainer-pod" with Nginx and Busybox containers, the latter sleeps    | [app-multicontainer.yaml](yaml/app-multicontainer.yaml) |
| app-resources.yaml      | create resources cpu ram | Defines ResourceQuota "cpu-ram-quota" limiting CPU to 1 and memory to 1Gi        | [app-resources.yaml](yaml/app-resources.yaml)           |
| app-secret-env.yaml     | create app-secret-env    | Secret "app-secret-env" with base64-encoded value for "MY_SECRET_KEY"            | [app-secret-env.yaml](yaml/app-secret-env.yaml)         |
