
<!-- TOC -->
* [Repository of Helm Charts](#repository-of-helm-charts)
  * [How to use the repo?](#how-to-use-the-repo)
  * [How to use within `skaffold`](#how-to-use-within-skaffold)
  * [Chart List](#chart-list)
    * [Generic Application](#generic-application)
<!-- TOC -->

# Repository of Helm Charts

A repository holding public Helm Charts, which are opinionated for development using Rancher Desktop. Should work on other installation of K8s, as well.


## How to use the repo?

Execute the below command to register the repo with `helm`.

```shell
helm repo add cloud-yantra-oss https://cloud-yantra-oss.github.io/helm/ 
```

The below command will list the Helm charts available under this repo. 
```shell
helm search repo cloud-yantra-oss
```

## How to use within [`skaffold`](https://skaffold.dev/)

In your `mafinest` section in your `skaffold.yaml` file, you can declare the repo as below:
```yaml
manifests:
  helm:
    releases:
      - name: your-app-name
        remoteChart: app
        repo: https://cloud-yantra-oss.github.io/helm/
        valuesFiles:
          - path/to/your/apps/value.yaml
```

## Chart List
### Generic Application

The chart at [app](charts/app) containt an helm chart for a generic microservice, which can be protected by a [OPA (Open Policy Agent)](https://www.openpolicyagent.org/).
