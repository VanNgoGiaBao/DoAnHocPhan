---
title: "JavaScript ES6: Những tính năng quan trọng cần biết"
date: 2025-10-24
tags: ["javascript", "es6", "cơ bản"]
categories: ["javascript"]
---

## Giới thiệu

ECMAScript 2015 (ES6) là một bước ngoặt quan trọng trong lịch sử phát triển của JavaScript, giới thiệu nhiều tính năng mới giúp code trở nên sạch sẽ, dễ đọc và mạnh mẽ hơn. Trong bài viết này, chúng ta sẽ tìm hiểu chi tiết về những tính năng quan trọng nhất của ES6.

## Yêu cầu trước khi bắt đầu

1. **Node.js** phiên bản 6.0.0 trở lên
2. **Trình duyệt hiện đại** hỗ trợ ES6:
   - Google Chrome
   - Firefox
   - Safari
   - Microsoft Edge
3. **Code Editor** với syntax highlighting cho ES6:
   - Visual Studio Code
   - Sublime Text
   - WebStorm

## Các tính năng chính của ES6

### 1. Let và Const

```javascript
// Let - phạm vi block scope
let x = 10;
if (true) {
    let x = 20; // biến mới, khác với x ở ngoài
    console.log(x); // 20
}
console.log(x); // 10

// Const - không thể gán lại giá trị
const PI = 3.14159;
// PI = 3.14; // Lỗi: không thể gán lại giá trị cho hằng số
```

### 2. Arrow Functions

```javascript
// Cú pháp truyền thống
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// Arrow function với nhiều dòng
const multiply = (a, b) => {
    const result = a * b;
    return result;
};

// Arrow function trong callback
const numbers = [1, 2, 3];
const doubled = numbers.map(num => num * 2);
```

### 3. Template Literals

```javascript
const name = 'John';
const age = 30;

// Cách cũ
console.log('Xin chào, tôi là ' + name + ' và tôi ' + age + ' tuổi.');

// Template literals
console.log(`Xin chào, tôi là ${name} và tôi ${age} tuổi.`);

// Template literals nhiều dòng
const html = `
    <div>
        <h1>${name}</h1>
        <p>Tuổi: ${age}</p>
    </div>
`;
```

### 4. Destructuring Assignment

```javascript
// Destructuring Array
const colors = ['red', 'green', 'blue'];
const [first, second, third] = colors;
console.log(first);  // red

// Destructuring Object
const person = {
    name: 'John',
    age: 30,
    city: 'New York'
};
const { name, age } = person;
console.log(name);  // John

// Đổi tên biến khi destructuring
const { name: fullName, age: years } = person;
console.log(fullName);  // John
```

### 5. Spread và Rest Operators

```javascript
// Spread operator với arrays
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];
console.log(arr2);  // [1, 2, 3, 4, 5]

// Spread operator với objects
const obj1 = { foo: 'bar', x: 42 };
const obj2 = { foo: 'baz', y: 13 };
const clonedObj = { ...obj1 };
const mergedObj = { ...obj1, ...obj2 };

// Rest parameter
const sum = (...numbers) => {
    return numbers.reduce((acc, cur) => acc + cur, 0);
};
console.log(sum(1, 2, 3, 4));  // 10
```

### 6. Classes

```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    speak() {
        console.log(`${this.name} makes a sound.`);
    }
}

class Dog extends Animal {
    constructor(name) {
        super(name);
    }
    
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog('Rex');
dog.speak();  // Rex barks.
```

### 7. Modules

```javascript
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// main.js
import { add, subtract } from './math.js';
console.log(add(5, 3));      // 8
console.log(subtract(5, 3)); // 2

// Default export
export default class User {
    constructor(name) {
        this.name = name;
    }
}

// Import default
import User from './User.js';
```

### 8. Promises

```javascript
const fetchData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = { id: 1, name: 'John' };
            if (data) {
                resolve(data);
            } else {
                reject('Error fetching data');
            }
        }, 1000);
    });
};

fetchData()
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

## Ví dụ thực tế

### 1. Quản lý người dùng với Class

```javascript
class UserManager {
    constructor() {
        this.users = [];
    }

    addUser(name, email) {
        const user = {
            id: Date.now(),
            name,
            email
        };
        this.users.push(user);
        return user;
    }

    findUser(id) {
        return this.users.find(user => user.id === id);
    }

    updateUser(id, updates) {
        const user = this.findUser(id);
        if (user) {
            Object.assign(user, updates);
            return true;
        }
        return false;
    }
}

const manager = new UserManager();
const user = manager.addUser('John', 'john@example.com');
```

### 2. API Service với Async/Await

```javascript
class APIService {
    constructor(baseURL) {
        this.baseURL = baseURL;
    }

    async fetchUsers() {
        try {
            const response = await fetch(`${this.baseURL}/users`);
            if (!response.ok) throw new Error('Network response was not ok');
            return await response.json();
        } catch (error) {
            console.error('Error:', error);
            throw error;
        }
    }

    async createUser(userData) {
        const response = await fetch(`${this.baseURL}/users`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(userData)
        });
        return await response.json();
    }
}
```

## Lỗi thường gặp và cách khắc phục

1. **Temporal Dead Zone với let/const**
   ```javascript
   console.log(x); // ReferenceError
   let x = 5;
   ```
   🔧 Giải pháp: Khai báo biến trước khi sử dụng

2. **This trong Arrow Function**
   ```javascript
   const obj = {
       name: 'Object',
       regularMethod: function() {
           console.log(this.name); // 'Object'
       },
       arrowMethod: () => {
           console.log(this.name); // undefined
       }
   };
   ```
   🔧 Giải pháp: Sử dụng regular function khi cần truy cập this

3. **Promise Chain không có catch**
   ```javascript
   // Không tốt
   promise.then(data => {/*...*/});
   
   // Tốt
   promise
       .then(data => {/*...*/})
       .catch(error => console.error(error));
   ```

## Best Practices

1. **Sử dụng const mặc định**
   ```javascript
   // Ưu tiên
   const config = { /*...*/ };
   
   // Chỉ dùng let khi cần thay đổi giá trị
   let counter = 0;
   ```

2. **Arrow Function ngắn gọn**
   ```javascript
   // Tốt
   const square = x => x * x;
   
   // Không cần dấu ngoặc với một tham số
   const double = x => x * 2;
   ```

3. **Destructuring trong tham số hàm**
   ```javascript
   // Tốt
   const printUser = ({ name, age }) => {
       console.log(`${name} is ${age} years old`);
   };
   ```

## Bài tập thực hành

1. Xây dựng class `ShoppingCart` với các phương thức quản lý giỏ hàng
2. Tạo module quản lý authentication với Promise
3. Viết utility function sử dụng destructuring và spread operator
4. Implement một event emitter sử dụng class

## Công cụ hỗ trợ

1. **Babel** - Compiler ES6 về ES5
2. **ESLint** - Kiểm tra code style và lỗi
3. **webpack** - Bundler hỗ trợ ES6 modules

## Kết luận

ES6 mang đến nhiều cải tiến quan trọng cho JavaScript:
- Cú pháp rõ ràng và ngắn gọn hơn
- Xử lý bất đồng bộ tốt hơn với Promise
- Lập trình hướng đối tượng dễ dàng hơn với Class
- Module hóa code hiệu quả

## Tài liệu tham khảo

1. [MDN Web Docs - JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
2. [ES6 Features](https://es6-features.org/)
3. [JavaScript.info](https://javascript.info/)
