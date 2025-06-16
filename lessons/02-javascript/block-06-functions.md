# Блок 6. Основы JavaScript - Функции (3.2 часа)

## 🎯 Цели блока

После изучения этого блока вы сможете:
- Создавать и использовать функции разными способами
- Понимать различия между function declaration и function expression
- Работать с стрелочными функциями
- Использовать функции высшего порядка
- Понимать область видимости и замыкания

---

## 📚 Теоретическая часть

### 1. Объявление функций (Function Declaration)

Самый базовый способ создания функций.

```javascript
// Простая функция
function greet() {
    console.log("Привет!");
}

greet(); // "Привет!"

// Функция с параметрами
function greetUser(name) {
    console.log(`Привет, ${name}!`);
}

greetUser("Анна"); // "Привет, Анна!"

// Функция с возвращаемым значением
function add(a, b) {
    return a + b;
}

let result = add(5, 3);
console.log(result); // 8

// Функция с несколькими параметрами и значениями по умолчанию
function createUser(name, age = 18, role = "user") {
    return {
        name: name,
        age: age,
        role: role,
        createdAt: new Date()
    };
}

console.log(createUser("Иван"));                    // age: 18, role: "user"
console.log(createUser("Мария", 25));               // age: 25, role: "user"  
console.log(createUser("Петр", 30, "admin"));       // age: 30, role: "admin"

// Ранний возврат
function checkAccess(user) {
    if (!user) {
        return false;
    }
    
    if (!user.isActive) {
        return false;
    }
    
    if (user.role !== "admin" && user.role !== "user") {
        return false;
    }
    
    return true;
}
```

### 2. Функциональные выражения (Function Expression)

Функции как значения переменных.

```javascript
// Анонимная функция в переменной
let sayHello = function() {
    console.log("Hello!");
};

sayHello(); // "Hello!"

// Именованное функциональное выражение
let factorial = function fact(n) {
    return n <= 1 ? 1 : n * fact(n - 1);
};

console.log(factorial(5)); // 120

// Различие между function declaration и function expression
console.log(typeof declaredFunction); // "function" - работает из-за hoisting
console.log(typeof expressedFunction); // "undefined" - еще не объявлена

function declaredFunction() {
    return "Я объявлена через declaration";
}

var expressedFunction = function() {
    return "Я объявлена через expression";
};

// Условное создание функций
let shouldUseAdvanced = true;

let processor;
if (shouldUseAdvanced) {
    processor = function(data) {
        // Сложная обработка
        return data.map(item => item * 2).filter(item => item > 10);
    };
} else {
    processor = function(data) {
        // Простая обработка
        return data.map(item => item + 1);
    };
}
```

### 3. Стрелочные функции (Arrow Functions)

Современный синтаксис для создания функций.

```javascript
// Базовый синтаксис
let add = (a, b) => a + b;
console.log(add(2, 3)); // 5

// Различные варианты записи
let square = x => x * x;              // Один параметр - скобки не нужны
let greet = () => console.log("Hi!"); // Без параметров
let multiply = (a, b) => a * b;       // Несколько параметров

// Блочное тело функции
let processUser = (user) => {
    if (!user.name) {
        throw new Error("Имя обязательно");
    }
    
    return {
        id: Date.now(),
        name: user.name.trim(),
        email: user.email?.toLowerCase(),
        createdAt: new Date()
    };
};

// Возврат объекта (нужны скобки)
let createPoint = (x, y) => ({ x: x, y: y });
let createPerson = (name, age) => ({
    name,
    age,
    toString: () => `${name}, ${age} лет`
});

// Стрелочные функции в методах массивов
let numbers = [1, 2, 3, 4, 5];

let doubled = numbers.map(n => n * 2);
let evens = numbers.filter(n => n % 2 === 0);
let sum = numbers.reduce((acc, n) => acc + n, 0);

console.log(doubled); // [2, 4, 6, 8, 10]
console.log(evens);   // [2, 4]
console.log(sum);     // 15

// Различия с обычными функциями (this)
let obj = {
    name: "Test",
    
    regularFunction: function() {
        console.log(this.name); // "Test"
    },
    
    arrowFunction: () => {
        console.log(this.name); // undefined (this не привязан)
    },
    
    methodWithArrow: function() {
        let inner = () => {
            console.log(this.name); // "Test" (наследует this от родительской функции)
        };
        inner();
    }
};
```

### 4. Функции высшего порядка

Функции, которые принимают другие функции как параметры или возвращают функции.

```javascript
// Функция принимает другую функцию как параметр
function processArray(array, callback) {
    let result = [];
    for (let i = 0; i < array.length; i++) {
        result.push(callback(array[i], i));
    }
    return result;
}

let numbers = [1, 2, 3, 4, 5];
let doubled = processArray(numbers, (x) => x * 2);
let indexed = processArray(numbers, (x, i) => `${i}: ${x}`);

console.log(doubled); // [2, 4, 6, 8, 10]
console.log(indexed); // ["0: 1", "1: 2", "2: 3", "3: 4", "4: 5"]

// Функция возвращает другую функцию
function createMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

let double = createMultiplier(2);
let triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(4)); // 12

// Фабрика функций-валидаторов
function createValidator(rule) {
    switch (rule) {
        case 'email':
            return (value) => /\S+@\S+\.\S+/.test(value);
        case 'phone':
            return (value) => /^\+?\d{10,15}$/.test(value);
        case 'minLength':
            return (minLength) => (value) => value.length >= minLength;
        default:
            return () => true;
    }
}

let emailValidator = createValidator('email');
let phoneValidator = createValidator('phone');
let passwordValidator = createValidator('minLength')(8);

console.log(emailValidator('test@test.com')); // true
console.log(phoneValidator('+1234567890'));   // true
console.log(passwordValidator('12345678'));   // true

// Композиция функций
function compose(f, g) {
    return function(x) {
        return f(g(x));
    };
}

let addOne = x => x + 1;
let multiplyByTwo = x => x * 2;
let addOneThenDouble = compose(multiplyByTwo, addOne);

console.log(addOneThenDouble(3)); // 8 ((3 + 1) * 2)

// Каррирование (currying)
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn.apply(this, args);
        } else {
            return function(...nextArgs) {
                return curried.apply(this, args.concat(nextArgs));
            };
        }
    };
}

let add3Numbers = (a, b, c) => a + b + c;
let curriedAdd = curry(add3Numbers);

console.log(curriedAdd(1)(2)(3)); // 6
console.log(curriedAdd(1, 2)(3)); // 6
console.log(curriedAdd(1)(2, 3)); // 6
```

### 5. Область видимости и замыкания

```javascript
// Глобальная область видимости
let globalVar = "Я глобальная";

function outerFunction() {
    // Локальная область видимости функции
    let outerVar = "Я из внешней функции";
    
    function innerFunction() {
        // Вложенная область видимости
        let innerVar = "Я из внутренней функции";
        
        console.log(globalVar); // Доступ к глобальной переменной
        console.log(outerVar);  // Доступ к переменной внешней функции
        console.log(innerVar);  // Доступ к локальной переменной
    }
    
    innerFunction();
    // console.log(innerVar); // Ошибка! innerVar недоступна здесь
}

// Замыкание (closure)
function createCounter() {
    let count = 0;
    
    return function() {
        count++;
        return count;
    };
}

let counter1 = createCounter();
let counter2 = createCounter();

console.log(counter1()); // 1
console.log(counter1()); // 2
console.log(counter2()); // 1 (независимый счетчик)
console.log(counter1()); // 3

// Практическое применение замыканий
function createBankAccount(initialBalance) {
    let balance = initialBalance;
    let transactionHistory = [];
    
    return {
        deposit: function(amount) {
            if (amount > 0) {
                balance += amount;
                transactionHistory.push({ type: 'deposit', amount, balance });
                return balance;
            }
            throw new Error('Сумма должна быть положительной');
        },
        
        withdraw: function(amount) {
            if (amount > 0 && amount <= balance) {
                balance -= amount;
                transactionHistory.push({ type: 'withdraw', amount, balance });
                return balance;
            }
            throw new Error('Недостаточно средств или некорректная сумма');
        },
        
        getBalance: function() {
            return balance;
        },
        
        getHistory: function() {
            return [...transactionHistory]; // Возвращаем копию
        }
    };
}

let account = createBankAccount(1000);
console.log(account.deposit(500)); // 1500
console.log(account.withdraw(200)); // 1300
console.log(account.getHistory());
// console.log(balance); // Ошибка! balance недоступна извне
```

### 6. Параметры функций

```javascript
// Rest параметры
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4, 5)); // 15
console.log(sum(10, 20));        // 30

// Destructuring параметров
function createUser({ name, email, age = 18, role = 'user' }) {
    return {
        id: Date.now(),
        name,
        email,
        age,
        role,
        isActive: true
    };
}

let newUser = createUser({
    name: "Анна",
    email: "anna@test.com",
    age: 25
});

// Смешанные параметры
function processData(requiredParam, { option1 = 'default', option2 } = {}, ...extraData) {
    console.log('Required:', requiredParam);
    console.log('Options:', { option1, option2 });
    console.log('Extra:', extraData);
}

processData('test', { option2: 'value' }, 'extra1', 'extra2');

// Функции как параметры с значениями по умолчанию
function processItems(items, transform = (x) => x, filter = () => true) {
    return items
        .filter(filter)
        .map(transform);
}

let data = [1, 2, 3, 4, 5];
console.log(processItems(data)); // [1, 2, 3, 4, 5]
console.log(processItems(data, x => x * 2)); // [2, 4, 6, 8, 10]
console.log(processItems(data, x => x * 2, x => x % 2 === 0)); // [4, 8]
```

---

## 💻 Практические упражнения

### Упражнение 1: Основы функций (45 минут)

```javascript
// 1. Создайте функцию для валидации email
function validateEmail(email) {
    // Проверьте, что email содержит @ и точку
    // Верните объект с результатом и сообщением
}

// 2. Функция для форматирования имени
function formatName(firstName, lastName, middleName) {
    // Верните отформатированное имя в формате "Фамилия И.О."
    // Учтите, что middleName может отсутствовать
}

// 3. Калькулятор процентов
function calculatePercentage(value, percentage, operation = 'add') {
    // operation может быть 'add' или 'subtract'
    // Верните результат вычисления
}

// 4. Функция для генерации случайного числа в диапазоне
function randomInRange(min, max, isInteger = true) {
    // Генерируйте случайное число от min до max
    // isInteger определяет, нужно ли округлять до целого
}

// 5. Функция проверки силы пароля
function checkPasswordStrength(password) {
    // Проверьте пароль на:
    // - Минимальную длину (8 символов)
    // - Наличие заглавных букв
    // - Наличие цифр
    // - Наличие специальных символов
    // Верните объект с оценкой силы и рекомендациями
}

// Тестирование
console.log(validateEmail('test@example.com'));
console.log(formatName('Иван', 'Петров', 'Сергеевич'));
console.log(calculatePercentage(1000, 15, 'add'));
console.log(randomInRange(1, 10));
console.log(checkPasswordStrength('MyPass123!'));
```

### Упражнение 2: Стрелочные функции и функции высшего порядка (50 минут)

```javascript
// 1. Переписать функции в стрелочном стиле
// Обычные функции для переписывания:
function double(x) { return x * 2; }
function isEven(n) { return n % 2 === 0; }
function createGreeting(name) { return `Hello, ${name}!`; }

// Перепишите их как стрелочные функции

// 2. Работа с массивами и стрелочными функциями
let products = [
    { name: 'Laptop', price: 1000, category: 'electronics', inStock: true },
    { name: 'Phone', price: 500, category: 'electronics', inStock: false },
    { name: 'Book', price: 20, category: 'books', inStock: true },
    { name: 'Headphones', price: 100, category: 'electronics', inStock: true }
];

// Используя методы массивов и стрелочные функции:
let availableProducts = // Получите товары в наличии
let expensiveProducts = // Получите товары дороже 50
let productNames = // Получите массив названий товаров
let totalValue = // Подсчитайте общую стоимость товаров в наличии
let groupedByCategory = // Сгруппируйте товары по категориям

// 3. Создание функций высшего порядка
function createFilter(property, value) {
    // Верните функцию, которая фильтрует объекты по свойству
}

function createSorter(property, direction = 'asc') {
    // Верните функцию для сортировки по свойству
    // direction может быть 'asc' или 'desc'
}

function createMapper(transform) {
    // Верните функцию, которая применяет transform к каждому элементу
}

// 4. Композиция функций
let pipe = (...functions) => {
    // Создайте функцию, которая применяет функции последовательно
    // pipe(f1, f2, f3)(x) должно быть равно f3(f2(f1(x)))
};

// Пример использования:
let addOne = x => x + 1;
let double = x => x * 2;
let square = x => x * x;

let complexTransform = pipe(addOne, double, square);
console.log(complexTransform(2)); // ((2+1)*2)^2 = 36

// Тестирование
let electronicsFilter = createFilter('category', 'electronics');
let priceHighToLow = createSorter('price', 'desc');
let nameMapper = createMapper(product => product.name.toUpperCase());

console.log(products.filter(electronicsFilter));
console.log(products.sort(priceHighToLow));
console.log(products.map(nameMapper));
```

### Упражнение 3: Замыкания и области видимости (40 минут)

```javascript
// 1. Создание модуля счетчика с разными операциями
function createAdvancedCounter(initialValue = 0) {
    // Создайте счетчик с методами:
    // increment, decrement, reset, getValue, getHistory
    // Сохраняйте историю всех операций
}

// 2. Фабрика конфигураций
function createConfig(defaults) {
    // Создайте объект конфигурации с методами:
    // set(key, value) - установить значение
    // get(key) - получить значение (с fallback на defaults)
    // getAll() - получить все значения
    // reset(key) - сбросить значение к умолчанию
    // Приватные данные должны быть недоступны извне
}

// 3. Система кэширования
function createCache(maxSize = 10) {
    // Создайте простой LRU кэш с методами:
    // set(key, value) - сохранить значение
    // get(key) - получить значение
    // clear() - очистить кэш
    // size() - получить размер кэша
    // При превышении maxSize удаляйте самые старые записи
}

// 4. Создание приватных методов
function createCalculator() {
    // Создайте калькулятор с приватными методами валидации
    // Публичные методы: add, subtract, multiply, divide
    // Приватные методы: validateNumbers, logOperation
    // Храните историю операций
}

// Тестирование
let counter = createAdvancedCounter(5);
console.log(counter.increment()); // 6
console.log(counter.decrement()); // 5
console.log(counter.getHistory()); // ['increment', 'decrement']

let config = createConfig({ theme: 'light', language: 'en' });
config.set('theme', 'dark');
console.log(config.get('theme')); // 'dark'
console.log(config.get('language')); // 'en' (из defaults)

let cache = createCache(3);
cache.set('a', 1);
cache.set('b', 2);
console.log(cache.get('a')); // 1

let calc = createCalculator();
console.log(calc.add(5, 3)); // 8
console.log(calc.divide(10, 2)); // 5
// console.log(calc.validateNumbers); // undefined (приватный метод)
```

### Упражнение 4: Практическое применение (37 минут)

```javascript
// 1. Система обработки событий
function createEventEmitter() {
    // Создайте простой эмиттер событий с методами:
    // on(event, callback) - подписаться на событие
    // off(event, callback) - отписаться от события
    // emit(event, ...args) - вызвать все обработчики события
    // once(event, callback) - подписаться на одно срабатывание
}

// 2. Дебаунс и троттлинг
function debounce(func, delay) {
    // Создайте функцию debounce
    // Функция должна вызываться только после окончания серии вызовов
}

function throttle(func, limit) {
    // Создайте функцию throttle
    // Функция должна вызываться не чаще, чем раз в limit миллисекунд
}

// 3. Система валидации форм
function createFormValidator(rules) {
    // rules - объект с правилами валидации для каждого поля
    // Создайте валидатор с методами:
    // validate(data) - валидация всех полей
    // validateField(field, value) - валидация одного поля
    // addRule(field, rule) - добавление нового правила
    // removeRule(field, rule) - удаление правила
}

// 4. Функциональные утилиты
let utils = {
    // Реализуйте утилиты используя функции высшего порядка:
    
    mapObject: (obj, mapper) => {
        // Применить функцию к каждому значению объекта
    },
    
    filterObject: (obj, predicate) => {
        // Отфильтровать объект по предикату
    },
    
    groupBy: (array, keyGetter) => {
        // Сгруппировать массив по ключу
    },
    
    partition: (array, predicate) => {
        // Разделить массив на два по предикату
    },
    
    memoize: (fn) => {
        // Создать мемоизированную версию функции
    }
};

// Тестирование
let emitter = createEventEmitter();
emitter.on('test', (data) => console.log('Test event:', data));
emitter.emit('test', 'Hello!');

let debouncedLog = debounce(console.log, 1000);
debouncedLog('1'); // Не выведется
debouncedLog('2'); // Не выведется  
debouncedLog('3'); // Выведется через 1 секунду

let validator = createFormValidator({
    email: [(val) => val.includes('@'), 'Email должен содержать @'],
    password: [(val) => val.length >= 8, 'Пароль должен быть не менее 8 символов']
});

console.log(validator.validate({ email: 'test@test.com', password: '123456' }));

// Тестирование утилит
let users = [
    { name: 'John', age: 25, role: 'user' },
    { name: 'Jane', age: 30, role: 'admin' },
    { name: 'Bob', age: 25, role: 'user' }
];

console.log(utils.groupBy(users, user => user.role));
console.log(utils.partition(users, user => user.age > 25));

let expensiveFunction = (n) => {
    console.log('Computing...');
    return n * n;
};
let memoizedFunction = utils.memoize(expensiveFunction);
console.log(memoizedFunction(5)); // Computing... 25
console.log(memoizedFunction(5)); // 25 (из кэша)
```

---

## 🧪 Проверочные вопросы

1. В чем разница между function declaration и function expression?
2. Что такое hoisting и как он влияет на функции?
3. Когда использовать стрелочные функции, а когда обычные?
4. Что такое замыкание и как оно работает?
5. В чем разница между `this` в обычных и стрелочных функциях?
6. Что такое функции высшего порядка?
7. Как работают rest параметры в функциях?

## 📝 Домашнее задание

Создайте систему управления задачами (Todo List) используя функции:

```javascript
// Система управления задачами
function createTodoManager() {
    // TODO: Реализуйте систему с использованием замыканий
    
    // Приватные данные:
    // - массив задач
    // - счетчик ID
    // - фильтры и сортировка
    
    return {
        // Основные операции
        addTask: function(title, description, priority = 'medium') {
            // Добавить новую задачу
        },
        
        removeTask: function(id) {
            // Удалить задачу по ID
        },
        
        updateTask: function(id, updates) {
            // Обновить задачу
        },
        
        toggleTask: function(id) {
            // Переключить статус задачи (выполнена/не выполнена)
        },
        
        // Получение данных
        getAllTasks: function() {
            // Получить все задачи
        },
        
        getTask: function(id) {
            // Получить задачу по ID
        },
        
        // Фильтрация и поиск
        filterTasks: function(filterFn) {
            // Отфильтровать задачи по функции
        },
        
        searchTasks: function(query) {
            // Найти задачи по запросу
        },
        
        // Группировка и сортировка
        groupByPriority: function() {
            // Сгруппировать задачи по приоритету
        },
        
        sortTasks: function(criteria) {
            // Отсортировать задачи
        },
        
        // Статистика
        getStats: function() {
            // Получить статистику (всего, выполнено, по приоритетам)
        }
    };
}

// Дополнительные утилиты
let TodoUtils = {
    // Создайте утилиты для работы с задачами
    
    createFilterBy: function(property, value) {
        // Создать функцию фильтрации по свойству
    },
    
    createSortBy: function(property, direction = 'asc') {
        // Создать функцию сортировки
    },
    
    formatTask: function(task) {
        // Отформатировать задачу для вывода
    },
    
    validateTask: function(task) {
        // Валидировать данные задачи
    }
};

// Пример использования:
let todoManager = createTodoManager();

todoManager.addTask('Изучить JavaScript', 'Пройти курс по основам JS', 'high');
todoManager.addTask('Купить продукты', 'Молоко, хлеб, яйца', 'medium');
todoManager.addTask('Погулять с собакой', 'Прогулка в парке', 'low');

console.log(todoManager.getAllTasks());
console.log(todoManager.getStats());

let highPriorityTasks = todoManager.filterTasks(
    TodoUtils.createFilterBy('priority', 'high')
);
console.log(highPriorityTasks);
```

---

## 🔗 Полезные ссылки

- [Functions - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- [Arrow Functions - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Closures - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- [Higher-order Functions](https://eloquentjavascript.net/05_higher_order.html)

**Время изучения блока: 3.2 часа** 