---
title: "Java: Hướng dẫn chi tiết về vòng lặp (Loops)"
date: 2025-10-24
tags: ["java", "cơ bản"]
categories: ["java"]
---

## Giới thiệu

Vòng lặp (Loops) là một trong những cấu trúc điều khiển cơ bản nhất trong lập trình Java. Chúng cho phép thực thi một khối lệnh nhiều lần dựa trên một điều kiện. Trong bài viết này, chúng ta sẽ tìm hiểu chi tiết về các loại vòng lặp trong Java và cách sử dụng chúng hiệu quả.

## Yêu cầu trước khi bắt đầu

1. **Java Development Kit (JDK)** - Phiên bản 8 trở lên
2. **Một IDE** (Môi trường phát triển tích hợp):
   - IntelliJ IDEA
   - Eclipse
   - Visual Studio Code với Extension Pack for Java

## Các loại vòng lặp trong Java

Java cung cấp bốn loại vòng lặp chính:

1. Vòng lặp for
2. Vòng lặp while
3. Vòng lặp do-while
4. Vòng lặp for-each (Enhanced for)

### 1. Vòng lặp for

```java
for (initialization; condition; increment/decrement) {
    // Khối lệnh cần lặp
}
```

Ví dụ:
```java
// In ra các số từ 1 đến 5
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}

// Đếm ngược từ 5 về 1
for (int i = 5; i >= 1; i--) {
    System.out.println(i);
}
```

### 2. Vòng lặp while

```java
while (condition) {
    // Khối lệnh cần lặp
}
```

Ví dụ:
```java
int count = 1;
while (count <= 5) {
    System.out.println(count);
    count++;
}
```

### 3. Vòng lặp do-while

```java
do {
    // Khối lệnh cần lặp
} while (condition);
```

Ví dụ:
```java
int number = 1;
do {
    System.out.println(number);
    number++;
} while (number <= 5);
```

### 4. Vòng lặp for-each

```java
for (dataType item : array/collection) {
    // Khối lệnh cần lặp
}
```

Ví dụ:
```java
String[] fruits = {"Apple", "Banana", "Orange"};
for (String fruit : fruits) {
    System.out.println(fruit);
}
```

## Các từ khóa điều khiển vòng lặp

### 1. break

Dùng để thoát khỏi vòng lặp:
```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break; // Thoát khi i = 5
    }
    System.out.println(i);
}
```

### 2. continue

Bỏ qua phần còn lại của vòng lặp hiện tại:
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue; // Bỏ qua số 3
    }
    System.out.println(i);
}
```

## Các ví dụ thực tế

### 1. Tính tổng các số

```java
public class SumCalculator {
    public static void main(String[] args) {
        int sum = 0;
        for (int i = 1; i <= 100; i++) {
            sum += i;
        }
        System.out.println("Tổng từ 1 đến 100: " + sum);
    }
}
```

### 2. In bảng cửu chương

```java
public class MultiplicationTable {
    public static void main(String[] args) {
        int number = 5;
        for (int i = 1; i <= 10; i++) {
            System.out.printf("%d x %d = %d%n", 
                number, i, (number * i));
        }
    }
}
```

### 3. Tìm số nguyên tố

```java
public class PrimeNumber {
    public static void main(String[] args) {
        int number = 17;
        boolean isPrime = true;
        
        for (int i = 2; i <= Math.sqrt(number); i++) {
            if (number % i == 0) {
                isPrime = false;
                break;
            }
        }
        
        System.out.println(number + (isPrime ? " là" : " không là") + " số nguyên tố");
    }
}
```

## Lỗi thường gặp và cách khắc phục

1. **Vòng lặp vô hạn**
   ```java
   // Lỗi: Vòng lặp vô hạn
   for (int i = 1; i > 0; i++) {
       System.out.println(i);
   }
   ```
   🔧 Giải pháp: Đảm bảo điều kiện dừng hợp lý

2. **Sai điều kiện dừng**
   ```java
   // Lỗi: Điều kiện không bao giờ đạt được
   while (i != 10) {
       i += 2;
   }
   ```
   🔧 Giải pháp: Kiểm tra kỹ điều kiện dừng

3. **Quên cập nhật biến điều kiện**
   ```java
   // Lỗi: Quên tăng i
   while (i < 5) {
       System.out.println(i);
       // Thiếu i++
   }
   ```
   🔧 Giải pháp: Đảm bảo cập nhật biến điều kiện

## Kỹ thuật tối ưu vòng lặp

### 1. Sử dụng vòng lặp phù hợp
- `for`: khi biết trước số lần lặp
- `while`: khi không biết trước số lần lặp
- `do-while`: khi cần thực hiện ít nhất một lần
- `for-each`: khi duyệt qua collection

### 2. Tối ưu hóa điều kiện
```java
// Không tối ưu
for (int i = 0; i < array.length; i++)

// Tối ưu hơn
int length = array.length;
for (int i = 0; i < length; i++)
```

### 3. Sử dụng break và continue hợp lý
```java
// Tìm phần tử trong mảng
for (int element : array) {
    if (element == target) {
        found = true;
        break; // Thoát ngay khi tìm thấy
    }
}
```

## Bài tập thực hành

1. Viết chương trình in ra các số Fibonacci
2. Tính giai thừa của một số
3. In ra tam giác số
4. Đếm số ký tự trong một chuỗi

## Kết luận

Vòng lặp là một công cụ mạnh mẽ trong Java, giúp:
- Tự động hóa các tác vụ lặp lại
- Xử lý dữ liệu trong mảng và collection
- Tối ưu hóa code
- Giảm sự lặp lại trong code

## Tài liệu tham khảo

1. [Oracle Java Loops Guide](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html)
2. [W3Schools Java Loops](https://www.w3schools.com/java/java_for_loop.asp)
3. [Java Loop Performance](https://www.baeldung.com/java-loops)
