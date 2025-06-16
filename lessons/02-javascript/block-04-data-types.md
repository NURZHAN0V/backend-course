# Блок 4. Основы JavaScript - Типы данных (3.2 часа)

## 🎯 Цели блока

После изучения этого блока вы сможете:
- Понимать все типы данных JavaScript
- Выполнять преобразования типов (явные и неявные)
- Использовать шаблонные строки
- Понимать приоритет операторов

---

## 📚 Теоретическая часть

### 1. Типы данных в JavaScript

JavaScript - слабо типизированный язык с динамической типизацией.

#### Примитивные типы:

```javascript
// Number (числа)
let age = 25;
let price = 19.99;
let infinity = Infinity;
let notANumber = NaN;

// String (строки)
let name = "John";
let city = 'Moscow';
let template = `Hello, ${name}!`;

// Boolean (логический)
let isActive = true;
let isComplete = false;

// Undefined (неопределенный)
let undefinedValue;
let explicitUndefined = undefined;

// Null (пустое значение)
let emptyValue = null;

// Symbol (уникальный идентификатор)
let symbol1 = Symbol('id');
let symbol2 = Symbol('id');
console.log(symbol1 === symbol2); // false

// BigInt (большие целые числа)
let bigNumber = 123456789012345678901234567890n;
let anotherBig = BigInt(123456789012345678901234567890);
```

#### Ссылочные типы:

```javascript
// Object (объект)
let person = {
    name: "John",
    age: 30
};

// Array (массив)
let numbers = [1, 2, 3, 4, 5];
let mixed = [1, "hello", true, null];

// Function (функция)
function greet() {
    console.log("Hello!");
}

// Date (дата)
let now = new Date();

// RegExp (регулярное выражение)
let pattern = /[a-z]+/g;
```

### 2. Проверка типов

```javascript
// Оператор typeof
console.log(typeof 42);          // "number"
console.log(typeof "hello");     // "string"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object" (особенность JS!)
console.log(typeof {});          // "object"
console.log(typeof []);          // "object"
console.log(typeof function(){}); // "function"

// Более точная проверка
console.log(Array.isArray([]));  // true
console.log(Object.prototype.toString.call([])); // "[object Array]"
```

### 3. Преобразования типов

#### Явные преобразования:

```javascript
// Преобразование в строку
String(123);        // "123"
String(true);       // "true"
String(null);       // "null"
String(undefined);  // "undefined"

// Преобразование в число
Number("123");      // 123
Number("123.45");   // 123.45
Number("hello");    // NaN
Number(true);       // 1
Number(false);      // 0
Number(null);       // 0
Number(undefined);  // NaN

// Преобразование в логический тип
Boolean(1);         // true
Boolean(0);         // false
Boolean("");        // false
Boolean("hello");   // true
Boolean(null);      // false
Boolean(undefined); // false

// Альтернативные способы
123 + "";           // "123" (преобразование в строку)
+"123";             // 123 (преобразование в число)
!!"hello";          // true (преобразование в boolean)
```

#### Неявные преобразования:

```javascript
// Сложение со строками
5 + "5";            // "55"
"5" + 5;            // "55"
5 + 3 + "2";        // "82"
"2" + 3 + 5;        // "235"

// Математические операции
"5" - 2;            // 3
"5" * "2";          // 10
"10" / "2";         // 5
"5" % 2;            // 1

// Логические операции
if ("hello") { }    // true
if ("") { }         // false
if (0) { }          // false
if (null) { }       // false

// Сравнения
"5" == 5;           // true (с приведением типов)
"5" === 5;          // false (строгое сравнение)
null == undefined;  // true
null === undefined; // false
```

### 4. Шаблонные строки (Template Literals)

```javascript
let name = "John";
let age = 30;

// Обычные строки
let greeting1 = "Hello, " + name + "! You are " + age + " years old.";

// Шаблонные строки
let greeting2 = `Hello, ${name}! You are ${age} years old.`;

// Многострочные шаблоны
let multiline = `
    This is a
    multiline
    string
`;

// Выражения в шаблонах
let calculation = `2 + 3 = ${2 + 3}`;
let conditional = `You are ${age >= 18 ? 'adult' : 'minor'}`;

// Функции в шаблонах
function formatCurrency(amount) {
    return `$${amount.toFixed(2)}`;
}
let price = `Price: ${formatCurrency(19.99)}`;

// Вложенные шаблоны
let items = ['apple', 'banana', 'orange'];
let list = `Items: ${items.map(item => `• ${item}`).join('\n')}`;
```

### 5. Операторы и их приоритет

#### Арифметические операторы:
```javascript
let a = 10, b = 3;

console.log(a + b);   // 13 (сложение)
console.log(a - b);   // 7 (вычитание)
console.log(a * b);   // 30 (умножение)
console.log(a / b);   // 3.333... (деление)
console.log(a % b);   // 1 (остаток от деления)
console.log(a ** b);  // 1000 (возведение в степень)

// Инкремент и декремент
let x = 5;
console.log(++x);     // 6 (префиксный инкремент)
console.log(x++);     // 6 (постфиксный инкремент)
console.log(x);       // 7
```

#### Операторы сравнения:
```javascript
console.log(5 > 3);   // true
console.log(5 < 3);   // false
console.log(5 >= 5);  // true
console.log(5 <= 4);  // false
console.log(5 == "5"); // true (нестрогое сравнение)
console.log(5 === "5"); // false (строгое сравнение)
console.log(5 != "5"); // false
console.log(5 !== "5"); // true
```

#### Логические операторы:
```javascript
console.log(true && false);  // false (И)
console.log(true || false);  // true (ИЛИ)
console.log(!true);          // false (НЕ)

// Короткое замыкание
let result = true || someFunction(); // someFunction не вызовется
let value = false && expensiveOperation(); // expensiveOperation не вызовется
```

#### Приоритет операторов (от высшего к низшему):
1. `()` - группировка
2. `++`, `--` - инкремент/декремент
3. `**` - возведение в степень
4. `*`, `/`, `%` - умножение, деление, остаток
5. `+`, `-` - сложение, вычитание
6. `<`, `>`, `<=`, `>=` - сравнение
7. `==`, `!=`, `===`, `!==` - равенство
8. `&&` - логическое И
9. `||` - логическое ИЛИ
10. `=`, `+=`, `-=`, etc. - присваивание

```javascript
let result = 2 + 3 * 4;        // 14, не 20
let result2 = (2 + 3) * 4;     // 20
let result3 = 2 ** 3 ** 2;     // 512 (2^(3^2)), не (2^3)^2
```

---

## 💻 Практические упражнения

### Упражнение 1: Работа с типами данных (45 минут)

```javascript
// 1. Создайте переменные разных типов
let userName = "Alice";
let userAge = 25;
let isStudent = true;
let courses = ["JavaScript", "Python", "React"];
let userProfile = {
    name: userName,
    age: userAge,
    isStudent: isStudent,
    courses: courses
};

// 2. Проверьте типы созданных переменных
console.log("userName type:", typeof userName);
console.log("userAge type:", typeof userAge);
console.log("isStudent type:", typeof isStudent);
console.log("courses type:", typeof courses);
console.log("Is courses array?", Array.isArray(courses));
console.log("userProfile type:", typeof userProfile);

// 3. Создайте переменные со специальными значениями
let nullValue = null;
let undefinedValue;
let notANumber = NaN;
let infinityValue = Infinity;

console.log("null type:", typeof nullValue);
console.log("undefined type:", typeof undefinedValue);
console.log("NaN type:", typeof notANumber);
console.log("Infinity type:", typeof infinityValue);
```

### Упражнение 2: Преобразования типов (50 минут)

```javascript
// 1. Явные преобразования
function explicitConversions() {
    let values = [123, "456", true, false, null, undefined, "", "0", "hello"];
    
    values.forEach(value => {
        console.log(`Value: ${value}`);
        console.log(`  to String: "${String(value)}"`);
        console.log(`  to Number: ${Number(value)}`);
        console.log(`  to Boolean: ${Boolean(value)}`);
        console.log('---');
    });
}

// 2. Неявные преобразования
function implicitConversions() {
    console.log("5" + 3);          // ?
    console.log(5 + "3");          // ?
    console.log("5" - 3);          // ?
    console.log("5" * 3);          // ?
    console.log("hello" - 3);      // ?
    console.log(true + 1);         // ?
    console.log(false + 1);        // ?
    console.log(null + 5);         // ?
    console.log(undefined + 5);    // ?
}

// 3. Сравнения
function comparisons() {
    console.log("5" == 5);         // ?
    console.log("5" === 5);        // ?
    console.log(0 == false);       // ?
    console.log(0 === false);      // ?
    console.log("" == false);      // ?
    console.log("" === false);     // ?
    console.log(null == undefined); // ?
    console.log(null === undefined); // ?
}
```

### Упражнение 3: Шаблонные строки (40 минут)

```javascript
// 1. Базовые шаблонные строки
let product = {
    name: "Laptop",
    price: 999.99,
    discount: 0.1,
    inStock: true
};

let description = `
Product: ${product.name}
Original Price: $${product.price}
Discount: ${product.discount * 100}%
Final Price: $${(product.price * (1 - product.discount)).toFixed(2)}
Status: ${product.inStock ? 'In Stock' : 'Out of Stock'}
`;

console.log(description);

// 2. Функции в шаблонах
function formatDate(date) {
    return date.toLocaleDateString('ru-RU');
}

function getTimeOfDay() {
    let hour = new Date().getHours();
    if (hour < 12) return 'утром';
    if (hour < 18) return 'днём';
    return 'вечером';
}

let greeting = `
Сегодня ${formatDate(new Date())}, ${getTimeOfDay()}.
Добро пожаловать в наш магазин!
`;

// 3. Создайте функцию для генерации HTML
function createUserCard(user) {
    return `
        <div class="user-card">
            <h2>${user.name}</h2>
            <p>Возраст: ${user.age} лет</p>
            <p>Email: ${user.email}</p>
            <p>Статус: ${user.isActive ? 'Активен' : 'Неактивен'}</p>
        </div>
    `;
}

let user = {
    name: "Иван Петров",
    age: 28,
    email: "ivan@example.com",
    isActive: true
};

console.log(createUserCard(user));
```

### Упражнение 4: Операторы и приоритет (35 минут)

```javascript
// 1. Вычислите результаты без запуска кода
let expressions = [
    "2 + 3 * 4",
    "(2 + 3) * 4",
    "2 ** 3 ** 2",
    "2 ** (3 ** 2)",
    "10 / 2 * 3",
    "10 / (2 * 3)",
    "5 + 3 > 2 * 4",
    "true && false || true",
    "(true && false) || true",
    "true && (false || true)"
];

// Проверьте свои ответы
expressions.forEach(expr => {
    console.log(`${expr} = ${eval(expr)}`);
});

// 2. Практические примеры
function calculateTotal(price, tax, discount) {
    // Расчет с учетом приоритета операторов
    return price * (1 + tax) * (1 - discount);
}

function isValidAge(age) {
    return age >= 0 && age <= 120;
}

function getDiscountedPrice(originalPrice, discountPercent) {
    return originalPrice * (1 - discountPercent / 100);
}

// Тестирование
console.log(calculateTotal(100, 0.2, 0.1)); // ?
console.log(isValidAge(25)); // ?
console.log(isValidAge(-5)); // ?
console.log(getDiscountedPrice(200, 15)); // ?
```

---

## 🧪 Проверочные вопросы

1. Сколько примитивных типов данных в JavaScript? Назовите их.
2. Почему `typeof null` возвращает "object"?
3. В чем разница между `==` и `===`?
4. Что произойдет при выполнении `"5" + 3 + 2`?
5. Как преобразовать строку в число наиболее безопасным способом?
6. Что такое falsy значения в JavaScript?
7. Какой приоритет у оператора `**` относительно других арифметических операторов?

## 📝 Домашнее задание

Создайте программу "Калькулятор покупок":

```javascript
function shoppingCalculator() {
    // Данные о товарах
    let items = [
        { name: "Хлеб", price: 30, quantity: 2 },
        { name: "Молоко", price: 60, quantity: 1 },
        { name: "Яйца", price: 80, quantity: 1 }
    ];
    
    let discountPercent = 10; // 10% скидка
    let taxPercent = 20; // 20% налог
    
    // TODO: Рассчитайте:
    // 1. Общую стоимость без скидки и налога
    // 2. Размер скидки в рублях
    // 3. Стоимость после скидки
    // 4. Размер налога в рублях
    // 5. Итоговую стоимость
    
    // TODO: Выведите красивый чек используя шаблонные строки
}

// Дополнительно: создайте функции для проверки типов
function getVariableInfo(variable) {
    // Верните объект с информацией о переменной:
    // { value, type, isArray, isTruthy, stringRepresentation }
}
```

---

## 🔗 Полезные ссылки

- [JavaScript Data Types - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [Type Conversion - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [Template Literals - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- [Operator Precedence - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

**Время изучения блока: 3.2 часа** 