# Блок 2. Основы Git - Ветки и слияние (3.5 часа)

## 🎯 Цели блока

После изучения этого блока вы сможете:
- Создавать и переключаться между ветками
- Выполнять слияние веток
- Понимать концепцию HEAD
- Работать с тегами
- Использовать rebase и cherry-pick

---

## 📚 Теоретическая часть

### 1. Ветки (Branches)

Ветки в Git позволяют работать над разными функциями параллельно, не затрагивая основную ветку.

#### Основные команды веток:
```bash
# Создание новой ветки
git branch feature-auth

# Переключение на ветку
git checkout feature-auth

# Создание и переключение одной командой
git checkout -b feature-auth

# Просмотр всех веток
git branch

# Просмотр веток с последними коммитами
git branch -v

# Удаление ветки
git branch -d feature-auth

# Принудительное удаление
git branch -D feature-auth
```

### 2. HEAD - указатель текущей позиции

HEAD - это указатель на текущий коммит или ветку.

```bash
# Посмотреть на что указывает HEAD
cat .git/HEAD

# Перемещение HEAD на конкретный коммит
git checkout abc123

# Возврат на ветку
git checkout main
```

### 3. Слияние веток (Merge)

#### Fast-forward merge
Происходит когда целевая ветка не имеет новых коммитов:

```bash
git checkout main
git merge feature-auth
```

#### Recursive merge (3-way merge)
Когда обе ветки имеют новые коммиты:

```bash
git checkout main
git merge feature-auth
```

#### Разрешение конфликтов:
```bash
# Посмотреть статус конфликта
git status

# После разрешения конфликтов
git add .
git commit -m "Resolve merge conflict"
```

### 4. Тэги (Tags)

Тэги используются для маркировки важных точек в истории проекта:

```bash
# Создание простого тэга
git tag v1.0

# Создание аннотированного тэга
git tag -a v1.0 -m "Version 1.0 release"

# Просмотр тэгов
git tag

# Просмотр информации о тэге
git show v1.0

# Удаление тэга
git tag -d v1.0

# Отправка тэгов на удаленный репозиторий
git push origin v1.0
git push origin --tags
```

### 5. Rebase - перебазирование

Rebase позволяет "пересадить" коммиты на другую ветку:

```bash
# Обычный rebase
git checkout feature-auth
git rebase main

# Интерактивный rebase (последние 3 коммита)
git rebase -i HEAD~3
```

#### Опции интерактивного rebase:
- `pick` - оставить коммит как есть
- `reword` - изменить сообщение коммита
- `edit` - остановиться для редактирования
- `squash` - объединить с предыдущим коммитом
- `drop` - удалить коммит

### 6. Cherry-pick - выборочное применение

Cherry-pick позволяет применить конкретный коммит из другой ветки:

```bash
# Применить конкретный коммит
git cherry-pick abc123

# Применить несколько коммитов
git cherry-pick abc123 def456

# Cherry-pick с редактированием сообщения
git cherry-pick -e abc123
```

---

## 💻 Практические упражнения

### Упражнение 1: Работа с ветками (30 минут)

1. Создайте новую ветку `feature-login`:
```bash
git checkout -b feature-login
```

2. Создайте файл `login.js` с содержимым:
```javascript
function login(username, password) {
    console.log(`Logging in user: ${username}`);
    return true;
}
```

3. Зафиксируйте изменения:
```bash
git add login.js
git commit -m "Add login function"
```

4. Переключитесь на main и создайте файл `app.js`:
```bash
git checkout main
echo "console.log('App started');" > app.js
git add app.js
git commit -m "Add app.js"
```

### Упражнение 2: Слияние веток (30 минут)

1. Слейте ветку `feature-login` в `main`:
```bash
git merge feature-login
```

2. Удалите ветку после слияния:
```bash
git branch -d feature-login
```

### Упражнение 3: Работа с конфликтами (45 минут)

1. Создайте две ветки с конфликтующими изменениями:
```bash
# Ветка 1
git checkout -b feature-a
echo "Feature A implementation" > feature.txt
git add feature.txt
git commit -m "Add feature A"

# Ветка 2
git checkout main
git checkout -b feature-b
echo "Feature B implementation" > feature.txt
git add feature.txt
git commit -m "Add feature B"
```

2. Попробуйте слить ветки и разрешите конфликт:
```bash
git checkout main
git merge feature-a
git merge feature-b
# Разрешите конфликт в файле feature.txt
git add feature.txt
git commit -m "Resolve conflict between feature A and B"
```

### Упражнение 4: Rebase (45 минут)

1. Создайте ветку и несколько коммитов:
```bash
git checkout -b feature-rebase
echo "Step 1" > steps.txt
git add steps.txt
git commit -m "Add step 1"

echo "Step 2" >> steps.txt
git add steps.txt
git commit -m "Add step 2"

echo "Step 3" >> steps.txt
git add steps.txt
git commit -m "Add step 3"
```

2. Выполните интерактивный rebase:
```bash
git rebase -i HEAD~3
```

3. Объедините коммиты в один (squash)

### Упражнение 5: Тэги (30 минут)

1. Создайте тэг для текущей версии:
```bash
git tag -a v1.0.0 -m "Initial release"
```

2. Создайте еще несколько коммитов и тэг:
```bash
echo "Bug fix" >> app.js
git add app.js
git commit -m "Fix critical bug"
git tag -a v1.0.1 -m "Bug fix release"
```

3. Посмотрите историю с тэгами:
```bash
git log --oneline --decorate
```

---

## 🧪 Проверочные вопросы

1. В чем разница между `git checkout -b` и `git branch`?
2. Что такое Fast-forward merge и когда он происходит?
3. Как разрешить конфликт слияния?
4. В чем разница между merge и rebase?
5. Когда использовать cherry-pick?
6. Что такое HEAD в Git?
7. Как создать аннотированный тэг?

## 📝 Домашнее задание

1. Создайте репозиторий с файлом README.md
2. Создайте ветку `develop` и добавьте файл `config.js`
3. Создайте ветку `feature/authentication` от `develop`
4. Добавьте функцию аутентификации в отдельном файле
5. Слейте `feature/authentication` в `develop`
6. Создайте тэг `v0.1.0` для ветки `develop`
7. Слейте `develop` в `main`
8. Создайте тэг `v1.0.0` для релиза

---

## 🔗 Полезные ссылки

- [Git Branching - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
- [Git Tools - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
- [Git Basics - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

**Время изучения блока: 3.5 часа** 