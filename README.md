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

# Cert-Manager
```bash
kustomize build cert-manager --enable-helm | kubectl apply --server-side -f -

## Esperar a que esté listo
kubectl -n cert-manager wait --for=condition=Available deployment --all --timeout=120s
```

## Cert-Manager Config (ClusterIssuers + CA)
```bash
kubectl apply -k cert-manager-config
```

## Verificar
```bash
kubectl get clusterissuer
kubectl get certificate -n cert-manager
```

# ArgoCD
```bash
kustomize build argocd --enable-helm | kubectl apply --server-side -f -
```