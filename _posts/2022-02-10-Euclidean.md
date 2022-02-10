---
layout: single
title: "[Algorithm] 유클리드호제법"
excerpt: "최대공약수(GCD)와 최소공배수(LCM) 구하기"
date: 2022-02-10
last_modified_at: 2022-02-10
toc: true
toc_sticky: true
categories:
  - Algorithm
tags:
  - Algorithm
  - JAVA
---

## 유클리드호제법이란?
- 최대 공약수를 구하는 알고리즘
- 2개의 자연수 a, b (단, a>b) 에 대하여 a를 b로 나눈 나머지를 r이라 하면, a와 b의 최대공약수는 b와 r의 최대공약수와 같다.
- 이 성질을 이용하여 b를 r로 나눈 나머지를 구하는 과정을 반복하여 나머지가 0이 됐을 때 나누는 수가 a와 b의 최대공약수가 된다.

참조 : [위키피디아-유클리드호제법](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)

## 최대공약수를 구하는 알고리즘
최대공약수는 유클리드호제법을 사용하여 a(큰 수)를 b(작은 수)로 나눈 나머지(r)가 0이 될 때까지 b와 r 값을 인수로 하여 gcd 함수를 재귀적으로 호출한다.
a를 b로 나눈 나머지(r)가 0이 되면 b(작은 수)를 반환한다.

```java
int gcd(int a, int b){
  int r = a%b;
  if(r==0) return b;
  else return gcd(b, r);
}
```
## 최소공배수를 구하는 알고리즘
최소공배수는 두 자연수의 곱을 최대공약수로 나누어 구할 수 있다.
```java
int lcm = a*b/gcd(a,b);
```
