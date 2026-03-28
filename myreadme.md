
```
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.30/deploy/local-path-storage.yaml
namespace/local-path-storage created
serviceaccount/local-path-provisioner-service-account created
role.rbac.authorization.k8s.io/local-path-provisioner-role created
clusterrole.rbac.authorization.k8s.io/local-path-provisioner-role created
rolebinding.rbac.authorization.k8s.io/local-path-provisioner-bind created
clusterrolebinding.rbac.authorization.k8s.io/local-path-provisioner-bind created
deployment.apps/local-path-provisioner created
storageclass.storage.k8s.io/local-path created
configmap/local-path-config created
```

** Make it the default storage class:**
```
kubectl annotate storageclass local-path storageclass.kubernetes.io/is-default-class=true
```

```
helm $ kubectl describe pod -n ollama
.
.
.
Events:
  Type     Reason            Age    From               Message
  ----     ------            ----   ----               -------
  Warning  FailedScheduling  7m46s  default-scheduler  0/4 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/4 nodes are available: 4 Preemption is not helpful for scheduling.
  Normal   Scheduled         6m8s   default-scheduler  Successfully assigned ollama/ollama-75dfcf7c84-zpx8q to worker2
  Normal   Pulling           6m8s   kubelet            spec.containers{ollama}: Pulling image "ollama/ollama:0.18.3"
  Normal   Pulled            3m32s  kubelet            spec.containers{ollama}: Successfully pulled image "ollama/ollama:0.18.3" in 2m35.654s (2m35.654s including waiting). Image size: 3646908667 bytes.
  Normal   Created           3m32s  kubelet            spec.containers{ollama}: Created container: ollama
  Normal   Started           3m32s  kubelet            spec.containers{ollama}: Started container ollama
```

![](./images/ollama-pod-describe.png)

