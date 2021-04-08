# K8s Ingress Controller setup (demo)

This repository contains example how to configure `NGINX Ingress Controller` in **Docker for Mac** and proxy traffic to
backend service.

## Getting Started

### Prerequisite

* Java 11
* Docker for Mac
* Kubernetes

### Installation

* Build docker image.
  ```shell
  ./gradlew bootBuildImage
  ```

* Install `NGINX Ingress Controller`.
  ````shell
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.45.0/deploy/static/provider/cloud/deploy.yaml
  ````

* Check if the ingress controller pods started, run the following command:
  ```shell
  kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
  ```

### Usage

* Start skaffold in dev mode.
  ```shell
  skaffold dev
  ```

* Describe ingress.
  ```shell
  kubectl describe ingress k8s-demo-ingress --namespace k8s-ingress-demo
  ```

* Check if ingress is working.
  ```shell
  curl http://kubernetes.docker.internal/hello
  ```

* Stop skaffold dev (`CMD + C`).

* Uninstall `NGINX Ingress Controller`
  ```shell
  kubectl delete all --all -n ingress-nginx
  kubectl delete ns ingress-nginx
  ```

## References

* [NGINX Ingress Controller - Docker for Mac](https://kubernetes.github.io/ingress-nginx/deploy/#docker-for-mac)
* [Skaffold - Local Kubernetes Development Made Easy](https://www.youtube.com/watch?v=tTNrzEjROCo)
* [Skaffold - Github releases](https://github.com/GoogleContainerTools/skaffold/releases)
* [Google Cloud - Cloud Code](https://cloud.google.com/code)
* [k9s](https://github.com/derailed/k9s)

## License

Distributed under the MIT License. See `LICENSE` for more information.