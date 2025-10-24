---
title: "Java: Hướng dẫn chi tiết về Biến và Kiểu dữ liệu"
date: 2025-10-24
tags: ["java", "cơ bản"]
categories: ["java"]
---

## Giới thiệu

Biến và kiểu dữ liệu là những khái niệm cơ bản nhất trong lập trình Java. Chúng là nền tảng để lưu trữ và xử lý dữ liệu trong chương trình. Trong bài viết này, chúng ta sẽ tìm hiểu chi tiết về các loại biến và kiểu dữ liệu trong Java.

## Yêu cầu trước khi bắt đầu

1. **Java Development Kit (JDK)** - Phiên bản 8 trở lên
2. **Một IDE** (Môi trường phát triển tích hợp):
   - IntelliJ IDEA
   - Eclipse
   - Visual Studio Code với Extension Pack for Java

## Biến trong Java

### 1. Định nghĩa biến

Biến là một vùng nhớ được đặt tên để lưu trữ dữ liệu. Cú pháp khai báo biến:

```java
dataType variableName = value;
```

Ví dụ:
```java
int age = 25;
String name = "John";
double salary = 1000.50;
```

### 2. Quy tắc đặt tên biến

- Bắt đầu bằng chữ cái, underscore (_) hoặc dollar sign ($)
- Không được bắt đầu bằng số
- Không được sử dụng từ khóa của Java
- Phân biệt chữ hoa chữ thường
- Tuân theo quy ước camelCase

```java
// Hợp lệ
int userAge;
String firstName;
double _temperature;
float $price;

// Không hợp lệ
int 1number;      // Bắt đầu bằng số
String class;     // Từ khóa của Java
float my-price;   // Chứa dấu gạch ngang
```

## Kiểu dữ liệu trong Java

### 1. Kiểu dữ liệu nguyên thủy (Primitive Data Types)

#### a. Kiểu số nguyên

```java
byte byteNum = 127;         // 8-bit, -128 đến 127
short shortNum = 32767;     // 16-bit, -32,768 đến 32,767
int intNum = 2147483647;    // 32-bit, -2^31 đến 2^31-1
long longNum = 9223372036854775807L;  // 64-bit, -2^63 đến 2^63-1
```

#### b. Kiểu số thực

```java
float floatNum = 3.14f;     // 32-bit, ~7 chữ số thập phân
double doubleNum = 3.14159; // 64-bit, ~15 chữ số thập phân
```

#### c. Kiểu ký tự

```java
char letter = 'A';          // 16-bit Unicode character
```

#### d. Kiểu logic

```java
boolean isTrue = true;      // true hoặc false
```

### 2. Kiểu dữ liệu tham chiếu (Reference Data Types)

#### a. String

```java
String text = "Hello World";
String emptyString = "";
String nullString = null;
```

#### b. Array

```java
int[] numbers = {1, 2, 3, 4, 5};
String[] names = new String[3];
```

#### c. Class

```java
class Person {
    String name;
    int age;
}
Person person = new Person();
```

## Chuyển đổi kiểu dữ liệu

### 1. Chuyển đổi ngầm định (Widening Casting)

```java
int myInt = 9;
double myDouble = myInt;    // Tự động chuyển từ int sang double
```

### 2. Chuyển đổi tường minh (Narrowing Casting)

```java
double myDouble = 9.78;
int myInt = (int) myDouble; // Phải ép kiểu tường minh
```

## Hằng số (Constants)

```java
final double PI = 3.14159;
final String COMPANY_NAME = "Tech Corp";
```

## Phạm vi biến (Variable Scope)

### 1. Biến cục bộ (Local Variables)

```java
public void calculateSum() {
    int x = 10;  // Biến cục bộ
    int y = 20;  // Chỉ có thể sử dụng trong phương thức này
    int sum = x + y;
}
```

### 2. Biến instance

```java
public class Student {
    private String name;    // Biến instance
    private int age;       // Có thể sử dụng trong toàn bộ class
}
```

### 3. Biến static

```java
public class Counter {
    public static int count = 0;  // Biến static
    // Được chia sẻ giữa tất cả các đối tượng của class
}
```

## Ví dụ thực tế

### 1. Tính diện tích hình chữ nhật

```java
public class RectangleCalculator {
    public static void main(String[] args) {
        double length = 5.5;
        double width = 3.2;
        double area = length * width;
        
        System.out.printf("Diện tích: %.2f%n", area);
    }
}
```

### 2. Quản lý thông tin sinh viên

```java
public class StudentInfo {
    public static void main(String[] args) {
        String studentName = "Nguyen Van A";
        int studentAge = 20;
        float gpa = 3.75f;
        boolean isScholarship = gpa >= 3.5;
        
        System.out.println("Tên: " + studentName);
        System.out.println("Tuổi: " + studentAge);
        System.out.println("GPA: " + gpa);
        System.out.println("Học bổng: " + isScholarship);
    }
}
```

## Lỗi thường gặp và cách khắc phục

1. **Sử dụng biến chưa khởi tạo**
   ```java
   int number;
   System.out.println(number); // Lỗi: biến chưa được khởi tạo
   ```
   🔧 Giải pháp: Khởi tạo giá trị cho biến trước khi sử dụng

2. **Tràn số**
   ```java
   byte smallNumber = 128; // Lỗi: vượt quá giới hạn của byte
   ```
   🔧 Giải pháp: Sử dụng kiểu dữ liệu phù hợp

3. **Ép kiểu không an toàn**
   ```java
   double price = 19.99;
   int roundedPrice = price; // Lỗi: cần ép kiểu tường minh
   ```
   🔧 Giải pháp: Sử dụng ép kiểu tường minh (int)price

## Best Practices

1. **Đặt tên biến có ý nghĩa**
   ```java
   // Không tốt
   int x = 5;
   
   // Tốt
   int age = 5;
   ```

2. **Khởi tạo giá trị mặc định**
   ```java
   int count = 0;
   String name = "";
   boolean isActive = false;
   ```

3. **Sử dụng final cho hằng số**
   ```java
   final double TAX_RATE = 0.1;
   final int MAX_USERS = 100;
   ```

## Bài tập thực hành

1. Tạo chương trình tính chỉ số BMI
2. Xây dựng ứng dụng chuyển đổi đơn vị tiền tệ
3. Tính điểm trung bình của sinh viên
4. Quản lý thông tin sản phẩm trong cửa hàng

## Kết luận

Hiểu rõ về biến và kiểu dữ liệu là nền tảng quan trọng trong lập trình Java. Điều này giúp:
- Quản lý bộ nhớ hiệu quả
- Tránh lỗi runtime
- Viết code rõ ràng và dễ bảo trì
- Tối ưu hóa hiệu suất chương trình

## Tài liệu tham khảo

1. [Oracle Java Variables Guide](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html)
2. [Java Data Types](https://www.w3schools.com/java/java_data_types.asp)
3. [Java Programming Basics](https://www.tutorialspoint.com/java/java_basic_datatypes.htm)
