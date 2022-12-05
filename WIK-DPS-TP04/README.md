# TP - WIK-DPS-TP04

## Créer un Pod

### Fichier YAML : [./pod1.yaml](./pod1.yaml)

```
WIK-DPS-TP04> kubectl apply -f .\pod1.yaml
pod/serverpod created

WIK-DPS-TP04> kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
serverpod   1/1     Running   0          7m31s

WIK-DPS-TP04> kubectl port-forward serverpod 8080:8080
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080

WIK-DPS-TP04> curl http://localhost:8080/ping
StatusCode        : 200
StatusDescription : OK
Content           : {"user-agent":"Mozilla/5.0 (Windows NT; Windows NT 10.0; fr-FR) WindowsPowerShell/5.1.22000.832","host":"localhost:8080"}
[...]
```

On peut voir que l'image du TP02 fonctionne parfaitement grâce à notre port forwarding.

## Remplacer le Pod par un ReplicaSet

### Fichier YAML : [./pod2.yaml](./pod2.yaml)

```
WIK-DPS-TP04> kubectl apply -f .\pod2.yaml
replicaset.apps/serverrs created

WIK-DPS-TP04> kubectl get pods
NAME             READY   STATUS    RESTARTS   AGE
serverrs-2cp4b   1/1     Running   0          18s
serverrs-72bpc   1/1     Running   0          18s
serverrs-79b2g   1/1     Running   0          18s
serverrs-7b4kw   1/1     Running   0          18s
```

On peut voir que le ReplicaSet a créé 4 réplicas du Pod créé précédemment.

## Remplacer le ReplicaSet par un Deployment

### Fichier YAML : [./pod3.yaml](./pod3.yaml)

```
WIK-DPS-TP04> kubectl apply -f .\pod3.yaml
deployment.apps/serverdeploy created

WIK-DPS-TP04> kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
serverdeploy-698b8d7fd6-8tr4q   1/1     Running   0          41s
serverdeploy-698b8d7fd6-8wnz6   1/1     Running   0          41s
serverdeploy-698b8d7fd6-fjh8t   1/1     Running   0          41s
serverdeploy-698b8d7fd6-md6sm   1/1     Running   0          41s
```

Nos pods se sont bien déployés.

## Créer un Service

### Fichier YAML : [./pod4.yaml](./pod4.yaml)

```
WIK-DPS-TP04> kubectl apply -f .\pod4.yaml
service/server-service created

WIK-DPS-TP04> kubectl get service
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
server-service   ClusterIP   10.106.160.210   <none>        3000/TCP   3m24s

WIK-DPS-TP04> kubectl port-forward service/server-service 3000:3000
Forwarding from 127.0.0.1:3000 -> 8080
Forwarding from [::1]:3000 -> 8080

WIK-DPS-TP04> curl http://localhost:3000/ping

StatusCode        : 200
StatusDescription : OK
Content           : {"user-agent":"Mozilla/5.0 (Windows NT; Windows NT 10.0; fr-FR) WindowsPowerShell/5.1.22000.832","host":"localhost:3000"}
```

On voit que le service fonctionne bien.

## Créer un Ingress

### Fichier YAML : [./pod5.yaml](./pod5.yaml)