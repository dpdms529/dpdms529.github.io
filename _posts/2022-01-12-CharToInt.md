---
layout: single
title: "Char To Int"
excerpt: "char형 숫자를 int형으로 바꾸는 법"
date: 2022-01-12T02:58:00+09:00
toc: true
toc_sticky: true
categories:
  - PL
  - JAVA
tags:
  - PL
  - JAVA
---
## char형 숫자를 int형으로 바꾸는 법
```java
char c = '5';
int i = c - '0';
```
또는
```java
char c = '5';
int i = Character.getNumericValue(c);
```