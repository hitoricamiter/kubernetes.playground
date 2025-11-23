1. Spotless (Java форматирование)

Что подключить:
spotless-maven-plugin

Что настроить:
– стиль форматирования (обычно googleJavaFormat)

2. yamllint (проверка YAML)

Что подключить:
yamllint (утилита)

Что настроить:
– .yamllint.yaml (правила: отступы, длина строки, ключи)

3. hadolint (Dockerfile lint)

Что подключить:
hadolint (бинарь или через Docker)

Что настроить:
– .hadolint.yaml — правила (можно выключить некоторые проверки)

4. JaCoCo (coverage)

Что подключить:
jacoco-maven-plugin

Что настроить:
– включить цель jacoco:report
– путь отчёта GitLab читает автоматически (jacoco.xml)

5. JUnit (юнит-тесты)

Что подключить:
junit-jupiter

Что настроить:
– ничего особого, просто тесты

6. Trivy (security scan Docker образа)

Что подключить:
trivy (apk install, binary или Docker)

Что настроить:
– уровни уязвимостей для fail (HIGH, CRITICAL)

7. Docker + Docker-in-Docker

Что подключить:
docker:24 + docker:dind

Что настроить:
– логин в registry
– build/push через $CI_REGISTRY

8. kubectl

Что подключить:
образ bitnami/kubectl

Что настроить:
– kubeconfig контексты (dev-cluster, stage-cluster, prod-cluster)


kubeval — проверка Kubernetes YAML на корректность схемы.

kube-score — проверка best-practices для K8s манифестов.