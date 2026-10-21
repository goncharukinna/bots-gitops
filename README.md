# Bots GitOps Repository

Этот репозиторий — **единственный источник правды** для развертывания Telegram-ботов в Kubernetes. 

Управление приложениями осуществляется по методологии **GitOps** с помощью **Argo CD**. Любые изменения в манифестах автоматически применяются в кластере.

## 🏗 Архитектура

1. **Разработчик** пушит код в репозиторий бота (например, `random-bot`).
2. **Jenkins** собирает Docker-образ, пушит его в Docker Hub и **обновляет тег** в этом репозитории (`bots-gitops`).
3. **Argo CD** замечает изменение в Git, синхронизирует манифесты и обновляет поды в Kubernetes.

## 📁 Структура

*   `apps/` — манифесты `Application` для Argo CD (по одному на каждого бота).
*   `manifests/` — манифесты `Deployment` и `Service` для каждого бота.

## 🤖 Боты

| Бот | Репозиторий с кодом | Образ Docker Hub |
|-----|---------------------|------------------|
| `random-bot` | [goncharukinna/random-bot](https://github.com/goncharukinna/random-bot) | `docin82/random-bot` |
| `cat-bot` | [goncharukinna/cat-bot](https://github.com/goncharukinna/cat-bot) | `docin82/cat-bot` |
| `hello-bot` | [goncharukinna/hello-bot](https://github.com/goncharukinna/hello-bot) | `docin82/hello-bot` |
| `echo-bot` | [goncharukinna/echo_bot](https://github.com/goncharukinna/echo_bot) | `docin82/echo-bot` |

## 🚀 Как развернуть с нуля

1.  Установите Argo CD в кластер:
    ```bash
    helm install argocd argo/argo-cd -n argocd --create-namespace
