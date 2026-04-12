# Cilium
```bash
kustomize build cilium --enable-helm | kubectl apply -f -

## Esperar a que esté listo
kubectl -n kube-system get pods -l k8s-app=cilium
```

# Cilium-lb
```bash
kubectl apply -k cilium-lb
```

## Podemos probar el LB
```bash
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80 --type=LoadBalancer
kubectl get svc nginx
kubectl delete deployment nginx
kubectl delete svc nginx
```

# Envoy CRDs
```bash
kustomize build envoy-crds | kubectl apply --server-side -f -
```

# Envoy
```bash
kustomize build envoy --enable-helm | kubectl apply -f -
```

## Podemos probar el Envoy
```bash
curl -v -H "Host: www.example.com" 192.168.3.10
```