# Розгортання ArgoCD

## Запуск кластера

```sh
k3d cluster create argo

... 
INFO[0029] Cluster 'argo' created successfully!         
INFO[0029] You can now use it like this: kubectl cluster-info
```

Перевіримо стан
```sh
kubectl cluster-info

Kubernetes control plane is running at https://0.0.0.0:49990
CoreDNS is running at https://0.0.0.0:49990/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://0.0.0.0:49990/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

```sh
kubectl get all -A

...
NAMESPACE     NAME                                                   READY   STATUS      RESTARTS   AGE
kube-system   pod/local-path-provisioner-957fdf8bc-pqgpt             1/1     Running     0          44m
kube-system   pod/coredns-77ccd57875-r49x7                           1/1     Running     0          44m
kube-system   pod/helm-install-traefik-crd-b94dw                     0/1     Completed   0          44m
kube-system   pod/helm-install-traefik-cv6xv                         0/1     Completed   1          44m
kube-system   pod/svclb-traefik-7080422f-r84lc                       2/2     Running     0          44m
kube-system   pod/traefik-64f55bb67d-kspw4                           1/1     Running     0          44m
kube-system   pod/metrics-server-648b5df564-72tcr                    1/1     Running     0          44m
...
```


## Встановлення ArgoCD

```sh
kubectl create namespace argocd

namespace/argocd created
```

Перевіримо що namespace було дійсно створено

```ns
kubectl get ns

NAME              STATUS   AGE
default           Active   48m
kube-system       Active   48m
kube-public       Active   48m
kube-node-lease   Active   48m
argocd            Active   28s
```

Встановлюємо безпосередньо ArgoCD

```sh
kubectl config set-context --current --namespace=argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Перевіряємо чи все було правильно встановлено

```sh
kubectl get all -n argocd

...
NAME                                                   READY   STATUS    RESTARTS   AGE
pod/argocd-redis-b5d6bf5f5-tdzpk                       1/1     Running   0          54m
...
NAME                                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/argocd-redis                       1/1     1            1           54m
...
NAME                                                         DESIRED   CURRENT   READY   AGE
replicaset.apps/argocd-redis-b5d6bf5f5                       1         1         1       54m
...
```

Перевіримо статус подів

```sh
kubectl get po -n argocd -w

NAME                                               READY   STATUS    RESTARTS   AGE
argocd-redis-b5d6bf5f5-tdzpk                       1/1     Running   0          52m
argocd-applicationset-controller-dc5c4c965-bglt6   1/1     Running   0          52m
argocd-notifications-controller-db4f975f8-bm9mk    1/1     Running   0          52m
argocd-repo-server-579cdc7849-cmgk2                1/1     Running   0          52m
argocd-application-controller-0                    1/1     Running   0          52m
argocd-server-557c4c6dff-zldp8                     1/1     Running   0          52m
argocd-dex-server-9769d6499-wdfhx                  1/1     Running   0          52m
^C%
```


## Налаштування доступу до веб інтерфейсу

Прокидання порту сервісу на нашу локальну машину

```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443&

Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
Handling connection for 8080
```

Веб інтерфейс доступний по адресі https://127.0.0.1:8080

За замовчуванням, логін - `admin`. 
Щоб отримати пароль, необхідно виконати наступну команду:

```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath=" {.data.password}"|base64 -d;echo
```

На цьому встановлення завершено. Ми повинні мати розгорнутий ArgoCD та доступ до вебінтерфейсу.