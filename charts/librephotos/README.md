# librephotos

![Version: 0.202215.2](https://img.shields.io/badge/Version-0.202215.2-informational?style=flat-square) ![AppVersion: 2022w15](https://img.shields.io/badge/AppVersion-2022w15-informational?style=flat-square)

Helmchart used to install Librephotos in a microservice manner

**Homepage:** <https://github.com/varet80/publiccharts/tree/main/charts/librephotos>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Vassilis Aretakis |  | <https://github.com/varet80> |

## Source Code

* <https://github.com/LibrePhotos/librephotos>
* <https://hub.docker.com/r/reallibrephotos>

## Requirements

Kubernetes: `>=1.21.0-0`

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | postgresql | => 11.0.0 |
| https://charts.bitnami.com/bitnami | redis | => 16.0.0 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| backend | object | `{"annotations":{},"env":{"ALLOW_UPLOAD":"false","DB_BACKEND":"postgresql","DEBUG":"0","HEAVYWEIGHT_PROCESS":"2","SKIP_PATTERNS":"","WEB_CONCURRENCY":"4"},"envTemplates":{"dbName":"{{ .Values.postgresql.auth.database }}","dbPort":"{{ .Values.postgresql.containerPorts.postgresql }}","dbUser":"{{ .Values.postgresql.auth.database }}","redisPort":"{{ .Values.redis.master.containerPorts.redis }}"},"healthchecks":{"livenessProbe":{"failureThreshold":5,"initialDelaySeconds":10,"periodSeconds":120,"tcpSocket":{"port":8001},"timeoutSeconds":5},"readinessProbe":{"failureThreshold":5,"initialDelaySeconds":10,"periodSeconds":120,"tcpSocket":{"port":8001},"timeoutSeconds":5},"startupProbe":{"failureThreshold":60,"initialDelaySeconds":10,"periodSeconds":5,"tcpSocket":{"port":8001},"timeoutSeconds":2}},"image":{"repository":"reallibrephotos/librephotos"},"replicaCount":1,"resources":{"limits":{"memory":"8Gi"},"requests":{"cpu":"10m","memory":"50Mi"}}}` | Configurationf or the Backend services |
| backend.annotations | object | `{}` | Annotations |
| backend.envTemplates.dbName | string | `"{{ .Values.postgresql.auth.database }}"` | Postgresql DB Name |
| backend.envTemplates.dbPort | string | `"{{ .Values.postgresql.containerPorts.postgresql }}"` | Postgresql DB port |
| backend.envTemplates.dbUser | string | `"{{ .Values.postgresql.auth.database }}"` | Postgresql DB password |
| backend.envTemplates.redisPort | string | `"{{ .Values.redis.master.containerPorts.redis }}"` | redis port retrieved by parent helm chart |
| backend.image.repository | string | `"reallibrephotos/librephotos"` | Repository and image name |
| backend.replicaCount | int | `1` | Replica counts |
| cronjob.native.concurrencyPolicy | string | `"Forbid"` | concurrency policy, Forbid as default, to avoid running two scans |
| cronjob.native.failedJobsHistoryLimit | int | `10` | keep 10 jobs for log parsing (if they fail |
| cronjob.native.image.imagePullPolicy | string | `"IfNotPresent"` |  |
| cronjob.native.image.kubernetesVersion | string | `"1.22.6"` | Check alpine image for the latest available https://hub.docker.com/r/alpine/k8s/tags |
| cronjob.native.schedule | string | `"0 * * * *"` | Cronjob schedule |
| cronjob.native.successfulJobHistoryLimit | int | `5` | keep 5 successful jobs for log parsing. |
| cronjob.native.suspend | bool | `true` | suspension is enabled, to avoid scheduling waiting jobs while scan takes hours! |
| cronjob.type | string | `"native"` | Create a native kubernetes cronjob, using roles to access kubernetes exec and execute the python through a third party container. This is an Antipattern! but the only way, till another exists |
| dataVolume.accessModes | list | `["ReadWriteOnce"]` | Access mode of volume |
| dataVolume.size | string | `"100Gi"` | Size of the volume to be created (data) |
| dataVolume.stroageClass | string | `""` | Storage class of data volume |
| extraVolumeMounts | string | `nil` | You can define extra volume mounts, in the typical K8s syntax (Only in backend) |
| extraVolumes | string | `nil` | You can define extra volumes, in the typical K8s syntax (Only in backend) |
| frontend.annotations | object | `{}` |  |
| frontend.healthchecks.livenessProbe.failureThreshold | int | `5` |  |
| frontend.healthchecks.livenessProbe.initialDelaySeconds | int | `10` |  |
| frontend.healthchecks.livenessProbe.periodSeconds | int | `120` |  |
| frontend.healthchecks.livenessProbe.tcpSocket.port | int | `3000` |  |
| frontend.healthchecks.livenessProbe.timeoutSeconds | int | `5` |  |
| frontend.healthchecks.readinessProbe.failureThreshold | int | `5` |  |
| frontend.healthchecks.readinessProbe.initialDelaySeconds | int | `10` |  |
| frontend.healthchecks.readinessProbe.periodSeconds | int | `120` |  |
| frontend.healthchecks.readinessProbe.tcpSocket.port | int | `3000` |  |
| frontend.healthchecks.readinessProbe.timeoutSeconds | int | `5` |  |
| frontend.healthchecks.startupProbe.failureThreshold | int | `60` |  |
| frontend.healthchecks.startupProbe.initialDelaySeconds | int | `10` |  |
| frontend.healthchecks.startupProbe.periodSeconds | int | `5` |  |
| frontend.healthchecks.startupProbe.tcpSocket.port | int | `3000` |  |
| frontend.healthchecks.startupProbe.timeoutSeconds | int | `2` |  |
| frontend.image.repository | string | `"reallibrephotos/librephotos-frontend"` |  |
| frontend.replicaCount | int | `1` |  |
| fullnameOverride | string | `""` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` | enable ingress  |
| ingress.hostname | string | `""` | currently only hotsname is needed for ingress |
| nameOverride | string | `""` |  |
| postgresql.auth.database | string | `"librephotos"` |  |
| postgresql.auth.username | string | `"librephotos"` |  |
| postgresql.enabled | bool | `true` | install bitnami postgresql |
| proxy.annotations | object | `{}` |  |
| proxy.healthchecks.livenessProbe.failureThreshold | int | `5` |  |
| proxy.healthchecks.livenessProbe.httpGet.path | string | `"/protected_media/"` |  |
| proxy.healthchecks.livenessProbe.httpGet.port | int | `80` |  |
| proxy.healthchecks.livenessProbe.initialDelaySeconds | int | `10` |  |
| proxy.healthchecks.livenessProbe.periodSeconds | int | `60` |  |
| proxy.healthchecks.livenessProbe.timeoutSeconds | int | `5` |  |
| proxy.healthchecks.readinessProbe.failureThreshold | int | `5` |  |
| proxy.healthchecks.readinessProbe.httpGet.path | string | `"/protected_media/"` |  |
| proxy.healthchecks.readinessProbe.httpGet.port | int | `80` |  |
| proxy.healthchecks.readinessProbe.initialDelaySeconds | int | `10` |  |
| proxy.healthchecks.readinessProbe.periodSeconds | int | `60` |  |
| proxy.healthchecks.readinessProbe.timeoutSeconds | int | `5` |  |
| proxy.healthchecks.startupProbe.failureThreshold | int | `60` |  |
| proxy.healthchecks.startupProbe.httpGet.path | string | `"/protected_media/"` |  |
| proxy.healthchecks.startupProbe.httpGet.port | int | `80` |  |
| proxy.healthchecks.startupProbe.initialDelaySeconds | int | `10` |  |
| proxy.healthchecks.startupProbe.periodSeconds | int | `5` |  |
| proxy.healthchecks.startupProbe.timeoutSeconds | int | `2` |  |
| proxy.image.repository | string | `"reallibrephotos/librephotos-proxy"` |  |
| proxy.replicaCount | int | `1` |  |
| redis.architecture | string | `"standalone"` |  |
| redis.enabled | bool | `true` | install bitnami redis |
| redis.master.disableCommands[0] | string | `"FLUSHALL"` |  |
| secret.ADMIN_EMAIL | string | `"admin@mydomain.com"` |  |
| secret.ADMIN_PASSWORD | string | `"password"` |  |
| secret.ADMIN_USERNAME | string | `"admin"` |  |
| secret.MAPBOX_API_KEY | string | `""` |  |
| securityContext.allowPrivilegeEscalation | bool | `false` |  |
| securityContext.capabilities.add | list | `[]` |  |
| securityContext.capabilities.drop | list | `[]` |  |
| securityContext.privileged | bool | `false` |  |
| securityContext.readOnlyRootFilesystem | bool | `false` |  |
| securityContext.runAsNonRoot | bool | `false` |  |
| service.backend.annotations | object | `{}` |  |
| service.backend.ports[0].name | string | `"backend"` |  |
| service.backend.ports[0].port | int | `80` |  |
| service.backend.ports[0].protocol | string | `"TCP"` |  |
| service.backend.ports[0].targetPort | int | `8001` |  |
| service.backend.type | string | `"ClusterIP"` |  |
| service.frontend.annotations | object | `{}` |  |
| service.frontend.ports[0].name | string | `"backend"` |  |
| service.frontend.ports[0].port | int | `80` |  |
| service.frontend.ports[0].protocol | string | `"TCP"` |  |
| service.frontend.ports[0].targetPort | int | `3000` |  |
| service.frontend.type | string | `"ClusterIP"` |  |
| service.proxy.annotations | object | `{}` |  |
| service.proxy.ports[0].name | string | `"backend"` |  |
| service.proxy.ports[0].port | int | `80` |  |
| service.proxy.ports[0].protocol | string | `"TCP"` |  |
| service.proxy.ports[0].targetPort | int | `80` |  |
| service.proxy.type | string | `"ClusterIP"` |  |
| volumes[0] | object | `{"emptyDir":{},"name":"shared"}` | Shared volume, as emptyDir |
| volumes[1] | object | `{"emptyDir":{"medium":"Memory"},"name":"temp"}` | temporary folder in Memory |
| volumes[2] | object | `{"emptyDir":{},"name":"varlogs"}` | logs in emptyDir |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)