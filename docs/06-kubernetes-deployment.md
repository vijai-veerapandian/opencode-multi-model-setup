# 06 - Kubernetes Deployment for Ollama

This guide details the steps to deploy the local Ollama instance to a Kubernetes cluster running Metallb and a Gateway API (like Cilium). This enables `opencode` or other tools to access the models served by Ollama from within your local network.

## Prerequisites

- A running Kubernetes cluster (e.g., K3s, K8s).
- `kubectl` configured to interact with your cluster.
- A local storage provisioner.

## Step 1: Install Local Path Provisioner

To ensure persistent storage for the downloaded Ollama models, we deploy the local-path-provisioner:

```bash
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.30/deploy/local-path-storage.yaml
```

Once deployed, make it the default storage class:

```bash
kubectl annotate storageclass local-path storageclass.kubernetes.io/is-default-class=true
```

## Step 2: Deploy Ollama Manifests

You can deploy the Ollama components using the manifests provided in the `ollama-k8s` directory. These configurations include the namespace, persistent volume claim, deployment, configmap, service, IP address pool, and HTTPRoute.

```bash
kubectl apply -f ollama-k8s/namespace.yaml
kubectl apply -f ollama-k8s/
```

### Alternatively: Helm Deployment

If you prefer deploying via Helm, a `values.yaml` file is provided at `helm/ollama-values.yaml`.

```bash
helm repo add ollama-helm https://otwld.github.io/ollama-helm/
helm repo update
helm upgrade --install ollama ollama-helm/ollama --namespace ollama --create-namespace -f helm/ollama-values.yaml
```

## Step 3: Verify the Deployment

Verify that the Ollama pod is running and has successfully pulled the selected model via the initializer:

```bash
kubectl get pods -n ollama
```

To see detailed events and confirm the model image has been pulled successfully, execute:

```bash
kubectl describe pod -n ollama -l app=ollama
```

## Step 4: Accessing the API

The deployment includes a `gateway.yaml` which sets up an HTTP Route (`ollama-route`) routing traffic to the `ollama` service on port `11434`. Combined with the `metallb-config.yaml` assigning the IP pool `192.168.2.240-192.168.2.250`, you can point your tools via HTTP to the Gateway IP assigned to the `cilium-gateway`.

For example, to list available local models via the API:

```bash
curl http://192.168.2.240/api/tags
```
