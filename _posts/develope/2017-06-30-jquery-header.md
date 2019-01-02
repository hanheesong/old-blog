---
layout: amp
title: "javascript 배열"
description: ""
tag: []
category: develope
sitemap:
  changefreq: daily
---

배열 만들기
1. 리터럴로
var empty=[]; ㅇㅒ도 배열
var misc = [1.1, true, "a",]; 얘도 배열

var count = [1,,2]
var aa = [,,] => 원소갯수는 2개임
배열 리터럴 문법은 마지막 원소 다음에 쉼표를 추가 할 수 있다고 명시하고 있음

2. Array() 생성자
호출 방법은 3가지가 있음

* 빈배열 생성 = 리터럴과 동일
var a = Array();

* 배열의 길이를 의미하는 숫자 값을 인자로 줘 호출
var a = new Array(10);

* 두개 이상의 원소 또는 숫자가 아닌 원소 값 하나를 명시적으로 지정하는 방법
var a = new Array(5,4,3,2,1,"testing, testing");
근데 이건 배열의 생성자를 사용하는 것보다 리터럴로 사용하ㅡㄴ 것이 더 편함.


희소배열
var a1 = [,,,]; => 세 개의 원소가 undefined인 배열
var a2 = new Array(3) => 원소개 존재하지않고 length가 3인
0 in a1 // => true : a1에는 0번쨰 인덱스 위치에 원소가 존재
0 in a2 // => false : a2에는 원소가 존재하지 X

배열의 length는 가장 큰 인덱스 값보다 하나 더 큰 값
그래서 마지막 배열의 인덱스 을 나타낼땐 배열.length-1 처리해줘야함.
[].length -> 원소가 없는 배열 이므로 length는 0
['a','b','c'].length -> 가장 큰 인덱스는 2고, length는 3임

# 배열은 읽기 전용으로 쓸수도있음
a = [1,2,3];
Object.defineProperty(a, "length", {writable:false});
a.length=0하게 되도 변하지않음.

# 배열 원소 지우기
a = [1,2,3];
delete a[1]; //=> 인덱스가 1인 값을 지운다
delete 해도 원소의 개수는 변하지 않음
