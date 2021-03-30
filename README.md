# helm-thingsboard

[![CircleCI](https://circleci.com/gh/cetic/helm-thingsboard.svg?style=svg)](https://circleci.com/gh/cetic/helm-thingsboard/tree/master) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) ![version](https://img.shields.io/github/tag/cetic/helm-thingsboard.svg?label=release) ![Version: 2.2](https://img.shields.io/badge/Version-2.2-informational?style=flat-square)

ThingsBoard is an open-source IoT platform for data collection, processing, visualization, and device management.

# Introduction

This [Helm](https://github.com/cetic/helm-thingsboard) chart installs [thingsboard](https://thingsboard.io/) in a Kubernetes cluster.

# Prerequisites

- Kubernetes cluster 1.10+
- Helm 3.0+
- PV provisioner support in the underlying infrastructure.

# Thingsboard

Thingsboard enables device connectivity via industry standard IoT protocols - MQTT, CoAP and HTTP and supports both cloud and on-premises deployments. ThingsBoard combines scalability, fault-tolerance and performance so you will never lose your data.


## RabbitMQ

**[RabbitMQ](https://www.rabbitmq.com/)** is an open source message broker software that implements the Advanced Message Queuing Protocol (AMQP).

ThingsBoard is able to use various messaging systems/brokers for storing the messages and communication between ThingsBoard services, this helm Chart uses RabbitMQ.

 RabbitMQ is recommended if you don’t have much load and you already have experience with this messaging system.

we're using [bitnami/rabbitmq](https://artifacthub.io/packages/helm/bitnami/rabbitmq) helm chart. for more info about how to use it, please check the [documentation ](https://artifacthub.io/packages/helm/bitnami/rabbitmq).

## Configure the chart

The items of section [Configuration](#Configuration) can be set via ``--set`` flag during installation or change the values according to the need of the environment in ``helm-thingsboard/values.yaml`` file.

### Configure the way how to expose thingsboard service:

- **Ingress**: The ingress controller must be installed in the Kubernetes cluster.
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster.
- **NodePort**: Exposes the service on each Node’s IP at a static port (the NodePort). You’ll be able to contact the NodePort service, from outside the cluster, by requesting ``NodeIP:NodePort``.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.

# Installation

Access a Kubernetes cluster.

Add Helm repo:

```bash
helm repo add cetic https://cetic.github.io/helm-charts
```

Update the list helm chart available for installation (like ``apt-get update``). This is recommend before install/upgrade a helm chart:

```bash
helm repo update
helm dep up
```



Change the values according to the environment in the file `values.yaml`.

Install the thingsboard helm chart with a release name `my-release`:

```bash
helm install my-release cetic/thingsboard
```

View the pods.

```bash
kubectl get pods
```

# Uninstallation

To uninstall/delete the ``thingsboard`` deployment:

```bash
helm delete my-release
```

# How to access thingsboard

After deploying the chart in your cluster, you can use the following command to access the thingsboard frontend service: 

```bash
minikube service <my-release>-thingsboard
```

# Configuration

The following tables lists the configurable parameters of the chart and their default values.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity configurations |
| ingress.annotations | object | `{}` | Ingress annotations |
| ingress.enabled | bool | `false` | Enables Ingress |
| ingress.hosts | list | `[{"host":null,"paths":[]}]` | Ingress hosts |
| ingress.tls | list | `[]` | Ingress TLS configuration |
| nodeSelector | object | `{}` | nodeSelector configurations |
| rabbitmq.enabled | bool | `true` | enable rabbitmq |
| rabbitmq.auth.username | string | `"admin"` | userName of rabbitmq |
| rabbitmq.auth.password | string | `"password1"` | Password of rabbitmq |
| rabbitmq.ldap.enabled | bool | false | enable/disable ldad for user authentication |
| rabbitmq.ldap.server | string | `my-openldap` | ldap server adress |
| rrabbitmq.ldap.port | int | `389` | ldap server port |
| rabbitmq.ldap.user\_dn\_pattern | string | `cn=${username},dc=example,dc=org` | ldap user dn pattern |
| readinessProbe.enabled | bool | true | enable/disbale ReadinessProbe |
| readinessProbe.initialDelaySeconds | int | `60` | Specifies the number of the readinessProbe's delay seconds |
| readinessProbe.periodSeconds | int | `7` | readinessProbe's period seconds |
| TB_RABBIT_MQ.TB_QUEUE_TYPE | string | `"rabbitmq"` | ThingsBoard QUEUE TYPE |
| TB_RABBIT_MQ.TB_QUEUE_RABBIT_MQ_USERNAME | string | `"admin"` | rabbitmq's username |
| TB_RABBIT_MQ.TB_QUEUE_RABBIT_MQ_PASSWORD | string | `"password1"` | rabbitmq's password |
| TB_RABBIT_MQ.TB_QUEUE_RABBIT_MQ_HOST | string | `"rabbitmq"` | rabbitmq's host |
| TB_RABBIT_MQ.TB_QUEUE_RABBIT_MQ_PORT | int | `5672` | rabbitmq's port |


# Uninstallation


To delete the thingsboard release:

```bash
helm delete my-release
```


# License

[Apache License 2.0](/LICENSE)