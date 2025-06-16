# Блок 5. Основы JavaScript - Условные операторы (3.2 часа)

## 🎯 Цели блока

После изучения этого блока вы сможете:
- Использовать if/else конструкции
- Применять логические операторы эффективно
- Работать с switch-case
- Использовать тернарные операторы
- Понимать принципы короткого замыкания

---

## 📚 Теоретическая часть

### 1. Условный оператор if/else

Базовая конструкция для принятия решений в коде.

```javascript
// Простое условие
let age = 18;

if (age >= 18) {
    console.log("Вы совершеннолетний");
}

// Условие с else
if (age >= 18) {
    console.log("Вы совершеннолетний");
} else {
    console.log("Вы несовершеннолетний");
}

// Множественные условия (else if)
if (age < 13) {
    console.log("Ребенок");
} else if (age < 18) {
    console.log("Подросток");
} else if (age < 65) {
    console.log("Взрослый");
} else {
    console.log("Пожилой");
}

// Вложенные условия
let hasLicense = true;
let hasExperience = true;

if (age >= 18) {
    if (hasLicense) {
        if (hasExperience) {
            console.log("Можете водить автомобиль");
        } else {
            console.log("Нужен опыт вождения");
        }
    } else {
        console.log("Нужны права");
    }
} else {
    console.log("Слишком молоды для вождения");
}
```

### 2. Логические операторы

#### Логическое И (&&)
```javascript
let username = "john";
let password = "12345";

// Оба условия должны быть true
if (username === "john" && password === "12345") {
    console.log("Вход выполнен успешно");
}

// Короткое замыкание с &&
let user = { name: "John" };
user && user.name && console.log(user.name); // Безопасное обращение

// Присваивание с &&
let isLoggedIn = true;
let welcomeMessage = isLoggedIn && "Добро пожаловать!";
console.log(welcomeMessage); // "Добро пожаловать!"
```

#### Логическое ИЛИ (||)
```javascript
let role = "guest";

// Одно из условий должно быть true
if (role === "admin" || role === "moderator") {
    console.log("У вас есть права администратора");
}

// Значение по умолчанию с ||
let userName = "" || "Гость";
console.log(userName); // "Гость"

let config = {
    theme: undefined,
    language: "ru"
};

let theme = config.theme || "light";
let language = config.language || "en";
```

#### Логическое НЕ (!)
```javascript
let isVisible = false;

if (!isVisible) {
    console.log("Элемент скрыт");
}

// Преобразование в boolean
let value = "hello";
console.log(!value);  // false
console.log(!!value); // true (двойное отрицание)

// Проверка на существование
let data = null;
if (!data) {
    console.log("Данные отсутствуют");
}
```

### 3. Оператор switch

Альтернатива множественным if-else для сравнения одного значения.

```javascript
let dayOfWeek = 3;
let dayName;

switch (dayOfWeek) {
    case 1:
        dayName = "Понедельник";
        break;
    case 2:
        dayName = "Вторник";
        break;
    case 3:
        dayName = "Среда";
        break;
    case 4:
        dayName = "Четверг";
        break;
    case 5:
        dayName = "Пятница";
        break;
    case 6:
    case 7:
        dayName = "Выходной";
        break;
    default:
        dayName = "Неизвестный день";
}

console.log(dayName); // "Среда"

// Switch с выражениями
let operation = "+";
let a = 10, b = 5;
let result;

switch (operation) {
    case "+":
        result = a + b;
        break;
    case "-":
        result = a - b;
        break;
    case "*":
        result = a * b;
        break;
    case "/":
        result = b !== 0 ? a / b : "Деление на ноль!";
        break;
    default:
        result = "Неизвестная операция";
}

// Switch без break (fall-through)
let grade = "B";

switch (grade) {
    case "A":
        console.log("Отлично!");
        // fall-through
    case "B":
        console.log("Хорошо!");
        // fall-through
    case "C":
        console.log("Зачтено");
        break;
    case "D":
    case "F":
        console.log("Не зачтено");
        break;
    default:
        console.log("Неизвестная оценка");
}
```

### 4. Тернарный оператор

Краткая форма условного оператора.

```javascript
// Базовый синтаксис: условие ? значение_если_true : значение_если_false

let age = 20;
let status = age >= 18 ? "взрослый" : "несовершеннолетний";
console.log(status); // "взрослый"

// Вложенные тернарные операторы
let score = 85;
let grade = score >= 90 ? "A" : 
           score >= 80 ? "B" : 
           score >= 70 ? "C" : 
           score >= 60 ? "D" : "F";

// Тернарный оператор в функциях
function getDiscount(isVIP) {
    return isVIP ? 0.2 : 0.05;
}

// Тернарный оператор с выражениями
let items = [1, 2, 3];
let message = items.length > 0 ? `У вас ${items.length} товаров` : "Корзина пуста";

// Присваивание значений
let user = { name: "John", isAdmin: true };
let welcomeText = user.isAdmin ? `Добро пожаловать, администратор ${user.name}!` : `Привет, ${user.name}!`;
```

### 5. Короткое замыкание (Short-circuit evaluation)

JavaScript вычисляет логические выражения слева направо и останавливается, как только результат становится очевидным.

```javascript
// Короткое замыкание с &&
function expensiveOperation() {
    console.log("Выполняется дорогая операция");
    return true;
}

let shouldExecute = false;
shouldExecute && expensiveOperation(); // expensiveOperation не вызовется

// Практическое применение &&
let user = { name: "John" };
user && user.name && console.log(`Привет, ${user.name}!`);

// Короткое замыкание с ||
let cachedValue = null;
function getValue() {
    console.log("Получение значения...");
    return "новое значение";
}

let value = cachedValue || getValue(); // getValue вызовется только если cachedValue falsy

// Цепочка значений по умолчанию
let config = {};
let theme = config.theme || localStorage.getItem('theme') || 'light';

// Условное выполнение
let isDebug = true;
isDebug && console.log("Debug информация");

// Присваивание с проверкой
let data = null;
let processedData = data && data.map(item => item.value);
```

### 6. Truthy и Falsy значения

В JavaScript некоторые значения при преобразовании в boolean становятся false.

```javascript
// Falsy значения (все остальные - truthy)
let falsyValues = [
    false,      // boolean false
    0,          // число ноль
    -0,         // отрицательный ноль
    0n,         // BigInt ноль
    "",         // пустая строка
    null,       // null
    undefined,  // undefined
    NaN         // Not a Number
];

// Проверка на truthy/falsy
function checkValue(value) {
    if (value) {
        console.log(`${value} является truthy`);
    } else {
        console.log(`${value} является falsy`);
    }
}

// Примеры truthy значений
let truthyValues = [
    true,           // boolean true
    1,              // любое ненулевое число
    "0",            // непустая строка (даже "0")
    "false",        // непустая строка
    [],             // пустой массив
    {},             // пустой объект
    function(){}    // функция
];
```

---

## 💻 Практические упражнения

### Упражнение 1: Основные условия (45 минут)

```javascript
// 1. Система оценок
function getGradeInfo(score) {
    // Реализуйте функцию, которая:
    // 90-100: "Отлично (A)"
    // 80-89: "Хорошо (B)" 
    // 70-79: "Удовлетворительно (C)"
    // 60-69: "Слабо (D)"
    // 0-59: "Неудовлетворительно (F)"
    // Некорректный ввод: "Ошибка: оценка должна быть от 0 до 100"
}

// 2. Проверка возраста для разных активностей
function checkAgePermissions(age) {
    let permissions = {
        canVote: false,
        canDrink: false,
        canDrive: false,
        canRetire: false
    };
    
    // Установите права на основе возраста:
    // Голосование: 18+
    // Вождение: 16+
    // Алкоголь: 21+
    // Пенсия: 65+
    
    return permissions;
}

// 3. Калькулятор скидок
function calculateDiscount(price, customerType, purchaseAmount) {
    // VIP клиенты: 20% скидка
    // Постоянные клиенты: 10% скидка
    // Новые клиенты: 5% скидка
    // Дополнительная скидка 5% при покупке свыше 1000₽
    // Максимальная скидка не может превышать 25%
}

// Тестирование
console.log(getGradeInfo(95));  // "Отлично (A)"
console.log(getGradeInfo(75));  // "Удовлетворительно (C)"
console.log(getGradeInfo(101)); // "Ошибка: оценка должна быть от 0 до 100"

console.log(checkAgePermissions(17)); // {canVote: false, canDrink: false, canDrive: true, canRetire: false}
console.log(checkAgePermissions(25)); // {canVote: true, canDrink: true, canDrive: true, canRetire: false}

console.log(calculateDiscount(500, "VIP", 500));    // 20% скидка
console.log(calculateDiscount(1200, "new", 1200));  // 10% скидка (5% + 5% за сумму)
```

### Упражнение 2: Switch и сложные условия (50 минут)

```javascript
// 1. Калькулятор
function calculator(num1, operator, num2) {
    // Используйте switch для операций: +, -, *, /, %, **
    // Обработайте деление на ноль
    // Верните объект с результатом и сообщением
}

// 2. Определение времени года и рекомендаций
function getSeasonInfo(month, day) {
    // Используйте switch для определения времени года
    // Добавьте особые случаи (например, первый день года, праздники)
    // Верните объект с информацией о сезоне и рекомендациями
}

// 3. Система статусов заказа
function getOrderStatus(status) {
    switch (status) {
        // Реализуйте статусы:
        // "pending": "Заказ ожидает обработки"
        // "processing": "Заказ обрабатывается"
        // "shipped": "Заказ отправлен"
        // "delivered": "Заказ доставлен"
        // "cancelled": "Заказ отменен"
        // "refunded": "Возврат оформлен"
        // Для статусов "shipped" и "delivered" добавьте информацию о трекинге
    }
}

// 4. Игра "Камень, ножницы, бумага"
function rockPaperScissors(player1, player2) {
    // Реализуйте логику игры используя switch
    // Верните результат: "Player 1 wins", "Player 2 wins", "Draw"
}

// Тестирование
console.log(calculator(10, "+", 5));   // {result: 15, message: "Операция выполнена успешно"}
console.log(calculator(10, "/", 0));   // {result: null, message: "Деление на ноль невозможно"}

console.log(getSeasonInfo(12, 31));    // Информация о зиме и новогодних рекомендациях
console.log(getSeasonInfo(6, 15));     // Информация о лете

console.log(rockPaperScissors("rock", "scissors")); // "Player 1 wins"
```

### Упражнение 3: Тернарные операторы и короткое замыкание (40 минут)

```javascript
// 1. Форматирование сообщений
function formatMessage(user, messageCount) {
    // Используйте тернарные операторы для:
    // - Проверки существования пользователя
    // - Формирования правильной формы слова "сообщение/сообщения/сообщений"
    // - Определения статуса пользователя (онлайн/офлайн)
    
    let userName = user?.name || "Гость";
    let status = user?.isOnline ? "онлайн" : "офлайн";
    let messageForm = messageCount === 1 ? "сообщение" : 
                     messageCount < 5 ? "сообщения" : "сообщений";
    
    return `${userName} (${status}): ${messageCount} ${messageForm}`;
}

// 2. Безопасное получение вложенных свойств
function safeGet(obj, path) {
    // Используйте короткое замыкание для безопасного доступа
    // path - строка вида "user.profile.avatar.url"
    // Верните значение или undefined, если путь не существует
    
    let keys = path.split('.');
    let current = obj;
    
    // Реализуйте логику с использованием && для безопасного доступа
}

// 3. Система уведомлений
function createNotification(type, message, options = {}) {
    // Используйте тернарные операторы и || для значений по умолчанию
    let title = options.title || (type === "error" ? "Ошибка" : 
                                 type === "warning" ? "Предупреждение" : 
                                 type === "success" ? "Успех" : "Уведомление");
    
    let icon = options.icon || (type === "error" ? "❌" : 
                               type === "warning" ? "⚠️" : 
                               type === "success" ? "✅" : "ℹ️");
    
    let duration = options.duration || (type === "error" ? 5000 : 3000);
    
    return {
        title: title,
        message: message,
        icon: icon,
        duration: duration,
        timestamp: new Date().toISOString()
    };
}

// 4. Валидация данных формы
function validateForm(formData) {
    let errors = [];
    
    // Используйте короткое замыкание для проверок
    !formData.email && errors.push("Email обязателен");
    !formData.password && errors.push("Пароль обязателен");
    formData.password && formData.password.length < 6 && errors.push("Пароль должен содержать минимум 6 символов");
    formData.email && !/\S+@\S+\.\S+/.test(formData.email) && errors.push("Некорректный email");
    
    return {
        isValid: errors.length === 0,
        errors: errors
    };
}

// Тестирование
let user1 = { name: "John", isOnline: true };
let user2 = null;

console.log(formatMessage(user1, 1));  // "John (онлайн): 1 сообщение"
console.log(formatMessage(user2, 5));  // "Гость (офлайн): 5 сообщений"

let testObj = { user: { profile: { avatar: { url: "avatar.jpg" } } } };
console.log(safeGet(testObj, "user.profile.avatar.url")); // "avatar.jpg"
console.log(safeGet(testObj, "user.settings.theme"));     // undefined

console.log(createNotification("error", "Что-то пошло не так"));
console.log(createNotification("success", "Операция выполнена", { duration: 2000 }));

console.log(validateForm({ email: "test@test.com", password: "123456" })); // {isValid: true, errors: []}
console.log(validateForm({ email: "invalid", password: "123" }));          // {isValid: false, errors: [...]}
```

### Упражнение 4: Комплексные условия (37 минут)

```javascript
// 1. Система доступа к ресурсам
function checkAccess(user, resource, action) {
    // Проверьте доступ на основе:
    // - Роль пользователя (admin, moderator, user, guest)
    // - Тип ресурса (post, comment, user_profile, admin_panel)
    // - Действие (read, write, delete, create)
    // - Владение ресурсом (пользователь является автором)
    
    // Правила доступа:
    // - admin: полный доступ ко всему
    // - moderator: может читать всё, редактировать посты и комментарии, удалять комментарии
    // - user: может читать всё, создавать посты/комментарии, редактировать свои посты/комментарии
    // - guest: только чтение постов и комментариев
}

// 2. Расчет стоимости доставки
function calculateShipping(order) {
    // Параметры: weight, distance, isPriority, isFragile, destination
    // Правила:
    // - Базовая стоимость: 100₽
    // - За каждый кг свыше 1кг: +50₽
    // - За каждые 100км свыше 500км: +100₽
    // - Приоритетная доставка: +200₽
    // - Хрупкий груз: +150₽
    // - Международная доставка: +500₽
    // - Бесплатная доставка при заказе свыше 5000₽ (кроме международной)
}

// Тестирование
let adminUser = { id: 1, role: "admin", name: "Admin" };
let regularUser = { id: 2, role: "user", name: "John" };
let guestUser = { id: 3, role: "guest", name: "Guest" };

let post = { id: 1, authorId: 2, title: "Test Post" };

console.log(checkAccess(adminUser, post, "delete"));   // true
console.log(checkAccess(regularUser, post, "delete"));  // true (own post)
console.log(checkAccess(guestUser, post, "read"));     // true
console.log(checkAccess(guestUser, post, "write"));    // false

let order1 = { weight: 0.5, distance: 300, isPriority: false, isFragile: false, destination: "domestic", total: 1000 };
let order2 = { weight: 3, distance: 800, isPriority: true, isFragile: true, destination: "international", total: 6000 };

console.log(calculateShipping(order1)); // 100₽
console.log(calculateShipping(order2)); // Рассчитайте самостоятельно
```

---

## 🧪 Проверочные вопросы

1. В чем разница между `==` и `===`?
2. Какие значения являются falsy в JavaScript?
3. Что такое короткое замыкание и как оно работает?
4. Когда использовать switch вместо if-else?
5. Как работает тернарный оператор с вложенными условиями?
6. Почему важно использовать `break` в switch?
7. Что произойдет при выполнении `null && someFunction()`?

## 📝 Домашнее задание

Создайте систему управления библиотекой:

```javascript
// Система управления библиотекой
class LibrarySystem {
    constructor() {
        this.books = [];
        this.users = [];
        this.loans = [];
    }
    
    // TODO: Реализуйте методы с использованием изученных условных операторов
    
    addBook(book) {
        // Проверка на обязательные поля
        // Проверка на дубликаты по ISBN
    }
    
    registerUser(user) {
        // Валидация данных пользователя
        // Определение типа пользователя (student, teacher, regular)
    }
    
    loanBook(userId, bookId) {
        // Проверка существования пользователя и книги
        // Проверка доступности книги
        // Проверка лимитов пользователя
        // Расчет срока возврата в зависимости от типа пользователя
    }
    
    returnBook(loanId) {
        // Проверка существования займа
        // Расчет штрафа за просрочку
        // Обновление статусов
    }
    
    getUserStatus(userId) {
        // Определение статуса пользователя
        // Подсчет активных займов
        // Расчет общей задолженности
    }
}

// Пример использования:
let library = new LibrarySystem();

library.addBook({
    isbn: "978-5-17-123456-7",
    title: "JavaScript для начинающих",
    author: "Иванов И.И.",
    genre: "programming",
    copies: 3
});

library.registerUser({
    id: 1,
    name: "Петр Петров",
    email: "petr@example.com",
    type: "student",
    faculty: "IT"
});
```

---

## 🔗 Полезные ссылки

- [Conditional Statements - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- [Logical Operators - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators)
- [Switch Statement - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)
- [Conditional Operator - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

**Время изучения блока: 3.2 часа** 