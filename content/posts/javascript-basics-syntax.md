---
title: "JavaScript cơ bản: Cú pháp và Cấu trúc"
date: 2025-10-24
tags: ["javascript", "cơ bản"]
categories: ["javascript"]
---

## Giới thiệu

JavaScript là một ngôn ngữ lập trình phổ biến được sử dụng rộng rãi trong phát triển web. Trong bài viết này, chúng ta sẽ tìm hiểu về cú pháp cơ bản và các thành phần quan trọng của JavaScript để bắt đầu hành trình lập trình web.

## Yêu cầu trước khi bắt đầu

1. **Trình duyệt web hiện đại**:
   - Google Chrome
   - Mozilla Firefox
   - Microsoft Edge

2. **Code Editor**:
   - Visual Studio Code
   - Sublime Text
   - WebStorm

3. **Extensions cho VS Code**:
   - JavaScript (ES6) code snippets
   - Live Server
   - ESLint

## Cấu trúc cơ bản của JavaScript

### 1. Nhúng JavaScript vào HTML

```html
<!-- Inline JavaScript -->
<script>
    console.log("Hello World!");
</script>

<!-- External JavaScript -->
<script src="script.js"></script>
```

### 2. Cú pháp cơ bản

```javascript
// Khai báo biến
let message = "Hello World";
const PI = 3.14159;
var oldWay = "Không khuyến khích";

// In ra console
console.log(message);

// Chú thích một dòng
/* Chú thích
   nhiều dòng */
```

## Kiểu dữ liệu trong JavaScript

### 1. Kiểu dữ liệu nguyên thủy

```javascript
// Number
let age = 25;
let price = 99.99;

// String
let name = "John";
let greeting = 'Hello';

// Boolean
let isActive = true;
let isLoggedIn = false;

// Undefined
let undefinedVar;

// Null
let nullVar = null;

// Symbol
let symbol = Symbol('description');

// BigInt
let bigNumber = 9007199254740991n;
```

### 2. Kiểu dữ liệu tham chiếu

```javascript
// Object
let person = {
    name: "John",
    age: 30,
    isStudent: false
};

// Array
let colors = ["red", "green", "blue"];

// Function
function greet(name) {
    return "Hello, " + name;
}
```

## Toán tử và Biểu thức

### 1. Toán tử số học

```javascript
let a = 10;
let b = 5;

console.log(a + b);  // Cộng: 15
console.log(a - b);  // Trừ: 5
console.log(a * b);  // Nhân: 50
console.log(a / b);  // Chia: 2
console.log(a % b);  // Chia lấy dư: 0
console.log(a ** b); // Lũy thừa: 100000
```

### 2. Toán tử so sánh

```javascript
console.log(5 == "5");   // true (so sánh giá trị)
console.log(5 === "5");  // false (so sánh giá trị và kiểu)
console.log(5 != "6");   // true
console.log(5 !== "5");  // true
console.log(5 > 3);      // true
console.log(5 <= 5);     // true
```

### 3. Toán tử logic

```javascript
let x = true;
let y = false;

console.log(x && y);  // AND: false
console.log(x || y);  // OR: true
console.log(!x);      // NOT: false
```

## Cấu trúc điều khiển

### 1. Câu lệnh điều kiện

```javascript
// if statement
let age = 18;
if (age >= 18) {
    console.log("Bạn đã đủ tuổi");
} else {
    console.log("Bạn chưa đủ tuổi");
}

// switch statement
let day = "Monday";
switch (day) {
    case "Monday":
        console.log("Đầu tuần");
        break;
    case "Friday":
        console.log("Cuối tuần");
        break;
    default:
        console.log("Ngày trong tuần");
}
```

### 2. Vòng lặp

```javascript
// for loop
for (let i = 0; i < 5; i++) {
    console.log(i);
}

// while loop
let count = 0;
while (count < 5) {
    console.log(count);
    count++;
}

// do-while loop
let num = 0;
do {
    console.log(num);
    num++;
} while (num < 5);

// for...of loop (Arrays)
let fruits = ["apple", "banana", "orange"];
for (let fruit of fruits) {
    console.log(fruit);
}

// for...in loop (Objects)
let person = { name: "John", age: 30 };
for (let key in person) {
    console.log(key + ": " + person[key]);
}
```

## Ví dụ thực tế

### 1. Tính điểm trung bình

```javascript
function calculateAverage(...scores) {
    const sum = scores.reduce((acc, curr) => acc + curr, 0);
    return sum / scores.length;
}

const average = calculateAverage(85, 90, 92, 88);
console.log(`Điểm trung bình: ${average}`);
```

### 2. Kiểm tra số chẵn lẻ

```javascript
function checkEvenOdd(number) {
    if (number % 2 === 0) {
        return "Số chẵn";
    } else {
        return "Số lẻ";
    }
}

console.log(checkEvenOdd(7));  // "Số lẻ"
console.log(checkEvenOdd(8));  // "Số chẵn"
```

## Lỗi thường gặp và cách khắc phục

1. **Sử dụng biến chưa khai báo**
   ```javascript
   console.log(x);  // ReferenceError
   ```
   🔧 Giải pháp: Luôn khai báo biến trước khi sử dụng

2. **So sánh không chặt chẽ**
   ```javascript
   0 == false   // true
   0 === false  // false
   ```
   🔧 Giải pháp: Sử dụng === thay vì ==

3. **Quên dấu chấm phẩy**
   ```javascript
   let a = 5
   let b = 6  // Có thể gây lỗi
   ```
   🔧 Giải pháp: Luôn kết thúc câu lệnh bằng dấu chấm phẩy

## Best Practices

1. **Đặt tên có ý nghĩa**
   ```javascript
   // Không tốt
   let x = 5;
   
   // Tốt
   let userAge = 5;
   ```

2. **Sử dụng let và const**
   ```javascript
   // Khuyến khích
   const PI = 3.14;
   let count = 0;
   
   // Không khuyến khích
   var number = 42;
   ```

3. **Thụt lề và định dạng code**
   ```javascript
   // Định dạng tốt
   function calculateSum(a, b) {
       let sum = a + b;
       return sum;
   }
   ```

## Bài tập thực hành

1. Viết chương trình tính chu vi và diện tích hình chữ nhật
2. Tạo ứng dụng Todo List đơn giản
3. Viết function kiểm tra số nguyên tố
4. Tạo chương trình tính điểm trung bình và xếp loại học sinh

## Công cụ và Extensions hữu ích

1. **Chrome DevTools**
   - Console để debug
   - Sources để theo dõi code
   - Network để kiểm tra requests

2. **VS Code Extensions**
   - ESLint: Kiểm tra lỗi code
   - Prettier: Định dạng code
   - JavaScript Debugger

3. **Online Playgrounds**
   - JSFiddle
   - CodePen
   - CodeSandbox

## Kết luận

Hiểu rõ cú pháp cơ bản của JavaScript là nền tảng quan trọng để:
- Phát triển ứng dụng web
- Debug code hiệu quả
- Viết code sạch và dễ bảo trì
- Tiếp cận các khái niệm nâng cao

## Tài liệu tham khảo

1. [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
2. [JavaScript.info](https://javascript.info/)
3. [W3Schools JavaScript Tutorial](https://www.w3schools.com/js/)
