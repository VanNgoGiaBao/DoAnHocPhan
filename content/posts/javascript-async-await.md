---
title: "JavaScript: Hướng dẫn toàn diện về Async/Await"
date: 2025-10-24
tags: ["javascript", "async/await", "promises"]
categories: ["javascript"]
---

## Giới thiệu

Async/Await là một tính năng mạnh mẽ trong JavaScript, giúp xử lý các tác vụ bất đồng bộ một cách dễ dàng và rõ ràng hơn. Được giới thiệu từ ES2017, Async/Await là một cách viết code bất đồng bộ theo kiểu đồng bộ, giúp code dễ đọc và dễ bảo trì hơn.

## Yêu cầu trước khi bắt đầu

1. **Kiến thức cơ bản về JavaScript**
2. **Hiểu về Promise trong JavaScript**
3. **Môi trường phát triển**:
   - Node.js (phiên bản 7.6.0 trở lên)
   - Trình duyệt hiện đại (Chrome, Firefox, Safari)
   - VS Code hoặc editor yêu thích

## Async/Await là gì?

### 1. Async Function

```javascript
async function myFunction() {
    // Code bất đồng bộ ở đây
    return "Hello";
}

// Tương đương với
function myFunction() {
    return Promise.resolve("Hello");
}
```

### 2. Await Operator

```javascript
async function getData() {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    return data;
}
```

## Cách sử dụng Async/Await

### 1. Cú pháp cơ bản

```javascript
async function fetchUserData() {
    try {
        const response = await fetch('https://api.example.com/user');
        const userData = await response.json();
        console.log(userData);
    } catch (error) {
        console.error('Error:', error);
    }
}
```

### 2. So sánh với Promises

```javascript
// Sử dụng Promise
function getUserPromise() {
    return fetch('https://api.example.com/user')
        .then(response => response.json())
        .then(data => console.log(data))
        .catch(error => console.error('Error:', error));
}

// Sử dụng Async/Await
async function getUserAsync() {
    try {
        const response = await fetch('https://api.example.com/user');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error:', error);
    }
}
```

## Xử lý lỗi với Async/Await

### 1. Try-Catch

```javascript
async function handleErrors() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Có lỗi xảy ra:', error);
        throw new Error('Không thể lấy dữ liệu');
    }
}
```

### 2. Error Propagation

```javascript
async function fetchData() {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
    }
    return await response.json();
}

async function processData() {
    try {
        const data = await fetchData();
        // Xử lý dữ liệu
    } catch (error) {
        // Xử lý lỗi
        console.error('Error in processData:', error);
    }
}
```

## Các pattern thường dùng

### 1. Xử lý nhiều Promise cùng lúc

```javascript
async function fetchMultipleUrls() {
    try {
        const urls = [
            'https://api.example.com/data1',
            'https://api.example.com/data2',
            'https://api.example.com/data3'
        ];
        
        const promises = urls.map(url => fetch(url));
        const responses = await Promise.all(promises);
        const data = await Promise.all(responses.map(r => r.json()));
        
        return data;
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}
```

### 2. Sequential vs Parallel Execution

```javascript
// Tuần tự
async function sequential() {
    const result1 = await fetchData1();
    const result2 = await fetchData2();
    return [result1, result2];
}

// Song song
async function parallel() {
    const [result1, result2] = await Promise.all([
        fetchData1(),
        fetchData2()
    ]);
    return [result1, result2];
}
```

## Ví dụ thực tế

### 1. Ứng dụng đăng nhập

```javascript
async function login(username, password) {
    try {
        // Gửi request đăng nhập
        const response = await fetch('/api/login', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ username, password })
        });

        if (!response.ok) {
            throw new Error('Đăng nhập thất bại');
        }

        const userData = await response.json();
        
        // Lưu token
        localStorage.setItem('token', userData.token);
        
        return userData;
    } catch (error) {
        console.error('Lỗi đăng nhập:', error);
        throw error;
    }
}
```

### 2. Tải và hiển thị dữ liệu

```javascript
async function displayUserProfile() {
    try {
        // Hiển thị loading
        showLoading();
        
        // Lấy dữ liệu người dùng
        const userData = await fetchUserData();
        
        // Lấy bài viết của người dùng
        const userPosts = await fetchUserPosts(userData.id);
        
        // Cập nhật UI
        updateProfile(userData);
        updatePosts(userPosts);
    } catch (error) {
        showError(error);
    } finally {
        hideLoading();
    }
}
```

## Lỗi thường gặp và cách khắc phục

1. **Quên từ khóa await**
   ```javascript
   // Lỗi
   async function getData() {
       const data = fetch('https://api.example.com/data');
       console.log(data); // Promise pending
   }

   // Đúng
   async function getData() {
       const data = await fetch('https://api.example.com/data');
       console.log(data); // Response data
   }
   ```

2. **Await trong vòng lặp**
   ```javascript
   // Không hiệu quả
   for (const url of urls) {
       const data = await fetch(url);
   }

   // Tối ưu hơn
   const promises = urls.map(url => fetch(url));
   const results = await Promise.all(promises);
   ```

3. **Không xử lý lỗi**
   ```javascript
   // Thiếu xử lý lỗi
   async function getData() {
       const response = await fetch(url);
       return response.json();
   }

   // Có xử lý lỗi
   async function getData() {
       try {
           const response = await fetch(url);
           return await response.json();
       } catch (error) {
           console.error('Error:', error);
           throw error;
       }
   }
   ```

## Best Practices

1. **Luôn sử dụng Try-Catch**
   ```javascript
   async function safeFunction() {
       try {
           // code here
       } catch (error) {
           // handle error
       }
   }
   ```

2. **Tránh mixing Promises và Async/Await**
   ```javascript
   // Không nên
   async function mixed() {
       return fetch(url).then(r => r.json());
   }

   // Nên
   async function consistent() {
       const response = await fetch(url);
       return await response.json();
   }
   ```

3. **Xử lý song song khi có thể**
   ```javascript
   // Tốt hơn khi các promise độc lập
   const [users, posts, comments] = await Promise.all([
       fetchUsers(),
       fetchPosts(),
       fetchComments()
   ]);
   ```

## Bài tập thực hành

1. Tạo function tải dữ liệu từ nhiều API
2. Xây dựng hệ thống authentication đơn giản
3. Tạo ứng dụng tìm kiếm với debouncing
4. Xử lý upload file với progress tracking

## Kết luận

Async/Await là công cụ mạnh mẽ trong JavaScript để xử lý các tác vụ bất đồng bộ. Nó giúp:
- Code dễ đọc và dễ bảo trì hơn
- Xử lý lỗi hiệu quả hơn
- Dễ dàng debug hơn
- Tối ưu hiệu suất ứng dụng

## Tài liệu tham khảo

1. [MDN Web Docs - Async/Await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
2. [JavaScript.info - Async/Await](https://javascript.info/async-await)
3. [Node.js Documentation](https://nodejs.org/api/async_hooks.html)
