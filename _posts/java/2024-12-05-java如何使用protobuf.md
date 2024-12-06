---
title: java如何使用protobuf
categories: [dev]
comments: true
---

### 1. protobuf简介
protobuf是google开发的一种数据交换格式，类似于json，xml等。但是protobuf是二进制的，所以比json和xml更加高效。protobuf的定义文件是.proto文件，通过这个文件可以生成对应的java代码。

### 2. protobuf的使用
#### 2.1 定义.proto文件
1. syntax ["proto2","proto3"] 字段表示使用的protobuf版本，如果不写默认是proto2。
``` proto
syntax = "proto3";
```
2. package 字段表示生成的java代码的包名。
``` proto
package com.example.protobuf;
```
3. 一些基本设置
``` proto
// 为true时，每一个消息类型都会生成一个独立的消息类型文件。
option java_multiple_files = true; 
// 生成的java代码的包名
option java_package = "com.example.protobuf"; 
// 生成的java代码的外部类名，如果不设置，则默认是.proto文件的文件名
option java_outer_classname = "PersonProto"; 
```
4. 定义消息类型
    + optional：字段可以设置，也可以不设置。如果未设置可选字段值，则使用默认值。对于简单类型，您可以指定自己的默认值，就像我们type在示例中对电话号码所做的那样。否则，将使用系统默认值：数字类型为零，字符串为空字符串，布尔类型为 false。对于嵌入式消息，默认值始终是消息的“默认实例”或“原型”，其中未设置任何字段。调用访问器来获取未明确设置的可选（或必需）字段的值始终返回该字段的默认值。
    + required：字段必须设置。如果您尝试构建消息而未设置必需字段，则编译器将抛出错误。这对于确保消息的完整性非常有用。
    + repeated：字段可以重复任意次数（包括零次）。重复字段的顺序将保留在消息中，因此可以按照添加它们的顺序读取它们。重复字段的元素可以按任何顺序读取。
    注：required 需要小心使用，如果在后面某个版本中删除了这个字段，那么之前的版本就无法解析这个字段了。
5. proto中的枚举
``` proto
message Person {
    string name = 1;
    int32 id = 2;
    string email = 3;

    enum PhoneType {
        MOBILE = 0;
        HOME = 1;
        WORK = 2;
    }

    message PhoneNumber {
        string number = 1;
        PhoneType type = 2;
    }
    repeated PhoneNumber phones = 4;
}
```




