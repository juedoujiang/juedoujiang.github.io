---
title: New Java Learning
categories: Java Learning Notes
tags: Java
---



# Week1

## java变量变常量

### 在变量前加final



## println 和 print区别

### println后面需要加回车才可以进行下一步；print直接输出，不需要加回车



## 强制类型转换

###  (int)x



# Week3

## 验证规则

### 测试常用边界数据

* 个位数
* 10
* 0
* 负数



# Week4

## 标号

* 在循环前可以放一个label：来标示循环
* 可以用于跳出多重循环



# Week 5

## 普通变量和数组变量

* 普通数组是所有者

* 数组变量是管理者


  <center>
      <img src = "https://raw.githubusercontent.com/juedoujiang/PictureBed/main/img/普通变量和数组变量1.png">
      <center>5.1 Java数组变量原理</center>
  </center>

  <center>
      <img src="https://raw.githubusercontent.com/juedoujiang/PictureBed/main/img/普通变量和数组变量2.png">
      <center>5.2 Java数组变量原理2</center>
  </center>


## 数组变量

* 数组变量是数组的管理者而非数组本身

* 数组必须创建出来然后交给数组变量来管理

* 数组变量之间的赋值是管理权限的赋予

* 数组变量之间的比较是判断是否管理同一个数组

## 复制数组

* 必须遍历源数组将每个元素逐一拷贝给目的数组

  ```java
  int[] a = {1,2,3,4,5};
  int[] b = new int[a.length];
  for(int i=0;i<b.length;i++)
  {
  	b[i] = a[i];
  }
  ```

## For-Each循环

* For-Each循环的形式

  ```java
  for (k:data)
  {
  	//遍历data中的每一个数据
  }
  ```


##  构造素数表

* 欲构造n以内的素数表
* 1.令x为2
* 2.将2x、3x、4x直至ax<n的数标记为非素数
* 3.令x为下一个没有被标记为非素数的数，重复2；直到所有的数都已经尝试完毕

# Week6

## 包裹类型

| 基础类型 | 包裹类型  |
| :------: | :-------: |
| boolean  |  Boolean  |
|   char   | Character |
|   int    |  Integer  |
|  double  |  Double   |

## 字符串

* String使用`.equals`进行比较

  ```java
  in.next();//读入单词
  in.nextLine();//读入字符串
  ```

  

## 字符串比较

* 字符串是对象，对它的所有操作是通过`.`运算符进行的
* 字符串大小的比较`str1.compareTo(str2)`、`str1.compareToIgnoreCase(str2)`
* 字符串长度大小`str.length()`
* 访问String里的字符`str1.charAt(Index)`
* 字符串子串`str.substring(n)`or`str.substring(b,e)//不包括第e个`
* 寻找某个字符串是否存在
* `s.indexOf(c)\s.indexOf(c,n)\s.indexOf(s)\s.lastIndexOf(c)\s.lastIndexOf(c)`
* 其他String操作
  * `s.startsWith(t)`
  * `s.endsWith(t)`
  * `s.trim()`
  * `s.replace(c1,c2)`
  * `s.toLowerCase()`
  * `s.toUpperCase()`