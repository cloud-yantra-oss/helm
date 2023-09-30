
<!-- TOC -->
* [Repository of Helm Charts](#repository-of-helm-charts)
  * [How to use the repo?](#how-to-use-the-repo)
  * [Chart List](#chart-list)
    * [1. Generic Application](#1-generic-application)
      * [How to use within `skaffold`](#how-to-use-within-skaffold)
    * [2. Postgresql](#2-postgresql-)
      * [How to use within `skaffold`](#how-to-use-within-skaffold-1)
    * [3. SurrealDB](#3-surrealdb-)
      * [How to use within `skaffold`](#how-to-use-within-skaffold-2)
<!-- TOC -->

# Repository of Helm Charts

A repository holding public Helm Charts, which are opinionated for development using Rancher Desktop.
They should work on another installation of K8s, as well.


## How to use the repo?

Execute the below command to register the repo with `helm`.

```shell
helm repo add cloud-yantra-oss https://cloud-yantra-oss.github.io/helm/ 
```

The below command will list the Helm charts available under this repo. 
```shell
helm search repo cloud-yantra-oss
```

## Chart List
### 1. Generic Application

The chart at [app](charts/app) contains a helm chart for a generic microservice,
which can be protected by [OPA (Open Policy Agent)](https://www.openpolicyagent.org/).

#### How to use within [`skaffold`](https://skaffold.dev/)

In your `mafinest` section in your `skaffold.yaml` file, you can declare the repo as below:
```yaml
manifests:
  helm:
    releases:
      - name: your-app-name
        repo: https://cloud-yantra-oss.github.io/helm/
        remoteChart: app
        valuesFiles:
          - path/to/your/apps/value.yaml
```

### 2. Postgresql 

The chart at [postgresql](charts/postgresql) contains a helm chart for deploying a Postgresql server.

The default values are available in the [`values.yaml`](charts/postgresql/values.yaml) file.

#### How to use within [`skaffold`](https://skaffold.dev/)

In your `mafinest` section in your `skaffold.yaml` file, you can declare the repo as below:
```yaml
manifests:
  helm:
    releases:
      - name: postgresql
        repo: https://cloud-yantra-oss.github.io/helm/
        remoteChart: postgresql
        setValues:
          image.repository: postgres
          image.tag: 16
```


### 3. SurrealDB 

The chart at [surrealdb](charts/surrealdb) contains a helm chart for deploying a SurrealDB server.

The default values are available in the [`values.yaml`](charts/surrealdb/values.yaml) file.

#### How to use within [`skaffold`](https://skaffold.dev/)

In your `mafinest` section in your `skaffold.yaml` file, you can declare the repo as below:
```yaml
manifests:
  helm:
    releases:
      - name: surrealdb
        repo: https://cloud-yantra-oss.github.io/helm/
        remoteChart: surrealdb
        setValues:
          image.repository: docker.io
          image.name: surrealdb/surrealdb
          image.tag: latest
          service.ingress.enabled: true
          service.ingress.host: surrealdb.database.local
```
