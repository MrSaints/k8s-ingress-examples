# istio

https://istio.io/

## Basic Setup

```
curl -L https://git.io/getLatestIstio | sh -
helm template istio-<version>/install/kubernetes/helm/istio --name istio --namespace istio-system \
    --set pilot.resources.requests.cpu=200m \
    --set pilot.resources.requests.memory=256Mi > istio.yaml
kubectl create namespace istio-system
kubectl apply -f istio.yaml
```
