# Sausage Store — Развёртывание в Kubernetes

### Предварительные требования

Перед запуском убедитесь, что на вашей машине установлены следующие инструменты:

- [`kubectl`](https://kubernetes.io/docs/tasks/tools/)
- [`helm`](https://helm.sh/docs/intro/install/)

### Установка приложения

1. Перейдите в директорию с Helm chart'ом:

```bash
cd sausage-store-chart
```

2. Установите Helm-чарт:

```bash
helm install sausage-store .
```

3. Убедитесь, что все поды успешно запущены:

```bash
kubectl get pods
```

### Проверка работоспособности

- Деплойменты:

```bash
kubectl get deployments
```

- Логи:

```bash
kubectl logs deployment/sausage-store-frontend
kubectl logs deployment/sausage-store-backend
kubectl logs deployment/sausage-store-backend-report
```

- Cервисы:

```bash
kubectl get svc
```

- Ингрессы

```bash
kubectl get ingress
```

- VPA

```bash
kubectl describe vpa sausage-store-backend-vpa
```

- HPA

```bash
kubectl describe hpa sausage-store-backend-report-hpa
```

### Доступ к приложению

После успешного развёртывания приложение будет доступно по ссылке:

https://front-timofeev.2sem.students-projects.ru
