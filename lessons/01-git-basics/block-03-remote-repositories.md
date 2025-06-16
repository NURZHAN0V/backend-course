# Блок 3. Основы Git - Удаленные репозитории (3.5 часа)

## 🎯 Цели блока

После изучения этого блока вы сможете:
- Создавать и настраивать удаленные репозитории
- Генерировать и использовать SSH ключи
- Понимать концепции remote tracking branches
- Работать с upstream ветками
- Использовать clone, push, pull и fetch
- Применять force push безопасно

---

## 📚 Теоретическая часть

### 1. Удаленные репозитории (Remote Repositories)

Удаленные репозитории - это версии вашего проекта, размещенные в интернете или сети.

#### Основные команды для работы с remote:
```bash
# Просмотр удаленных репозиториев
git remote

# Подробная информация об удаленных репозиториях
git remote -v

# Добавление удаленного репозитория
git remote add origin https://github.com/username/repo.git

# Переименование remote
git remote rename origin upstream

# Удаление remote
git remote remove origin

# Изменение URL remote
git remote set-url origin https://github.com/username/new-repo.git
```

### 2. SSH ключи для безопасного подключения

SSH ключи обеспечивают безопасное подключение к удаленным репозиториям без ввода пароля.

#### Генерация SSH ключа:
```bash
# Генерация нового SSH ключа
ssh-keygen -t ed25519 -C "your.email@example.com"

# Для старых систем (RSA)
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"

# Запуск SSH агента
eval "$(ssh-agent -s)"

# Добавление ключа в SSH агент
ssh-add ~/.ssh/id_ed25519

# Копирование публичного ключа (Linux/Mac)
cat ~/.ssh/id_ed25519.pub

# Тестирование подключения к GitHub
ssh -T git@github.com
```

#### Настройка SSH для разных сервисов:
```bash
# Файл ~/.ssh/config
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519

Host gitlab.com
    HostName gitlab.com
    User git
    IdentityFile ~/.ssh/id_rsa_gitlab
```

### 3. Remote Tracking Branches

Remote tracking branches - это локальные ссылки на состояние веток в удаленном репозитории.

```bash
# Просмотр всех веток (включая remote)
git branch -a

# Просмотр только remote веток
git branch -r

# Создание локальной ветки из remote
git checkout -b feature origin/feature

# Установка upstream для существующей ветки
git branch --set-upstream-to=origin/main main
```

### 4. Local Tracking Branches и Upstream

```bash
# Создание ветки с автоматической настройкой upstream
git checkout -b feature origin/feature

# Установка upstream для текущей ветки
git branch -u origin/main

# Просмотр upstream настроек
git branch -vv

# Push с установкой upstream
git push -u origin feature
```

### 5. Клонирование репозиториев

```bash
# Обычное клонирование
git clone https://github.com/username/repo.git

# Клонирование в конкретную папку
git clone https://github.com/username/repo.git my-project

# Клонирование только последнего коммита (shallow clone)
git clone --depth 1 https://github.com/username/repo.git

# Клонирование конкретной ветки
git clone -b develop https://github.com/username/repo.git
```

### 6. Синхронизация с удаленным репозиторием

#### Fetch - получение изменений без слияния:
```bash
# Получение всех изменений
git fetch

# Получение изменений из конкретного remote
git fetch origin

# Получение конкретной ветки
git fetch origin main
```

#### Pull - получение и слияние изменений:
```bash
# Pull для текущей ветки
git pull

# Pull из конкретного remote и ветки
git pull origin main

# Pull с rebase вместо merge
git pull --rebase

# Настройка pull с rebase по умолчанию
git config --global pull.rebase true
```

#### Push - отправка изменений:
```bash
# Push текущей ветки
git push

# Push в конкретный remote и ветку
git push origin main

# Push с установкой upstream
git push -u origin feature

# Push всех веток
git push --all

# Push тегов
git push --tags
```

### 7. Force Push - принудительная отправка

⚠️ **Осторожно!** Force push может перезаписать историю в удаленном репозитории.

```bash
# Обычный force push (опасно!)
git push --force

# Безопасный force push
git push --force-with-lease

# Force push конкретной ветки
git push --force-with-lease origin feature
```

#### Когда использовать force push:
- После rebase локальной ветки
- После amend последнего коммита
- При исправлении истории в feature ветках
- **НИКОГДА** не делайте force push в main/master!

---

## 💻 Практические упражнения

### Упражнение 1: Создание удаленного репозитория (45 минут)

1. Создайте аккаунт на GitHub (если нет)
2. Создайте новый репозиторий `git-practice`
3. Клонируйте репозиторий локально:
```bash
git clone https://github.com/username/git-practice.git
cd git-practice
```

4. Создайте файл и отправьте изменения:
```bash
echo "# Git Practice Repository" > README.md
git add README.md
git commit -m "Initial commit"
git push origin main
```

### Упражнение 2: Настройка SSH ключей (30 минут)

1. Сгенерируйте SSH ключ:
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

2. Добавьте публичный ключ в GitHub:
   - Скопируйте содержимое `~/.ssh/id_ed25519.pub`
   - Перейдите в Settings → SSH and GPG keys
   - Добавьте новый SSH ключ

3. Измените URL репозитория на SSH:
```bash
git remote set-url origin git@github.com:username/git-practice.git
```

4. Проверьте подключение:
```bash
ssh -T git@github.com
```

### Упражнение 3: Работа с ветками и remote (60 минут)

1. Создайте и переключитесь на новую ветку:
```bash
git checkout -b feature/authentication
```

2. Создайте файл `auth.js`:
```javascript
function authenticate(token) {
    if (!token) {
        throw new Error('Token is required');
    }
    
    // Здесь будет логика аутентификации
    console.log('User authenticated successfully');
    return { success: true, user: 'testuser' };
}

module.exports = { authenticate };
```

3. Зафиксируйте изменения:
```bash
git add auth.js
git commit -m "Add authentication function"
```

4. Отправьте ветку на remote с установкой upstream:
```bash
git push -u origin feature/authentication
```

5. Проверьте remote ветки:
```bash
git branch -a
git branch -vv
```

### Упражнение 4: Совместная работа - Fork и Pull Request (45 минут)

1. Сделайте fork любого открытого проекта на GitHub
2. Клонируйте свой fork:
```bash
git clone git@github.com:yourusername/forked-repo.git
cd forked-repo
```

3. Добавьте upstream remote:
```bash
git remote add upstream git@github.com:originalowner/original-repo.git
```

4. Создайте ветку для изменений:
```bash
git checkout -b fix/typo-in-readme
```

5. Внесите небольшое изменение (исправьте опечатку в README)
6. Зафиксируйте и отправьте изменения:
```bash
git add .
git commit -m "Fix typo in README"
git push -u origin fix/typo-in-readme
```

### Упражнение 5: Синхронизация с upstream (30 минут)

1. Получите изменения из upstream:
```bash
git fetch upstream
```

2. Переключитесь на main и обновите:
```bash
git checkout main
git merge upstream/main
```

3. Обновите свой fork:
```bash
git push origin main
```

4. Обновите feature ветку с помощью rebase:
```bash
git checkout fix/typo-in-readme
git rebase main
git push --force-with-lease origin fix/typo-in-readme
```

---

## 🧪 Проверочные вопросы

1. В чем разница между HTTPS и SSH для подключения к Git?
2. Что такое remote tracking branch?
3. В чем разница между `git fetch` и `git pull`?
4. Когда безопасно использовать `git push --force`?
5. Что означает upstream ветка?
6. Как клонировать только последний коммит репозитория?
7. Как добавить несколько remote репозиториев?

## 📝 Домашнее задание

1. Создайте публичный репозиторий на GitHub
2. Настройте SSH ключи для доступа
3. Создайте локальный проект с несколькими файлами
4. Отправьте проект в удаленный репозиторий
5. Создайте feature ветку и внесите изменения
6. Отправьте feature ветку на GitHub
7. Сделайте Pull Request из feature ветки в main
8. Слейте Pull Request и удалите feature ветку
9. Обновите локальный main и удалите локальную feature ветку

## 🔧 Продвинутые задания

1. Настройте Git alias для часто используемых команд:
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.up 'pull --rebase'
git config --global alias.cm 'commit -m'
```

2. Настройте автоматический rebase при pull:
```bash
git config --global pull.rebase true
```

3. Создайте script для автоматической синхронизации всех веток с remote

---

## 🔗 Полезные ссылки

- [GitHub SSH Key Setup](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [Git Remote Branches](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches)
- [Git Tools - Advanced Merging](https://git-scm.com/book/en/v2/Git-Tools-Advanced-Merging)
- [GitHub Flow](https://guides.github.com/introduction/flow/)

**Время изучения блока: 3.5 часа** 