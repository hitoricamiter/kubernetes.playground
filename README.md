# Fullstack Kubernetes Helm Deployment

Репозиторий содержит Kubernetes манифесты и Helm шаблоны для развертывания fullstack приложения с **PostgreSQL**, **Spring Boot бэкендами** и **статическим фронтендом**. Все параметры конфигурируются через `values.yaml`.

## Компоненты

### PostgreSQL
- **Deployment** с настраиваемым количеством реплик.
- **PersistentVolumeClaim** для хранения данных (`ReadWriteOnce`).
- **Secret** для учётных данных БД и переменных окружения Spring Boot.
- **Service**: TCP 5432 для внутреннего использования.

### Бэкенд сервисы
- `backend-deployment-1` и `backend-deployment-2` с приложениями Spring Boot.
- Переменные окружения берутся из секрета PostgreSQL.
- **LoadBalancer Services** для внешнего доступа, IP настраивается через `values.yaml`.

### Фронтенд
- **Deployment** с раздачей статической HTML через ConfigMap.
- Простейший интерфейс с кнопками для:
  - заполнения БД (`seed`)
  - загрузки списка продуктов (`load`)
  - очистки продуктов (`clear`)
  - вызова тестового `/hi`
- **LoadBalancer Service** для внешнего доступа.

### Ingress
- Настраивается через `values.yaml`.
- `backend-ingress`: маршруты `/products` → backend-1, `/welcome` → backend-2.
- `frontend-ingress`: отдаёт фронтенд.

## Helm Values

Все параметры хранятся в `values.yaml`:

- `postgres`: образ, тег, размер PVC, реплики, креденшалы.
- `backendOne`, `backendTwo`: образ, тег, порт сервиса, реплики, IP LoadBalancer.
- `frontend`: образ, тег, порт сервиса, реплики, IP LoadBalancer.
- `ingress`: включён/выключен, класс, хосты, пути.

## Развёртывание

```bash
# Установка или обновление релиза
helm upgrade --install fullstack . -f values.yaml

# Проверка Pod'ов
kubectl get pods

# Проверка сервисов и IP LoadBalancer
kubectl get svc
