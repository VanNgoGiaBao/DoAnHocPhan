---
title: "Lập trình Java cơ bản: Hello World"
date: 2025-10-24
tags: ["java", "cơ bản"]
categories: ["java"]
---

## Giới thiệu

Trong lập trình, chương trình "Hello World" là chương trình đầu tiên mà hầu hết các lập trình viên viết khi học một ngôn ngữ mới. Với Java, điều này cũng không ngoại lệ. Trong bài viết này, chúng ta sẽ tìm hiểu chi tiết về cách tạo và chạy chương trình Hello World trong Java, đồng thời giải thích từng thành phần của mã nguồn.

## Yêu cầu trước khi bắt đầu

Trước khi bắt đầu, bạn cần cài đặt:

1. **Java Development Kit (JDK)** - Phiên bản 8 trở lên
2. **Một trình soạn thảo mã nguồn** (IDE) - Khuyến nghị sử dụng:
   - IntelliJ IDEA
   - Eclipse
   - Visual Studio Code với Extension Pack for Java

## Cấu trúc chương trình Hello World

Đây là mã nguồn của chương trình Hello World trong Java:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

## Giải thích chi tiết từng thành phần

### 1. Khai báo lớp (Class Declaration)

```java
public class HelloWorld
```

- `public`: Là access modifier (bổ từ truy cập), cho phép lớp này có thể được truy cập từ bất kỳ đâu
- `class`: Keyword để khai báo một lớp trong Java
- `HelloWorld`: Tên của lớp, phải trùng với tên file (HelloWorld.java)

### 2. Phương thức main

```java
public static void main(String[] args)
```

- `public`: Cho phép JVM có thể truy cập phương thức này từ bên ngoài lớp
- `static`: Phương thức này thuộc về lớp, không cần tạo đối tượng để gọi
- `void`: Kiểu trả về - không trả về giá trị nào
- `main`: Tên của phương thức - điểm khởi đầu của chương trình
- `String[] args`: Mảng tham số dòng lệnh

### 3. In ra màn hình

```java
System.out.println("Hello World!");
```

- `System`: Lớp chứa các thành phần tiêu chuẩn của hệ thống
- `out`: Đối tượng PrintStream chuẩn để xuất dữ liệu
- `println()`: Phương thức in một dòng text và xuống dòng mới
- `"Hello World!"`: Chuỗi ký tự được in ra màn hình

## Các bước thực hiện

1. **Tạo file mới** với tên `HelloWorld.java`

2. **Viết mã nguồn** như đã trình bày ở trên

3. **Biên dịch chương trình**:
   ```bash
   javac HelloWorld.java
   ```
   Lệnh này sẽ tạo ra file `HelloWorld.class`

4. **Chạy chương trình**:
   ```bash
   java HelloWorld
   ```

## Một số biến thể

### 1. Sử dụng print thay vì println

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.print("Hello, ");
        System.out.print("World!");
    }
}
```

### 2. Sử dụng biến

```java
public class HelloWorld {
    public static void main(String[] args) {
        String message = "Hello World!";
        System.out.println(message);
    }
}
```

### 3. Sử dụng tham số dòng lệnh

```java
public class HelloWorld {
    public static void main(String[] args) {
        if (args.length > 0) {
            System.out.println("Hello, " + args[0] + "!");
        } else {
            System.out.println("Hello World!");
        }
    }
}
```

## Lỗi thường gặp và cách khắc phục

1. **Lỗi tên file không khớp với tên class**
   ```
   Error: Could not find or load main class HelloWorld
   ```
   🔧 Giải pháp: Đảm bảo tên file .java trùng với tên class

2. **Thiếu điểm phẩy**
   ```
   Error: ';' expected
   ```
   🔧 Giải pháp: Kiểm tra và thêm dấu chấm phẩy vào cuối câu lệnh

3. **Viết sai chữ hoa/thường**
   ```
   Error: Main method not found in class HelloWorld
   ```
   🔧 Giải pháp: Đảm bảo viết đúng `public static void main(String[] args)`

## IDE và công cụ phát triển

### IntelliJ IDEA
- Tự động tạo cấu trúc project
- Code completion thông minh
- Debugging dễ dàng

### Eclipse
- Miễn phí và open source
- Nhiều plugin hữu ích
- Giao diện quen thuộc

### Visual Studio Code
- Nhẹ và nhanh
- Extension Pack for Java
- Tích hợp terminal

## Kết luận

Chương trình Hello World tuy đơn giản nhưng đã giới thiệu cho chúng ta những khái niệm cơ bản trong Java như:
- Cấu trúc của một chương trình Java
- Cách khai báo lớp và phương thức
- Cách in dữ liệu ra màn hình
- Quy trình biên dịch và chạy chương trình

Đây là nền tảng quan trọng để tiếp tục học những khái niệm phức tạp hơn trong Java.

## Bài tập thực hành

1. Tạo chương trình in "Hello, [tên của bạn]!"
2. Sửa đổi chương trình để nhận tên người dùng từ bàn phím
3. In "Hello World" nhiều lần sử dụng vòng lặp

## Tài liệu tham khảo

1. [Oracle Java Documentation](https://docs.oracle.com/javase/tutorial/getStarted/application/index.html)
2. [Java Programming for Beginners](https://www.oracle.com/java/technologies/javase/java-tutorial-downloads.html)
3. [W3Schools Java Tutorial](https://www.w3schools.com/java/)
