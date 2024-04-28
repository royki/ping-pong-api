# DEVOPS Kubernetes

- Architecture
  - AWS EKS
  - Multi AZ
  - Monitoring
  - Infra Provisioning

## Application Requirements

- Ubuntu `LTS 22.04`
- [Docker](https://docs.docker.com/engine/install/debian/)
- [minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
- [helm chart](https://helm.sh/docs/intro/quickstart/)

## Assignment Requirements

- Docker setup for the service [ping-pong-api](https://github.com/royki/ping-pong-api)
  - ✅ Dockerfile
  - ✅ CI pipeline to create docker image
  - ✅ Docker Image: `royki/ping-pong:v1.0.0`
- ✅ Kubernetes cluster setup (locally)
  - Start minikube cluster: `minikube start`
  - Enable Ingress: `minikube addons enable ingress`
  - Create namespace: `kubectl create namespace app`
- ✅ Run the application:
  - `cd ~/ping-pong-api/infra/ping-pong-api-helm`
  - `helm install ping-pong-api . -n app -f values.yaml`
- ✅ Check app is deployed
  - `kubectl -n app get all`
- ✅ Access ping-pong-api via URL
  - `minikube -n app service ping-pong-api --url`
  - Example: `http://192.168.49.2:31569`
  - Open the URL to the browser:
    - `http://192.168.49.2:31569/ping` -> `pong`
    - `http://192.168.49.2:31569/pong` -> `ping`
  - Can be accessed via `http://ping-pong-api.io/ping`
    - Add minikube IP and host name to `/etc/hosts`
    - `minikube ip` -> `192.168.49.2`
    - Example: `192.168.49.2    ping-pong-api.io`
- Restrict access of Kubernetest resources using rbac
  - ✅ Create `ServiceAccount`, `Role`, `ClusterRole`, `RoleBinding`, `ClusterRoleBinding`
  - ✅ User `dev` has access of `deployments, pods` to `get, watch, list`. User `dev` can't create/deploy deployment, pod. [It's an example]
  - [ ] Check the doc for [Certificates and Certificate Signing Requests](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/#create-certificatesigningrequest)
  - Check whether user can acceess
    - `kubectl auth can-i watch pods --as=dev --namespace=app` -> `yes`
    - `kubectl auth can-i create pods --as=dev --namespace=app` -> `no`
- Other features
  - ✅ Auto scaling
  - ✅ High Availability
