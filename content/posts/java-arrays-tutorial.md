---
title: "Lập trình Java: Hướng dẫn toàn diện về Mảng (Arrays)"
date: 2025-10-24
tags: ["java", "cơ bản"]
categories: ["java"]
---

## Giới thiệu

Mảng (Array) là một trong những cấu trúc dữ liệu cơ bản và quan trọng nhất trong Java. Mảng cho phép lưu trữ nhiều phần tử cùng kiểu dữ liệu trong một biến duy nhất. Trong bài viết này, chúng ta sẽ tìm hiểu chi tiết về cách sử dụng mảng trong Java.

## Yêu cầu trước khi bắt đầu

1. **Java Development Kit (JDK)** - Phiên bản 8 trở lên
2. **Một IDE** (Môi trường phát triển tích hợp):
   - IntelliJ IDEA
   - Eclipse
   - Visual Studio Code với Extension Pack for Java

## Khai báo và khởi tạo mảng

### 1. Khai báo mảng

Có hai cách để khai báo mảng trong Java:

```java
// Cách 1
int[] numbers;
String[] names;

// Cách 2
int numbers[];
String names[];
```

### 2. Khởi tạo mảng

```java
// Khởi tạo với kích thước cố định
int[] numbers = new int[5];

// Khởi tạo với giá trị ban đầu
int[] numbers = {1, 2, 3, 4, 5};
String[] fruits = {"apple", "banana", "orange"};
```

## Các thao tác cơ bản với mảng

### 1. Truy cập phần tử

```java
int[] numbers = {1, 2, 3, 4, 5};
System.out.println(numbers[0]); // In ra 1
System.out.println(numbers[4]); // In ra 5
```

### 2. Thay đổi giá trị phần tử

```java
int[] numbers = new int[3];
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
```

### 3. Duyệt mảng

```java
// Sử dụng vòng lặp for
int[] numbers = {1, 2, 3, 4, 5};
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

// Sử dụng for-each
for (int number : numbers) {
    System.out.println(number);
}
```

## Các tính năng nâng cao

### 1. Mảng đa chiều

```java
// Mảng 2 chiều
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Truy cập phần tử
System.out.println(matrix[0][0]); // In ra 1
```

### 2. Sao chép mảng

```java
// Sử dụng System.arraycopy()
int[] source = {1, 2, 3};
int[] destination = new int[3];
System.arraycopy(source, 0, destination, 0, source.length);

// Sử dụng Arrays.copyOf()
int[] newArray = Arrays.copyOf(source, source.length);
```

### 3. Sắp xếp mảng

```java
int[] numbers = {5, 2, 8, 1, 9};
Arrays.sort(numbers);
// Kết quả: {1, 2, 5, 8, 9}
```

## Các phương thức hữu ích của lớp Arrays

```java
import java.util.Arrays;

public class ArraysDemo {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        
        // Chuyển mảng thành chuỗi
        System.out.println(Arrays.toString(numbers));
        
        // Tìm kiếm phần tử
        int index = Arrays.binarySearch(numbers, 3);
        
        // So sánh mảng
        int[] array2 = {1, 2, 3, 4, 5};
        boolean isEqual = Arrays.equals(numbers, array2);
        
        // Điền giá trị
        Arrays.fill(numbers, 0);
    }
}
```

## Lỗi thường gặp và cách khắc phục

1. **ArrayIndexOutOfBoundsException**
   ```java
   int[] numbers = new int[3];
   numbers[3] = 10; // Lỗi: Index 3 nằm ngoài phạm vi
   ```
   🔧 Giải pháp: Kiểm tra kích thước mảng trước khi truy cập

2. **NullPointerException**
   ```java
   int[] numbers;
   System.out.println(numbers.length); // Lỗi: numbers chưa được khởi tạo
   ```
   🔧 Giải pháp: Khởi tạo mảng trước khi sử dụng

3. **Lỗi khi so sánh mảng**
   ```java
   int[] arr1 = {1, 2, 3};
   int[] arr2 = {1, 2, 3};
   System.out.println(arr1 == arr2); // false
   ```
   🔧 Giải pháp: Sử dụng Arrays.equals() để so sánh

## Ví dụ thực tế

### 1. Tính điểm trung bình

```java
public class AverageCalculator {
    public static void main(String[] args) {
        double[] scores = {85.5, 90.0, 78.5, 92.5, 88.0};
        double sum = 0;
        
        for (double score : scores) {
            sum += score;
        }
        
        double average = sum / scores.length;
        System.out.println("Điểm trung bình: " + average);
    }
}
```

### 2. Tìm phần tử lớn nhất

```java
public class MaxFinder {
    public static void main(String[] args) {
        int[] numbers = {45, 67, 23, 89, 12};
        int max = numbers[0];
        
        for (int number : numbers) {
            if (number > max) {
                max = number;
            }
        }
        
        System.out.println("Số lớn nhất: " + max);
    }
}
```

## Bài tập thực hành

1. Viết chương trình đảo ngược một mảng
2. Tìm phần tử xuất hiện nhiều nhất trong mảng
3. Tách mảng thành hai mảng con chứa số chẵn và số lẻ
4. Thực hiện phép cộng hai ma trận (mảng 2 chiều)

## Các thư viện và công cụ hữu ích

1. **java.util.Arrays**
   - Các phương thức tiện ích cho mảng
   - Sort, search, fill, copy

2. **java.util.ArrayList**
   - Thay thế cho mảng khi cần kích thước động
   - Nhiều phương thức tiện ích hơn

3. **Apache Commons Lang**
   - ArrayUtils
   - Các phương thức bổ sung cho mảng

## Kết luận

Mảng là một cấu trúc dữ liệu cơ bản nhưng mạnh mẽ trong Java. Hiểu và sử dụng thành thạo mảng sẽ giúp bạn:
- Quản lý dữ liệu hiệu quả
- Tối ưu hóa bộ nhớ
- Xử lý nhiều phần tử dữ liệu cùng lúc
- Tạo nền tảng cho các cấu trúc dữ liệu phức tạp hơn

## Tài liệu tham khảo

1. [Oracle Java Arrays Tutorial](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html)
2. [Java Arrays Documentation](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html)
3. [W3Schools Java Arrays](https://www.w3schools.com/java/java_arrays.asp)
