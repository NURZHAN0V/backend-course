# 🏗️ Проект: Microservices Application

## 📋 Описание проекта

Создание полноценного приложения на основе микросервисной архитектуры с использованием современных технологий контейнеризации и оркестрации.

## 🎯 Цели проекта

После выполнения этого проекта вы сможете:
- Проектировать микросервисную архитектуру
- Создавать независимые сервисы на Node.js
- Настраивать межсервисное взаимодействие
- Использовать Docker и Docker Compose
- Реализовывать API Gateway
- Настраивать мониторинг и логирование

## 📚 Связанные блоки

- Блок 48: Архитектура микросервисов
- Все предыдущие блоки Node.js (39-47)
- Блоки TypeScript для типизации

## 🚀 Архитектура приложения

### Основные сервисы
1. **API Gateway** - Единая точка входа
2. **User Service** - Управление пользователями
3. **Product Service** - Каталог товаров
4. **Order Service** - Обработка заказов
5. **Payment Service** - Платежная система
6. **Notification Service** - Уведомления

### Инфраструктурные сервисы
- **Service Discovery** - Consul/Eureka
- **Message Broker** - RabbitMQ/Apache Kafka
- **Database** - PostgreSQL, MongoDB, Redis
- **Monitoring** - Prometheus + Grafana
- **Logging** - ELK Stack

## 📁 Структура проекта

```
microservices-app/
├── README.md
├── docker-compose.yml
├── docker-compose.dev.yml
├── .env.example
├── services/
│   ├── api-gateway/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── src/
│   ├── user-service/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── src/
│   ├── product-service/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── src/
│   ├── order-service/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── src/
│   ├── payment-service/
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── src/
│   └── notification-service/
│       ├── Dockerfile
│       ├── package.json
│       └── src/
├── infrastructure/
│   ├── databases/
│   │   ├── postgres/
│   │   ├── mongodb/
│   │   └── redis/
│   ├── monitoring/
│   │   ├── prometheus/
│   │   └── grafana/
│   └── logging/
│       └── elk/
├── shared/
│   ├── types/
│   ├── utils/
│   └── middleware/
├── tests/
│   ├── integration/
│   └── e2e/
└── scripts/
    ├── setup.sh
    ├── deploy.sh
    └── cleanup.sh
```

## 🛠 Технологический стек

### Backend
- **Node.js + TypeScript** - основная платформа
- **Express.js** - веб-фреймворк
- **GraphQL** - для API Gateway
- **gRPC** - межсервисное взаимодействие

### Базы данных
- **PostgreSQL** - реляционные данные
- **MongoDB** - документы и каталоги
- **Redis** - кеширование и сессии

### Инфраструктура
- **Docker** - контейнеризация
- **Docker Compose** - оркестрация
- **Nginx** - reverse proxy
- **RabbitMQ** - очереди сообщений

### Мониторинг
- **Prometheus** - метрики
- **Grafana** - дашборды
- **Jaeger** - трассировка
- **ELK Stack** - логирование

## 🚀 Этапы разработки

### Этап 1: Базовая архитектура (8-10 часов)
- Настройка Docker окружения
- Создание базовых сервисов
- Настройка API Gateway
- Межсервисное взаимодействие

### Этап 2: Бизнес-логика (10-12 часов)
- Реализация User Service
- Создание Product Service
- Разработка Order Service
- Интеграция Payment Service

### Этап 3: Инфраструктура (6-8 часов)
- Настройка баз данных
- Конфигурация очередей
- Service Discovery
- Load Balancing

### Этап 4: Мониторинг и DevOps (4-6 часов)
- Настройка мониторинга
- Централизованное логирование
- Health checks
- CI/CD pipeline

## ⏱️ Время выполнения

**Общее время:** 28-36 часов
- Планирование архитектуры: 2-4 часа
- Разработка сервисов: 18-22 часа
- Настройка инфраструктуры: 6-8 часов
- Тестирование и отладка: 2-2 часа

## 🏆 Критерии оценки

### Архитектура
- ✅ Сервисы слабо связаны
- ✅ Каждый сервис имеет свою БД
- ✅ API Gateway настроен
- ✅ Service Discovery работает
- ✅ Обработка ошибок реализована

### Функциональность
- ✅ Все CRUD операции работают
- ✅ Межсервисное взаимодействие настроено
- ✅ Асинхронная обработка реализована
- ✅ Транзакции между сервисами
- ✅ Кеширование настроено

### DevOps
- ✅ Все сервисы контейнеризированы
- ✅ Docker Compose настроен
- ✅ Мониторинг работает
- ✅ Логирование централизовано
- ✅ Health checks настроены

### Безопасность
- ✅ JWT токены между сервисами
- ✅ Rate limiting настроен
- ✅ HTTPS настроен
- ✅ Секреты в переменных окружения
- ✅ Network isolation

## 📖 API Endpoints

### API Gateway (Port 3000)
- `POST /api/auth/login` - Аутентификация
- `GET /api/users/*` - Проксирование к User Service
- `GET /api/products/*` - Проксирование к Product Service
- `POST /api/orders/*` - Проксирование к Order Service

### User Service (Port 3001)
- `GET /users` - Список пользователей
- `POST /users` - Создание пользователя
- `GET /users/:id` - Получение пользователя
- `PUT /users/:id` - Обновление пользователя

### Product Service (Port 3002)
- `GET /products` - Каталог товаров
- `POST /products` - Добавление товара
- `GET /products/:id` - Информация о товаре
- `PUT /products/:id` - Обновление товара

### Order Service (Port 3003)
- `GET /orders` - Список заказов
- `POST /orders` - Создание заказа
- `GET /orders/:id` - Информация о заказе
- `PUT /orders/:id/status` - Обновление статуса

## 🚀 Запуск проекта

```bash
# Клонирование репозитория
git clone <repository-url>
cd microservices-app

# Настройка переменных окружения
cp .env.example .env

# Запуск всех сервисов
docker-compose up -d

# Просмотр логов
docker-compose logs -f

# Остановка сервисов
docker-compose down

# Запуск в режиме разработки
docker-compose -f docker-compose.dev.yml up
```

## 📊 Мониторинг

### Grafana Dashboard
- URL: http://localhost:3001
- Логин: admin / admin
- Дашборды для каждого сервиса

### Prometheus Metrics
- URL: http://localhost:9090
- Метрики производительности
- Алерты и уведомления

### Jaeger Tracing
- URL: http://localhost:16686
- Трассировка запросов
- Анализ производительности

## 🧪 Тестирование

```bash
# Unit тесты для каждого сервиса
npm run test:unit

# Integration тесты
npm run test:integration

# E2E тесты
npm run test:e2e

# Load тесты
npm run test:load
```

---

**Статус:** 🔴 Ожидает создания блока Микросервисы 