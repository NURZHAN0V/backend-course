# 🟢 Проект: Node.js REST API

## 📋 Описание проекта

Создание полнофункционального REST API на Node.js с использованием современных технологий и лучших практик backend разработки.

## 🎯 Цели проекта

После выполнения этого проекта вы сможете:
- Создавать RESTful API на Node.js
- Работать с базами данных (MongoDB/PostgreSQL)
- Реализовывать аутентификацию и авторизацию
- Применять middleware и обработку ошибок
- Тестировать API endpoints
- Документировать API с помощью Swagger

## 📚 Связанные блоки

- Блоки 39-47: Все блоки Node.js
- Блок 44: Аутентификация и безопасность
- Блок 45: Тестирование и отладка
- Блок 46: Работа с базами данных

## 🚀 Задания проекта

### Этап 1: Базовый API
**Проект:** Система управления задачами (Task Management API)
- CRUD операции для задач
- Валидация данных
- Обработка ошибок
- Логирование

### Этап 2: Аутентификация
- Регистрация и авторизация пользователей
- JWT токены
- Middleware для защиты роутов
- Роли и права доступа

### Этап 3: База данных
- Подключение к MongoDB/PostgreSQL
- Модели данных
- Миграции и сиды
- Оптимизация запросов

### Этап 4: Продвинутые возможности
- Пагинация и фильтрация
- Загрузка файлов
- Email уведомления
- Rate limiting

## 📁 Структура проекта

```
nodejs-api/
├── README.md
├── package.json
├── .env.example
├── src/
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   ├── tasks.controller.js
│   │   └── users.controller.js
│   ├── middleware/
│   │   ├── auth.middleware.js
│   │   ├── validation.middleware.js
│   │   └── error.middleware.js
│   ├── models/
│   │   ├── User.js
│   │   └── Task.js
│   ├── routes/
│   │   ├── auth.routes.js
│   │   ├── tasks.routes.js
│   │   └── users.routes.js
│   ├── services/
│   │   ├── auth.service.js
│   │   ├── email.service.js
│   │   └── file.service.js
│   ├── utils/
│   │   ├── database.js
│   │   ├── logger.js
│   │   └── validators.js
│   ├── config/
│   │   └── index.js
│   └── app.js
├── tests/
│   ├── auth.test.js
│   ├── tasks.test.js
│   └── users.test.js
├── docs/
│   ├── api-documentation.md
│   └── swagger.yaml
└── scripts/
    ├── seed.js
    └── migrate.js
```

## ⏱️ Время выполнения

**Общее время:** 30-35 часов
- Этап 1 (Базовый API): 8-10 часов
- Этап 2 (Аутентификация): 8-10 часов
- Этап 3 (База данных): 7-8 часов
- Этап 4 (Продвинутые функции): 7-7 часов

## 🏆 Критерии оценки

### Функциональность
- ✅ Все CRUD операции работают
- ✅ Аутентификация и авторизация настроены
- ✅ База данных интегрирована
- ✅ Валидация данных реализована
- ✅ Обработка ошибок настроена

### Качество кода
- ✅ Код структурирован и читаем
- ✅ Использованы лучшие практики Node.js
- ✅ Настроен линтинг (ESLint)
- ✅ Написаны unit и integration тесты
- ✅ Документация API создана

### Безопасность
- ✅ Пароли хешируются
- ✅ JWT токены защищены
- ✅ Валидация входных данных
- ✅ Rate limiting настроен
- ✅ CORS настроен правильно

## 🛠 Технологический стек

### Основные технологии
- **Node.js** - серверная платформа
- **Express.js** - веб-фреймворк
- **MongoDB/PostgreSQL** - база данных
- **Mongoose/Sequelize** - ORM/ODM

### Дополнительные библиотеки
- **jsonwebtoken** - JWT токены
- **bcryptjs** - хеширование паролей
- **joi** - валидация данных
- **winston** - логирование
- **nodemailer** - отправка email
- **multer** - загрузка файлов

### Инструменты разработки
- **Jest** - тестирование
- **Supertest** - тестирование API
- **ESLint** - линтинг кода
- **Prettier** - форматирование
- **Swagger** - документация API

## 📖 API Endpoints

### Аутентификация
- `POST /api/auth/register` - Регистрация
- `POST /api/auth/login` - Вход
- `POST /api/auth/logout` - Выход
- `POST /api/auth/refresh` - Обновление токена

### Пользователи
- `GET /api/users/profile` - Профиль пользователя
- `PUT /api/users/profile` - Обновление профиля
- `DELETE /api/users/profile` - Удаление аккаунта

### Задачи
- `GET /api/tasks` - Список задач
- `POST /api/tasks` - Создание задачи
- `GET /api/tasks/:id` - Получение задачи
- `PUT /api/tasks/:id` - Обновление задачи
- `DELETE /api/tasks/:id` - Удаление задачи

## 🚀 Запуск проекта

```bash
# Установка зависимостей
npm install

# Настройка переменных окружения
cp .env.example .env

# Запуск в режиме разработки
npm run dev

# Запуск тестов
npm test

# Запуск в продакшене
npm start
```

---

**Статус:** 🔴 Ожидает создания блоков Node.js 