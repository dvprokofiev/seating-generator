# Гибридный алгоритм оптимизации рассадки учащихся
[![Build and Push Go Backend Engine Docker Image](https://github.com/chashkakefira/seating-generator-backend/actions/workflows/docker-image.yml/badge.svg)](https://github.com/chashkakefira/seating-generator-backend/actions/workflows/docker-image.yml)
[![Build and Push Vue Frontend Docker Image](https://github.com/chashkakefira/seating-generator-frontend/actions/workflows/docker-image.yml/badge.svg)](https://github.com/chashkakefira/seating-generator-frontend/actions/workflows/docker-image.yml)
![License](https://img.shields.io/badge/license-AGPL--3.0-blue)

Данный мета-репозиторий объединяет все компоненты генератора рассадок. В основе решения задачи лежит гибридная стратегия, сочетающая генетический алгоритм и локальный поиск

## Структура
* **[Вычислительное ядро](https://github.com/chashkakefira/seating-generator-backend)** — Go-сервер, бекенд
* **[Интерфейс пользователя](https://github.com/chashkakefira/seating-generator-frontend)** — Vue-приложение, фронтенд

# Автоматизация сборки
Для автоматизации сборки проекта используется Github Actions. Он собирает два образа контейнеров: ```seating-generator-backend``` и ```seating-generator-frontend```

## Запуск
Для запуска программы на своем компьютере используйте Docker. Для этого клонируйте репозиторий и выполните команду для запуска контейнеров:

``` docker-compose up -d ```
