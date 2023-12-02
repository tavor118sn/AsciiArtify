# Вступ

Існує кілька інструментів для розгортання Kubernetes кластерів в локальному середовищі, а саме minikube, kind та k3d. Кожен з них відзначається своїми особливостями та можливостями. У цьому порівняльному аналізі ми розглянемо їхні характеристики, переваги та недоліки.

# Загальна інформація

- **minikube**. Це локальна система Kubernetes, яка дозволяє розгортати кластер Kubernetes на одному комп'ютері. Minikube є зручним варіантом для розробки та тестування на локальному комп'ютері. Це проект з відкритим кодом та підтримується спільнотою Kubernetes.

- **kind (Kubernetes IN Docker)**. Це інструмент, який дозволяє створювати локальні Kubernetes кластери в Docker контейнерах.

- **k3d**. Це інструмент для створення локальних Kubernetes кластерів в Docker контейнерах з використанням Rancher Kubernetes Engine (RKE). K3d дозволяє швидко створювати та тестувати кластери Kubernetes у Docker-контейнерах. AsciiArtify також вирішили використовувати k3d для підготовки PoC.


# Характеристики

## minikube

- Підтримувані ОС та архітектури: Linux, macOS, Windows; x86, x86_64, ARM64.
- Можливість автоматизації: Так.
- Додаткові функції: Інтеграція з моніторингом та управлінням Kubernetes кластером.


## kind

- Підтримувані ОС та архітектури: Linux, macOS, Windows; x86_64.
- Можливість автоматизації: Так.
- Додаткові функції: Висока швидкість розгортання, спрощене створення кластерів.


## k3d

- Підтримувані ОС та архітектури: Linux, macOS, Windows; x86_64.
- Можливість автоматизації: Так.
- Додаткові функції: Легкість використання, створення множини кластерів.


# Переваги та недоліки:

Коротка порівняльна таблиця деяких параметрів

| Характеристики | minikube | kind | k3d |
|---------------------------|-----------------------------------------------|--------------------------------------------|--------------------------------------------|
| Управління створенням/видаленням вузлів | Так | Так | Так |
| Можливість автоматизації | Так | Так | Так |
| Швидкість розгортання | Помірна | Висока | Висока |
| Легкість використання | Середня | Висока | Висока |
| Ефективність ресурсів | Зазвичай вимогливий | Зазвичай менш вимогливий | Ефективний по використанню ресурсів |
| Створення та управління кількома кластерами | Ні | Ні | Так |
| Підтримка Helm | Так | Передбачено у використанні, але не стандарт | Так |
| Активна спільнота | Так | Так | Так |
| Додаткові функції | Інтеграція з моніторингом, управлінням Kubernetes | Просте створення кластерів, гаряча заміна вузлів | Ефективне використання ресурсів |


## minikube

Переваги
- Простий у встановленні та використанні. Його можна встановити та налаштувати всього за кілька хвилин, і він вимагає мінімальної конфігурації.
- Має вбудовані додаткові інструменти для роботи з Kubernetes.
- Minikube надає вбудовану панель інструментів, яка дозволяє переглядати та управляти кластером з веб-браузера.
Недоліки 
- Може вимагати встановлення додаткових залежностей.
- Займає більше ресурсів порівняно з деякими іншими інструментами.
- Minikube може повільно запускатися


## kind

Переваги
- Гнучкість - дозволяє налаштовувати свій кластер, додавати або видаляти вузли, змінювати налаштування конфігурації та встановлювати додаткове програмне забезпечення. Minikube та k3d також гнучкі, але вони не надають такого рівня налаштувань, як KinD.
- Використання ресурсів - він використовує контейнери Docker для моделювання кластера Kubernetes, що означає, що він використовує менше ресурсів, ніж Minikube та k3d.
Недоліки
- Вимагаює більше конфігурації, ніж Minikube
- Може вимагати більше ресурсів при збільшенні кількості вузлів кластеру.
- Має менше вбудованих інструментів порівняно з minikube.


## k3d

Переваги
- Швидкість - за кілька секунд він може створити повнофункціональний кластер Kubernetes, і він вимагає мінімальної конфігурації.
- Легкість використання та ефективне використання ресурсів.
- Забезпечує можливість створення та управління кількома кластерами.
- Завдяки оптимізації ресурсів, k3d зазвичай пропонує швидше розгортання кластеру порівняно з minikube та kind.
- k3d може бути ефективнішим у використанні ресурсів порівняно з minikube, що робить його практичним для використання на робочих станціях або в обмежених локальних середовищах.
Недоліки
- Вимагаює більше конфігурації, ніж Minikube
- Можливі проблеми зі сумісністю деяких функцій.


## Podman

Переваги    
- Не вимагає демона для роботи, що полегшує використання та інтеграцію з іншими інструментами.
- Використовує той же контейнерний формат, що й Docker.
Недоліки
- Може вимагати додаткових конфігурацій для інтеграції з Kubernetes.
- Підтримка може бути менш широкою порівняно з Docker.


# Демонстрація

Встановлення k3d:
```sh
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

or

```sh
brew install k3d
```

### Створення кластера та розгортання застосунку


## Встановлення та перевірка k3d

### MacOS

```shell
brew install k3d
```

### Linux

```shell
curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash
```

### Windows
```shell
choco install k3d
```


## Перевірка встановлення k3d

```shell
k3d --version

k3d version v5.6.0
k3s version v1.27.5-k3s1 (default)
```


## Створення кластера k3d

```shell
k3d cluster create mycluster

INFO[0000] Prep: Network
INFO[0000] Created network 'k3d-mycluster'
INFO[0000] Created image volume k3d-mycluster-images
INFO[0000] Starting new tools node...
INFO[0001] Creating node 'k3d-mycluster-server-0'
INFO[0001] Pulling image 'ghcr.io/k3d-io/k3d-tools:5.6.0'
INFO[0002] Pulling image 'docker.io/rancher/k3s:v1.27.5-k3s1'
INFO[0003] Starting Node 'k3d-mycluster-tools'
INFO[0010] Creating LoadBalancer 'k3d-mycluster-serverlb'
INFO[0011] Pulling image 'ghcr.io/k3d-io/k3d-proxy:5.6.0'
INFO[0015] Using the k3d-tools node to gather environment information
INFO[0015] Starting new tools node...
INFO[0015] Starting Node 'k3d-mycluster-tools'
INFO[0017] Starting cluster 'mycluster'
INFO[0017] Starting servers...
INFO[0017] Starting Node 'k3d-mycluster-server-0'
INFO[0019] All agents already running.
INFO[0019] Starting helpers...
INFO[0019] Starting Node 'k3d-mycluster-serverlb'
INFO[0026] Injecting records for hostAliases (incl. host.k3d.internal) and for 3 network members into CoreDNS configmap...
INFO[0028] Cluster 'mycluster' created successfully!
INFO[0028] You can now use it like this:
kubectl cluster-info
```


## Перевірка статусу кластера

```shell
k3d cluster list

NAME        SERVERS   AGENTS   LOADBALANCER
mycluster   1/1       0/0      true
```

```shell
kubectl cluster-info --context k3d-mycluster

Kubernetes control plane is running at https://0.0.0.0:52076
CoreDNS is running at https://0.0.0.0:52076/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://0.0.0.0:52076/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy
```


### Перевірка конфігурації kubectl

Ви можете перевірити, чи kubectl налаштований правильно для вашого кластера k3d, використовуючи:
```shell
kubectl get nodes

NAME                     STATUS   ROLES                  AGE    VERSION
k3d-mycluster-server-0   Ready    control-plane,master   2m8s   v1.27.5+k3s1
```

Це повинно вивести вузли вашого кластера k3d, підтверджуючи, що kubectl підключений до кластера k3d.


### Видалити кластер

```shell
k3d cluster delete mycluster

INFO[0000] Deleting cluster 'mycluster'
INFO[0000] Deleting cluster network 'k3d-mycluster'
INFO[0000] Deleting 1 attached volumes...
INFO[0000] Removing cluster details from default kubeconfig...
INFO[0000] Removing standalone kubeconfig file (if there is one)...
INFO[0000] Successfully deleted cluster mycluster!
```

## Приклад

[![asciicast](https://asciinema.org/a/cjgHyYeFjt6oxancedtUi4kdb.svg)](https://asciinema.org/a/cjgHyYeFjt6oxancedtUi4kdb)


# Висновок

Щодо вибору між Minikube, KinD та k3d, немає чіткого переможця. Кожен інструмент має свої унікальні особливості та переваги, і найкращий вибір для вас буде залежати від конкретних потреб і вподобань.

Якщо важлива легкість використання та вбудована панель інструментів, Minikube може бути кращим вибором. Якщо вам потрібен високорівневий кластер та важлива гнучкість, KinD може бути кращим вибором для вас. Якщо основними вимогами є швидкість та легкий дизайн, k3d може бути кращим вибором.







