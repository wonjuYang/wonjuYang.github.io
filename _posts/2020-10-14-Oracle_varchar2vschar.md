---
title: "오라클 CHAR vs VARCHAR2 차이"
categories: Oracle datatype char varchar2
date: 2020-10-14
last_modified_at: 2020-10-14
---


# 데이터 타입
## 1) CHAR(size) : 고정길이 문자열 데이터 타입, size보다 작은 크기의 문자열을 저장하면 남은 공간만큼 공백으로 채워넣어 원래 설정인 size만큼 메모리에 저장 
<br/>

## ex) 주민번호, 제품 번호 
<br/> <br/>

## 2)VARCHAR2(size) : 가변길이 문자열 데이터 타입, size보다 작은 크기의 문자열을 저장하면 빈 공간에 null을 넣어 원래 넣고자 한 문자열 크기만큼 메모리에 저장
<br/>

## ex) 문자열을 비교할 때
<br/> <br/>




# VARCHAR2는 저장하고자 했던 문자열만큼 저장되니 상관이 없지만 CHAR은 빈 공간만큼 공백을 채워서 저장해 비교연산 실행시 주의해야 한다

