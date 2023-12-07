## Інструкція kubeplugin 

### Встановлення

Спочатку треба надати необхідні дозволи для виконання. У директорії з файлом `kubeplugin` виконати наступну команду

```bash
chmod +x ./kubeplugin
```

Для того, щоб плагін `kubeplugin` був доступний локально для `kubectl`, необхідно його скопіювати у відповідну директорію та перейменуємо:

```bash
cp ./kubeplugin /usr/local/bin/kubectl-kubeplugin
```

Перевіримо, чи плагін доступний

```bash
kubectl plugin list

The following compatible plugins are available:
/usr/local/bin/kubectl-kubeplugin
```

### Використання

Спочатку запустимо плагін без аргументів:

```bash
kubectl kubeplugin

Usage: /usr/local/bin/kubectl-kubeplugin <namespace> <node or pod>
```

Отож, нам потрібно передати бажаний namespace та тип ресурсу. Спробуємо ще раз:

```bash
kubectl kubeplugin kube-system pod

Resource, Namespace, Name, CPU, Memory
pod, kube-system, coredns-77ccd57875-r49x7, 6m, 22Mi
pod, kube-system, local-path-provisioner-957fdf8bc-pqgpt, 2m, 12Mi
pod, kube-system, metrics-server-648b5df564-72tcr, 11m, 29Mi
pod, kube-system, svclb-traefik-7080422f-r84lc, 0m, 0Mi
pod, kube-system, traefik-64f55bb67d-kspw4, 4m, 40Mi
```

Успішний вивід. Плагін встановлений та налаштований.
