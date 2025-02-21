# hub-fips-win

Testing Windows FIPS image of Traefik Hub

## Deploy Hub

### Create namespace

```bash
kubectl create ns traefik
```

### Create Hub token secret

```bash
kubectl create secret generic hub-license --from-literal=token="${HUB_TOKEN}" -n traefik
```

### deploy Hub

```bash
helm upgrade --install traefik traefik/traefik --create-namespace --namespace traefik --values hub/hub-values.yaml --set-json 'nodeSelector={"kubernetes.io/os": "windows"}' --set-json 'podSecurityContext=null' 
```

### Set DNS entry

```bash

```

### Deploy dashboard ingress

```bash
envsubst < hub/ingress.yaml | kubectl apply -f -
```

## Deploy app

### Create apps namespace

```bash
kubectl create ns whoami
```

### Deploy whoami and ingress

```bash
kubectl apply -f whoami/whoami.yaml
envsubst < whoami/ingress.yaml | kubectl apply -f -
```
