# Блок 7. Основы JavaScript - Методы массивов, Rest, деструктурирование (3.2 часа)

## 🎯 Цели блока

После изучения этого блока вы сможете:
- Работать с основными методами массивов
- Использовать rest и spread операторы
- Применять деструктурирование массивов и объектов
- Понимать разницу между мутирующими и немутирующими методами

---

## 📚 Теоретическая часть

### 1. Основные методы массивов

#### Методы добавления и удаления элементов:

```javascript
let fruits = ['apple', 'banana'];

// push() - добавляет элементы в конец (мутирует массив)
fruits.push('orange', 'grape');
console.log(fruits); // ['apple', 'banana', 'orange', 'grape']

// pop() - удаляет последний элемент (мутирует массив)
let lastFruit = fruits.pop();
console.log(lastFruit); // 'grape'
console.log(fruits); // ['apple', 'banana', 'orange']

// unshift() - добавляет элементы в начало (мутирует массив)
fruits.unshift('mango', 'kiwi');
console.log(fruits); // ['mango', 'kiwi', 'apple', 'banana', 'orange']

// shift() - удаляет первый элемент (мутирует массив)
let firstFruit = fruits.shift();
console.log(firstFruit); // 'mango'
console.log(fruits); // ['kiwi', 'apple', 'banana', 'orange']

// splice() - универсальный метод для добавления/удаления (мутирует массив)
let removed = fruits.splice(1, 2, 'pear', 'plum'); // начиная с индекса 1, удалить 2 элемента, добавить 'pear', 'plum'
console.log(removed); // ['apple', 'banana']
console.log(fruits); // ['kiwi', 'pear', 'plum', 'orange']

// slice() - создает копию части массива (НЕ мутирует)
let citrus = fruits.slice(1, 3); // от индекса 1 до 3 (не включая)
console.log(citrus); // ['pear', 'plum']
console.log(fruits); // ['kiwi', 'pear', 'plum', 'orange'] - не изменился
```

#### Методы поиска:

```javascript
let numbers = [1, 2, 3, 4, 5, 3, 6];

// indexOf() - первое вхождение элемента
console.log(numbers.indexOf(3)); // 2
console.log(numbers.indexOf(10)); // -1 (не найден)

// lastIndexOf() - последнее вхождение элемента
console.log(numbers.lastIndexOf(3)); // 5

// includes() - проверка наличия элемента
console.log(numbers.includes(4)); // true
console.log(numbers.includes(10)); // false

// find() - первый элемент, удовлетворяющий условию
let users = [
    { id: 1, name: 'John', age: 25 },
    { id: 2, name: 'Jane', age: 30 },
    { id: 3, name: 'Bob', age: 35 }
];

let user = users.find(u => u.age > 28);
console.log(user); // { id: 2, name: 'Jane', age: 30 }

// findIndex() - индекс первого элемента, удовлетворяющего условию
let index = users.findIndex(u => u.name === 'Bob');
console.log(index); // 2

// some() - проверка, есть ли элементы, удовлетворяющие условию
let hasAdults = users.some(u => u.age >= 18);
console.log(hasAdults); // true

// every() - проверка, все ли элементы удовлетворяют условию
let allAdults = users.every(u => u.age >= 18);
console.log(allAdults); // true
```

#### Методы преобразования:

```javascript
let numbers = [1, 2, 3, 4, 5];

// join() - объединение элементов в строку
console.log(numbers.join()); // "1,2,3,4,5"
console.log(numbers.join(' - ')); // "1 - 2 - 3 - 4 - 5"

// reverse() - переворачивает массив (мутирует!)
let reversed = [...numbers].reverse(); // создаем копию перед reverse
console.log(reversed); // [5, 4, 3, 2, 1]

// sort() - сортировка (мутирует!)
let words = ['banana', 'apple', 'cherry'];
let sortedWords = [...words].sort();
console.log(sortedWords); // ['apple', 'banana', 'cherry']

// Сортировка чисел (важно!)
let nums = [10, 5, 40, 25, 1000, 1];
let sortedNums = [...nums].sort((a, b) => a - b); // по возрастанию
console.log(sortedNums); // [1, 5, 10, 25, 40, 1000]

let sortedDesc = [...nums].sort((a, b) => b - a); // по убыванию
console.log(sortedDesc); // [1000, 40, 25, 10, 5, 1]

// concat() - объединение массивов (НЕ мутирует)
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = arr1.concat(arr2);
console.log(combined); // [1, 2, 3, 4, 5, 6]
```

### 2. Spread оператор (...)

Spread оператор "разворачивает" элементы массива или объекта.

```javascript
// Копирование массивов
let original = [1, 2, 3];
let copy = [...original];
console.log(copy); // [1, 2, 3]
console.log(copy === original); // false (разные объекты)

// Объединение массивов
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Добавление элементов
let numbers = [2, 3, 4];
let withMore = [1, ...numbers, 5, 6];
console.log(withMore); // [1, 2, 3, 4, 5, 6]

// Передача аргументов в функцию
function sum(a, b, c) {
    return a + b + c;
}

let nums = [1, 2, 3];
console.log(sum(...nums)); // 6

// Поиск максимального/минимального значения
let values = [5, 2, 8, 1, 9];
console.log(Math.max(...values)); // 9
console.log(Math.min(...values)); // 1

// Преобразование строки в массив символов
let str = "hello";
let chars = [...str];
console.log(chars); // ['h', 'e', 'l', 'l', 'o']

// Spread с объектами
let person = { name: 'John', age: 30 };
let employee = { ...person, position: 'Developer', salary: 50000 };
console.log(employee); // { name: 'John', age: 30, position: 'Developer', salary: 50000 }

// Обновление свойств объекта
let user = { id: 1, name: 'John', email: 'john@test.com' };
let updatedUser = { ...user, email: 'john.doe@test.com', isActive: true };
console.log(updatedUser); // { id: 1, name: 'John', email: 'john.doe@test.com', isActive: true }
```

### 3. Rest параметры (...)

Rest параметры собирают множество элементов в массив.

```javascript
// Rest в функциях
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4, 5)); // 15
console.log(sum(10, 20)); // 30

// Rest с обычными параметрами
function greet(greeting, ...names) {
    return `${greeting} ${names.join(', ')}!`;
}

console.log(greet('Hello', 'John', 'Jane', 'Bob')); // "Hello John, Jane, Bob!"

// Rest в деструктурировании массивов
let [first, second, ...rest] = [1, 2, 3, 4, 5];
console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3, 4, 5]

// Rest в деструктурировании объектов
let person = { name: 'John', age: 30, city: 'New York', country: 'USA' };
let { name, age, ...address } = person;
console.log(name); // 'John'
console.log(age); // 30
console.log(address); // { city: 'New York', country: 'USA' }

// Практический пример: функция логирования
function logger(level, message, ...details) {
    console.log(`[${level.toUpperCase()}] ${message}`);
    if (details.length > 0) {
        console.log('Details:', details);
    }
}

logger('info', 'User logged in', 'userId: 123', 'timestamp: 2023-01-01');
// [INFO] User logged in
// Details: ['userId: 123', 'timestamp: 2023-01-01']
```

### 4. Деструктурирование массивов

```javascript
// Базовое деструктурирование
let colors = ['red', 'green', 'blue'];
let [primary, secondary, tertiary] = colors;
console.log(primary); // 'red'
console.log(secondary); // 'green'
console.log(tertiary); // 'blue'

// Пропуск элементов
let [first, , third] = colors;
console.log(first); // 'red'
console.log(third); // 'blue'

// Значения по умолчанию
let [a, b, c, d = 'yellow'] = colors;
console.log(d); // 'yellow'

// Обмен значений переменных
let x = 1, y = 2;
[x, y] = [y, x];
console.log(x, y); // 2, 1

// Деструктурирование возвращаемых значений функции
function getCoordinates() {
    return [10, 20];
}

let [x_coord, y_coord] = getCoordinates();
console.log(x_coord, y_coord); // 10, 20

// Вложенное деструктурирование
let nested = [[1, 2], [3, 4]];
let [[a1, a2], [b1, b2]] = nested;
console.log(a1, a2, b1, b2); // 1, 2, 3, 4

// Деструктурирование в параметрах функции
function processPoint([x, y]) {
    return Math.sqrt(x * x + y * y);
}

console.log(processPoint([3, 4])); // 5

// Rest в деструктурировании
let numbers = [1, 2, 3, 4, 5];
let [head, ...tail] = numbers;
console.log(head); // 1
console.log(tail); // [2, 3, 4, 5]
```

### 5. Деструктурирование объектов

```javascript
// Базовое деструктурирование
let person = { name: 'John', age: 30, city: 'New York' };
let { name, age, city } = person;
console.log(name, age, city); // 'John', 30, 'New York'

// Переименование переменных
let { name: fullName, age: years } = person;
console.log(fullName, years); // 'John', 30

// Значения по умолчанию
let { name: userName, age: userAge, country = 'USA' } = person;
console.log(country); // 'USA'

// Вложенное деструктурирование
let user = {
    id: 1,
    profile: {
        name: 'John',
        contacts: {
            email: 'john@test.com',
            phone: '+1234567890'
        }
    }
};

let {
    profile: {
        name,
        contacts: { email, phone }
    }
} = user;

console.log(name, email, phone); // 'John', 'john@test.com', '+1234567890'

// Деструктурирование в параметрах функции
function createUser({ name, email, age = 18, role = 'user' }) {
    return {
        id: Date.now(),
        name,
        email,
        age,
        role,
        createdAt: new Date()
    };
}

let newUser = createUser({
    name: 'Jane',
    email: 'jane@test.com',
    age: 25
});

// Деструктурирование при итерации
let users = [
    { name: 'John', age: 30 },
    { name: 'Jane', age: 25 },
    { name: 'Bob', age: 35 }
];

users.forEach(({ name, age }) => {
    console.log(`${name} is ${age} years old`);
});

// Извлечение нужных свойств из объекта
function getPublicUserInfo({ name, email, ...privateData }) {
    return { name, email }; // возвращаем только публичную информацию
}

let userInfo = getPublicUserInfo({
    name: 'John',
    email: 'john@test.com',
    password: 'secret',
    ssn: '123-45-6789'
});

console.log(userInfo); // { name: 'John', email: 'john@test.com' }
```

### 6. Практические паттерны

```javascript
// Клонирование массивов и объектов
function deepClone(obj) {
    if (Array.isArray(obj)) {
        return obj.map(item => deepClone(item));
    } else if (typeof obj === 'object' && obj !== null) {
        return Object.keys(obj).reduce((clone, key) => {
            clone[key] = deepClone(obj[key]);
            return clone;
        }, {});
    }
    return obj;
}

// Слияние объектов с приоритетом
function mergeObjects(target, ...sources) {
    return sources.reduce((result, source) => {
        return { ...result, ...source };
    }, { ...target });
}

let config = { theme: 'light', language: 'en' };
let userPrefs = { theme: 'dark' };
let systemDefaults = { notifications: true };

let finalConfig = mergeObjects(config, userPrefs, systemDefaults);
console.log(finalConfig); // { theme: 'dark', language: 'en', notifications: true }

// Группировка массива объектов
function groupBy(array, keyGetter) {
    return array.reduce((groups, item) => {
        const key = keyGetter(item);
        if (!groups[key]) {
            groups[key] = [];
        }
        groups[key].push(item);
        return groups;
    }, {});
}

let products = [
    { name: 'Laptop', category: 'electronics', price: 1000 },
    { name: 'Phone', category: 'electronics', price: 500 },
    { name: 'Book', category: 'books', price: 20 },
    { name: 'Headphones', category: 'electronics', price: 100 }
];

let grouped = groupBy(products, product => product.category);
console.log(grouped);
// {
//   electronics: [{ name: 'Laptop', ... }, { name: 'Phone', ... }, { name: 'Headphones', ... }],
//   books: [{ name: 'Book', ... }]
// }

// Удаление дубликатов из массива
function removeDuplicates(array, keyGetter = item => item) {
    const seen = new Set();
    return array.filter(item => {
        const key = keyGetter(item);
        if (seen.has(key)) {
            return false;
        }
        seen.add(key);
        return true;
    });
}

let duplicates = [1, 2, 2, 3, 3, 3, 4];
console.log(removeDuplicates(duplicates)); // [1, 2, 3, 4]

let userDuplicates = [
    { id: 1, name: 'John' },
    { id: 2, name: 'Jane' },
    { id: 1, name: 'John' }
];
console.log(removeDuplicates(userDuplicates, user => user.id));
// [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }]
```

---

## 💻 Практические упражнения

### Упражнение 1: Основные методы массивов (45 минут)

```javascript
// 1. Работа с массивом задач
let tasks = [
    { id: 1, title: 'Изучить JavaScript', completed: false, priority: 'high' },
    { id: 2, title: 'Сделать покупки', completed: true, priority: 'medium' },
    { id: 3, title: 'Позвонить врачу', completed: false, priority: 'high' },
    { id: 4, title: 'Прочитать книгу', completed: false, priority: 'low' },
    { id: 5, title: 'Убрать дом', completed: true, priority: 'medium' }
];

// Реализуйте следующие функции:

function getCompletedTasks(tasks) {
    // Верните массив выполненных задач
}

function getHighPriorityTasks(tasks) {
    // Верните задачи с высоким приоритетом
}

function findTaskById(tasks, id) {
    // Найдите задачу по ID
}

function getTaskTitles(tasks) {
    // Верните массив названий всех задач
}

function hasIncompleteTasks(tasks) {
    // Проверьте, есть ли невыполненные задачи
}

function areAllTasksCompleted(tasks) {
    // Проверьте, все ли задачи выполнены
}

function sortTasksByPriority(tasks) {
    // Отсортируйте задачи по приоритету (high -> medium -> low)
    // Не мутируйте исходный массив
}

function getTaskStats(tasks) {
    // Верните объект со статистикой:
    // { total, completed, incomplete, byPriority: { high, medium, low } }
}

// 2. Работа с числовыми массивами
let numbers = [64, 34, 25, 12, 22, 11, 90, 5, 77, 30];

function getEvenNumbers(numbers) {
    // Верните четные числа
}

function getNumbersInRange(numbers, min, max) {
    // Верните числа в диапазоне от min до max (включительно)
}

function getUniqueNumbers(numbers) {
    // Удалите дубликаты из массива
}

function getNumbersSummary(numbers) {
    // Верните объект с min, max, sum, average
}

// Тестирование
console.log(getCompletedTasks(tasks));
console.log(getHighPriorityTasks(tasks));
console.log(findTaskById(tasks, 3));
console.log(getTaskTitles(tasks));
console.log(hasIncompleteTasks(tasks));
console.log(areAllTasksCompleted(tasks));
console.log(sortTasksByPriority(tasks));
console.log(getTaskStats(tasks));

console.log(getEvenNumbers(numbers));
console.log(getNumbersInRange(numbers, 20, 50));
console.log(getUniqueNumbers([1, 2, 2, 3, 3, 3, 4]));
console.log(getNumbersSummary(numbers));
```

### Упражнение 2: Spread и Rest операторы (50 минут)

```javascript
// 1. Функции с переменным количеством аргументов
function createShoppingList(store, ...items) {
    // Создайте объект списка покупок
    // { store: 'Магазин', items: [...], total: количество_товаров, createdAt: дата }
}

function combineArrays(...arrays) {
    // Объедините все переданные массивы в один
    // Удалите дубликаты
}

function findMinMax(...numbers) {
    // Найдите минимальное и максимальное значение
    // Верните объект { min, max, range }
}

// 2. Работа с объектами
function updateUser(user, updates) {
    // Обновите пользователя, не мутируя исходный объект
    // Добавьте поле updatedAt с текущей датой
}

function mergeConfigs(defaultConfig, ...configs) {
    // Слейте конфигурации с приоритетом (последние перезаписывают предыдущие)
    // Добавьте поле merged: true
}

function extractUserData(user) {
    // Извлеките name, email в отдельные переменные
    // Остальные данные поместите в объект otherData
    // Верните { name, email, otherData }
}

// 3. Клонирование и копирование
function deepCopyArray(arr) {
    // Создайте глубокую копию массива (включая вложенные объекты)
}

function shallowCopyObject(obj) {
    // Создайте поверхностную копию объекта
}

function addToArray(arr, ...newItems) {
    // Добавьте элементы в массив, не мутируя исходный
    // Верните новый массив
}

// Тестирование
console.log(createShoppingList('Пятерочка', 'молоко', 'хлеб', 'яйца'));
console.log(combineArrays([1, 2], [2, 3], [3, 4, 5]));
console.log(findMinMax(5, 2, 8, 1, 9, 3));

let user = { id: 1, name: 'John', email: 'john@test.com', age: 30 };
console.log(updateUser(user, { age: 31, city: 'Moscow' }));

let defaultConfig = { theme: 'light', language: 'en', notifications: true };
let userConfig = { theme: 'dark' };
let adminConfig = { debug: true };
console.log(mergeConfigs(defaultConfig, userConfig, adminConfig));

let fullUser = { 
    id: 1, 
    name: 'John', 
    email: 'john@test.com', 
    age: 30, 
    city: 'Moscow', 
    preferences: { theme: 'dark' } 
};
console.log(extractUserData(fullUser));

let nestedArray = [1, [2, 3], { a: 4, b: [5, 6] }];
console.log(deepCopyArray(nestedArray));

console.log(addToArray([1, 2, 3], 4, 5, 6));
```

### Упражнение 3: Деструктурирование (40 минут)

```javascript
// 1. Деструктурирование в функциях
function processOrder({ id, items, customer, shipping = {}, discount = 0 }) {
    // Извлеките данные о заказе и верните сводку
    // Используйте деструктурирование для извлечения:
    // - customer: { name, email }
    // - shipping: { address, method = 'standard' }
    // - первый товар из items
    
    // Верните объект с обработанными данными
}

function calculateDistance([x1, y1], [x2, y2]) {
    // Вычислите расстояние между двумя точками
    // Используйте деструктурирование параметров
}

function formatUserInfo({ name, email, profile: { age, city, country = 'Russia' } = {} }) {
    // Отформатируйте информацию о пользователе
    // Обработайте случай, когда profile может отсутствовать
}

// 2. Обмен и переназначение
function swapVariables(a, b) {
    // Поменяйте местами значения используя деструктурирование
    // Верните массив [b, a]
}

function getFirstAndLast(array) {
    // Извлеките первый и последний элементы массива
    // Верните объект { first, last, middle }
    // middle - все элементы между первым и последним
}

function parseFullName(fullName) {
    // Разберите полное имя "Иван Петров Сергеевич"
    // Верните { firstName, lastName, middleName }
    // Учтите, что отчество может отсутствовать
}

// 3. Работа с API данными
function processApiResponse(response) {
    // response = {
    //   data: {
    //     users: [...],
    //     pagination: { page, limit, total },
    //     meta: { timestamp, version }
    //   },
    //   status: 200,
    //   message: 'success'
    // }
    
    // Извлеките нужные данные используя деструктурирование
    // Верните { users, currentPage, totalPages, timestamp }
}

function extractConfigValues(config) {
    // config = {
    //   database: { host, port, name },
    //   server: { port: serverPort, host: serverHost },
    //   features: { auth, logging, caching }
    // }
    
    // Извлеките и переименуйте конфликтующие поля
    // Верните плоский объект со всеми настройками
}

// 4. Условное деструктурирование
function processUserArray(users) {
    // users - массив пользователей
    // Используя деструктурирование, извлеките:
    // - первого пользователя (admin)
    // - второго пользователя (moderator) 
    // - остальных пользователей (regularUsers)
    // Обработайте случаи, когда пользователей может быть меньше
}

// Тестовые данные
let order = {
    id: 'ORD-001',
    items: [
        { name: 'Laptop', price: 1000, quantity: 1 },
        { name: 'Mouse', price: 25, quantity: 2 }
    ],
    customer: { name: 'John Doe', email: 'john@test.com' },
    shipping: { address: 'Moscow, Red Square 1', method: 'express' },
    discount: 10
};

let user = {
    name: 'John',
    email: 'john@test.com',
    profile: {
        age: 30,
        city: 'Moscow'
    }
};

let apiResponse = {
    data: {
        users: [{ id: 1, name: 'John' }, { id: 2, name: 'Jane' }],
        pagination: { page: 1, limit: 10, total: 25 },
        meta: { timestamp: '2023-01-01T00:00:00Z', version: '1.0' }
    },
    status: 200,
    message: 'success'
};

// Тестирование
console.log(processOrder(order));
console.log(calculateDistance([0, 0], [3, 4]));
console.log(formatUserInfo(user));
console.log(swapVariables(5, 10));
console.log(getFirstAndLast([1, 2, 3, 4, 5]));
console.log(parseFullName('Иван Петров Сергеевич'));
console.log(processApiResponse(apiResponse));
```

### Упражнение 4: Комплексные задачи (37 минут)

```javascript
// 1. Система управления инвентарем
class InventoryManager {
    constructor() {
        this.items = [];
    }
    
    addItems(...newItems) {
        // Добавьте товары, используя spread
        // Каждый товар должен иметь уникальный ID
        // Если товар с таким именем уже есть, увеличьте количество
    }
    
    removeItems(...itemIds) {
        // Удалите товары по ID, используя rest параметры
        // Верните массив удаленных товаров
    }
    
    updateItem(id, updates) {
        // Обновите товар, не мутируя исходный объект
        // Используйте spread для создания нового объекта
    }
    
    getItemsByCategory(category) {
        // Верните товары определенной категории
        // Используйте деструктурирование в filter
    }
    
    getInventorySummary() {
        // Верните сводку: общее количество, стоимость, по категориям
        // Используйте деструктурирование для извлечения нужных полей
    }
    
    exportItems(...categories) {
        // Экспортируйте товары определенных категорий
        // Если категории не указаны, экспортируйте все
        // Используйте rest/spread операторы
    }
}

// 2. Обработчик форм
function createFormProcessor(defaultValues = {}) {
    return {
        process(formData, validationRules = {}) {
            // Обработайте данные формы
            // Слейте с значениями по умолчанию
            // Примените валидацию
            // Используйте деструктурирование для извлечения полей
        },
        
        validate({ required = [], patterns = {}, custom = {} } = {}) {
            // Валидируйте данные используя деструктурирование параметров
        },
        
        transform(data, transformers = {}) {
            // Примените трансформации к данным
            // transformers = { fieldName: transformFunction }
        }
    };
}

// 3. Утилиты для работы с данными
const DataUtils = {
    // Группировка массива по нескольким ключам
    groupByMultiple(array, ...keyGetters) {
        // Сгруппируйте массив по нескольким критериям
        // Используйте rest параметры для ключей группировки
    },
    
    // Плоское представление вложенного объекта
    flatten(obj, prefix = '') {
        // Преобразуйте { a: { b: { c: 1 } } } в { 'a.b.c': 1 }
        // Используйте деструктурирование и spread
    },
    
    // Восстановление структуры из плоского объекта
    unflatten(flatObj) {
        // Обратная операция для flatten
        // Используйте деструктурирование для разбора ключей
    },
    
    // Слияние массивов объектов по ключу
    mergeArraysByKey(key, ...arrays) {
        // Слейте массивы объектов, объединяя объекты с одинаковыми ключами
        // Используйте rest для получения массивов
    },
    
    // Извлечение уникальных значений по ключу
    uniqueBy(array, keyGetter) {
        // Оставьте только уникальные объекты по определенному ключу
        // Используйте деструктурирование в обработке
    }
};

// Тестирование
let inventory = new InventoryManager();

inventory.addItems(
    { name: 'Laptop', category: 'electronics', price: 1000, quantity: 5 },
    { name: 'Book', category: 'books', price: 20, quantity: 10 },
    { name: 'Phone', category: 'electronics', price: 500, quantity: 3 }
);

console.log(inventory.getItemsByCategory('electronics'));
console.log(inventory.getInventorySummary());

let formProcessor = createFormProcessor({ 
    country: 'Russia', 
    notifications: true 
});

let formData = {
    name: 'John',
    email: 'john@test.com',
    age: '30'
};

console.log(formProcessor.process(formData, {
    required: ['name', 'email'],
    patterns: { email: /\S+@\S+\.\S+/ }
}));

// Тестирование утилит
let users = [
    { id: 1, name: 'John', department: 'IT', role: 'developer' },
    { id: 2, name: 'Jane', department: 'IT', role: 'designer' },
    { id: 3, name: 'Bob', department: 'HR', role: 'manager' }
];

console.log(DataUtils.groupByMultiple(users, u => u.department, u => u.role));

let nested = { user: { profile: { name: 'John', age: 30 } }, settings: { theme: 'dark' } };
console.log(DataUtils.flatten(nested));

let flat = { 'user.profile.name': 'John', 'user.profile.age': 30, 'settings.theme': 'dark' };
console.log(DataUtils.unflatten(flat));
```

---

## 🧪 Проверочные вопросы

1. В чем разница между `push()` и `concat()`?
2. Какие методы массивов мутируют исходный массив?
3. В чем разница между spread и rest операторами?
4. Как поменять местами значения двух переменных используя деструктурирование?
5. Что произойдет при деструктурировании объекта с несуществующими свойствами?
6. Как использовать значения по умолчанию при деструктурировании?
7. В каких случаях полезно использовать rest параметры в функциях?

## 📝 Домашнее задание

Создайте систему управления студентами и курсами:

```javascript
// Система управления студентами
class StudentManager {
    constructor() {
        this.students = [];
        this.courses = [];
        this.enrollments = [];
    }
    
    // TODO: Реализуйте методы используя изученные концепции
    
    addStudents(...studentData) {
        // Добавьте студентов используя rest параметры
        // Каждый студент: { name, email, age, major }
        // Используйте spread для создания объектов с дополнительными полями
    }
    
    addCourses(...courseData) {
        // Добавьте курсы: { title, instructor, credits, prerequisites }
    }
    
    enrollStudent(studentId, ...courseIds) {
        // Запишите студента на курсы
        // Проверьте prerequisites
        // Используйте rest для courseIds
    }
    
    getStudentInfo(studentId) {
        // Верните полную информацию о студенте
        // Используйте деструктурирование для извлечения данных
        // Включите список курсов
    }
    
    getCourseStats(courseId) {
        // Статистика по курсу: количество студентов, средний возраст и т.д.
        // Используйте методы массивов и деструктурирование
    }
    
    getStudentsByMajor(...majors) {
        // Получите студентов по специальностям
        // Если majors пустой, верните всех студентов
    }
    
    updateStudent(studentId, updates) {
        // Обновите данные студента не мутируя исходный объект
        // Используйте spread оператор
    }
    
    generateReport() {
        // Сгенерируйте отчет используя все изученные методы
        // Группировка по специальностям, статистика по курсам и т.д.
    }
    
    exportData({ students = true, courses = true, enrollments = true } = {}) {
        // Экспортируйте данные используя деструктурирование параметров
        // Верните только запрошенные данные
    }
    
    importData({ students = [], courses = [], enrollments = [] }) {
        // Импортируйте данные используя деструктурирование
        // Слейте с существующими данными используя spread
    }
}

// Дополнительные утилиты
const StudentUtils = {
    // Создайте утилиты используя все изученные концепции:
    
    parseStudentData(csvString) {
        // Разберите CSV строку в массив объектов студентов
        // Используйте деструктурирование и spread
    },
    
    calculateGPA(grades) {
        // Рассчитайте средний балл из массива оценок
        // Используйте методы массивов
    },
    
    groupStudentsByYear(students) {
        // Сгруппируйте студентов по году поступления
    },
    
    findStudentConflicts(students) {
        // Найдите студентов с конфликтующими расписаниями
        // Используйте методы массивов и деструктурирование
    }
};

// Пример использования:
let manager = new StudentManager();

manager.addStudents(
    { name: 'John Doe', email: 'john@university.edu', age: 20, major: 'Computer Science' },
    { name: 'Jane Smith', email: 'jane@university.edu', age: 19, major: 'Mathematics' }
);

manager.addCourses(
    { title: 'JavaScript Fundamentals', instructor: 'Dr. Johnson', credits: 3, prerequisites: [] },
    { title: 'Advanced Algorithms', instructor: 'Prof. Smith', credits: 4, prerequisites: ['JavaScript Fundamentals'] }
);

manager.enrollStudent(1, 1, 2);
console.log(manager.getStudentInfo(1));
console.log(manager.generateReport());
```

---

## 🔗 Полезные ссылки

- [Array Methods - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Spread Operator - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Rest Parameters - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Destructuring Assignment - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

**Время изучения блока: 3.2 часа** 