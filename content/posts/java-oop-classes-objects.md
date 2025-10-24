---
title: "Java OOP: Hướng dẫn toàn diện về Lớp và Đối tượng"
date: 2025-10-24
tags: ["java", "cơ bản", "oop"]
categories: ["java"]
---

## Giới thiệu

Lập trình hướng đối tượng (Object-Oriented Programming - OOP) là một phương pháp lập trình quan trọng trong Java. Hai khái niệm cốt lõi của OOP là Lớp (Class) và Đối tượng (Object). Trong bài viết này, chúng ta sẽ tìm hiểu chi tiết về cách tạo và sử dụng lớp và đối tượng trong Java.

## Yêu cầu trước khi bắt đầu

1. **Java Development Kit (JDK)** - Phiên bản 8 trở lên
2. **Một IDE** (Môi trường phát triển tích hợp):
   - IntelliJ IDEA
   - Eclipse
   - Visual Studio Code với Extension Pack for Java

## Lớp (Class) trong Java

### 1. Định nghĩa lớp

```java
public class Student {
    // Thuộc tính (Fields)
    private String name;
    private int age;
    private String studentId;
    
    // Constructor
    public Student(String name, int age, String studentId) {
        this.name = name;
        this.age = age;
        this.studentId = studentId;
    }
    
    // Phương thức (Methods)
    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Student ID: " + studentId);
    }
}
```

### 2. Các thành phần của lớp

#### a. Thuộc tính (Fields)
```java
public class Car {
    // Thuộc tính instance
    private String brand;
    private String model;
    
    // Thuộc tính static
    private static int totalCars = 0;
}
```

#### b. Constructor
```java
public class Person {
    private String name;
    
    // Constructor mặc định
    public Person() {
        this.name = "Unknown";
    }
    
    // Constructor có tham số
    public Person(String name) {
        this.name = name;
    }
}
```

#### c. Phương thức (Methods)
```java
public class Calculator {
    // Phương thức instance
    public int add(int a, int b) {
        return a + b;
    }
    
    // Phương thức static
    public static int multiply(int a, int b) {
        return a * b;
    }
}
```

## Đối tượng (Object) trong Java

### 1. Tạo đối tượng

```java
// Sử dụng từ khóa new
Student student1 = new Student("John Doe", 20, "S001");

// Tạo nhiều đối tượng
Student student2 = new Student("Jane Smith", 21, "S002");
```

### 2. Truy cập thuộc tính và phương thức

```java
public class BankAccount {
    private double balance;
    
    public void deposit(double amount) {
        balance += amount;
    }
    
    public double getBalance() {
        return balance;
    }
}

// Sử dụng đối tượng
BankAccount account = new BankAccount();
account.deposit(1000);
System.out.println(account.getBalance());
```

## Tính đóng gói (Encapsulation)

### 1. Access Modifiers

```java
public class Employee {
    // private - chỉ truy cập được trong class
    private String name;
    
    // protected - truy cập được trong package và lớp con
    protected double salary;
    
    // public - truy cập được từ mọi nơi
    public String department;
    
    // default - truy cập được trong package
    String position;
}
```

### 2. Getter và Setter

```java
public class Product {
    private String name;
    private double price;
    
    // Getter
    public String getName() {
        return name;
    }
    
    // Setter
    public void setName(String name) {
        this.name = name;
    }
    
    public double getPrice() {
        return price;
    }
    
    public void setPrice(double price) {
        if (price >= 0) {
            this.price = price;
        }
    }
}
```

## Ví dụ thực tế

### 1. Quản lý thông tin sinh viên

```java
public class Student {
    private String name;
    private double[] scores;
    
    public Student(String name, double[] scores) {
        this.name = name;
        this.scores = scores;
    }
    
    public double calculateAverage() {
        double sum = 0;
        for (double score : scores) {
            sum += score;
        }
        return sum / scores.length;
    }
    
    public char getGrade() {
        double average = calculateAverage();
        if (average >= 90) return 'A';
        if (average >= 80) return 'B';
        if (average >= 70) return 'C';
        if (average >= 60) return 'D';
        return 'F';
    }
}
```

### 2. Hệ thống quản lý thư viện

```java
public class Book {
    private String title;
    private String author;
    private boolean borrowed;
    
    public Book(String title, String author) {
        this.title = title;
        this.author = author;
        this.borrowed = false;
    }
    
    public void borrowBook() {
        if (!borrowed) {
            borrowed = true;
            System.out.println("Book borrowed successfully");
        } else {
            System.out.println("Book is already borrowed");
        }
    }
    
    public void returnBook() {
        if (borrowed) {
            borrowed = false;
            System.out.println("Book returned successfully");
        } else {
            System.out.println("Book was not borrowed");
        }
    }
}
```

## Lỗi thường gặp và cách khắc phục

1. **NullPointerException**
   ```java
   Student student;
   student.displayInfo(); // Lỗi: Chưa khởi tạo đối tượng
   ```
   🔧 Giải pháp: Khởi tạo đối tượng trước khi sử dụng

2. **Truy cập sai access modifier**
   ```java
   public class Test {
       private int data;
   }
   Test t = new Test();
   t.data = 10; // Lỗi: Không thể truy cập trực tiếp thuộc tính private
   ```
   🔧 Giải pháp: Sử dụng getter/setter hoặc điều chỉnh access modifier

3. **Quên từ khóa this**
   ```java
   public class Person {
       private String name;
       public Person(String name) {
           name = name; // Gán sai
       }
   }
   ```
   🔧 Giải pháp: Sử dụng this.name = name

## Best Practices

1. **Tên lớp**
   - Sử dụng PascalCase
   - Tên phải mang tính mô tả
   - Ví dụ: `StudentManager`, `BankAccount`

2. **Tên thuộc tính và phương thức**
   - Sử dụng camelCase
   - Động từ cho phương thức
   - Ví dụ: `firstName`, `calculateTotal()`

3. **Encapsulation**
   - Đặt thuộc tính là private
   - Sử dụng getter/setter
   - Kiểm tra dữ liệu trong setter

## Bài tập thực hành

1. Tạo lớp `Rectangle` với các thuộc tính length và width
2. Xây dựng hệ thống quản lý nhân viên đơn giản
3. Thiết kế lớp `BankAccount` với các phương thức gửi và rút tiền
4. Tạo lớp `Car` với các thuộc tính và phương thức phù hợp

## Kết luận

Hiểu và sử dụng tốt lớp và đối tượng là nền tảng quan trọng trong lập trình Java. Điều này giúp:
- Tổ chức code có cấu trúc
- Tái sử dụng code hiệu quả
- Bảo mật và kiểm soát dữ liệu tốt hơn
- Dễ dàng bảo trì và mở rộng code

## Tài liệu tham khảo

1. [Oracle Java OOP Concepts](https://docs.oracle.com/javase/tutorial/java/concepts/index.html)
2. [Java Classes and Objects](https://www.w3schools.com/java/java_classes.asp)
3. [Object-Oriented Programming in Java](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/)
