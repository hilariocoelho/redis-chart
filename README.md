# Redis Helm Chart
This chart is composed by a single master and it's meant to be used for a quick deployment for development purposes on x86 and ARM (Raspberry Pi) CPU Architectures.  

In order to keep it as simple as possible, all master-slave or replica set configurations are not present in this chart, although you may a good example on how to setup these in Helm's [stable/redis](https://github.com/helm/charts/tree/master/stable/redis).

## Usage

### Installing chart
Helm 3:
```shell script
git clone https://github.com/SpaWn2KiLl/redis-chart && cd redis-chart
helm install redis .
```

Helm 2:
```shell script
git clone https://github.com/SpaWn2KiLl/redis-chart && cd redis-chart
helm install --name redis .
```

### Uninstalling chart
Helm 3:
```shell script
helm del redis
```

Helm 2:
```shell script
helm del --purge redis
```

#### Warning
You should not use helm 2 because of it's big security issues due the use of tiller. You may find more information on this post by Andrés Martínez, a bitnami's software enginner [here](https://engineering.bitnami.com/articles/running-helm-in-production.html)

## Values

|             **Parameter**            |                 **Description**                 |               **Default**              |
|--------------------------------------|-------------------------------------------------|----------------------------------------|
| `image.arm`                          | Whether to use ARM image or not                 | `true`                                 |
| `image.armImage`                     | Redis docker's image for ARM architecture       | `arm32v7/redis:5.0.7`                  |
| `image.x86Image`                     | Redis docker's image for x86 architecture       | `redis:5.0.7`                          |
| `image.pullPolicy`                   | Docker's image pull policy                      | `IfNotPresent`                         |
| `resources`                          | Pod's resource requests/limits                  | Limits:<br>CPU: `50m`, Memory: `300Mi` |
| `service.type`                       | Kubernetes service type                         | `ClusterIP`                            |
| `service.port`                       | Kubernetes service port                         | `6379`                                 |
| `redis.port`                         | Redis port                                      | `6379`                                 |
| `redis.persistence.enabled`          | Whether to persist data or no                   | `true`                                 |
| `redis.persistence.storageClassName` | Global storage class for dynamic provisioning   |                                        |
| `saves`                              | Redis saves config set (`seconds`, `threshold`) | `save 900 10`<br>`save 30 3`           |