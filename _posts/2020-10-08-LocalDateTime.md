---
title: "Java에서 날짜, 시간 표현하기"
categories: JAVA LocalDateTime LocalDate LocalTime
date: 2020-10-08
last_modified_at: now
---



- 기존에 쓰던 Date, Calendar 클래스는 문제점이 많다 ex) 헷갈리는 월 표현, 상수 필드 남용 등
- 그래서 JAVA8부터는 LocalDate, LocalTime, LocalDateTime을 쓰는 게 좋다


## 기본 사용 법
```java
    LocalDate currentDate = LocalDate.now(); //현재 날짜
    //LocalDate myDate = LocalDate.of(2020, 10, 8);

    
    System.out.println(currentDate.getYear()); //년도
    System.out.println(currentDate.getMonth()); // 월 ( ex JANUARY,, ) 
    System.out.println(currentDate.getMonthValue()); // 월 ( ex 1 ,, )
    System.out.println(currentDate.getDayOfMonth()); // 날짜
    System.out.println(currentDate.getDayOfWeek()); // 요일 ( ex Monday ,,, )
    
    
    LocalTime currentTime = LocalTime.now();
    //LocalTime myTime = LocalTime.of(9, 0, 0, 0); //9시 00분 00.000 초
    
    System.out.println(currentTime.getHour()); //시간
    System.out.println(currentTime.getMinute()); //분
    System.out.println(currentTime.getSecond()); //초
    System.out.println(currentTime.getNano()); //9자리로 
    
    
    LocalDateTime currentDateTime = LocalDateTime.now();    // 컴퓨터의 현재 날짜와 시간 정보. 결과 : 2018-07-26T16:34:24.757
    //LocalDateTime targetDateTime = LocalDateTime.of();
    ZonedDateTime utcDateTime = ZonedDateTime.now(ZoneId.of("UTC"));
    ZonedDateTime seoulDateTime = ZonedDateTime.now(ZoneId.of("Asia/Seoul"));
    
    System.out.println("-------");
    System.out.println(currentDateTime.toString());
    System.out.println(utcDateTime.toString());
    System.out.println(seoulDateTime.toString());

```
***

## 날짜/ 시간 변환


```java

    //LocalDate -> String
    LocalDate.of(2020, 10, 8).format(DateTimeFormatter.BASIC_ISO_DATE); //20201008
    
    //LocalDateTime -> String
    LocalDateTime.now().format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")); // 2020-10-08 21:00:00
    
    //LocalDateTime -> java.util.Date
    Date.from(LocalDateTime.now().atZone(ZoneId.systemDefault()).toInstant());
    
    //LocalDate -> java.sql.Date
    java.sql.Date.valueOf(LocalDate.of(2020, 10, 8));
    
    //LocalDateTime -> java.sql.Timestamp
    Timestamp.valueOf(LocalDateTime.now());
    
    //String -> LocalDate
    LocalDate.parse("2020-10-09");
    LocalDate.parse("20201009", DateTimeFormatter.BASIC_ISO_DATE);
    
    //String -> LocalDateTime
    LocalDateTime.parse("2020-10-08T21:09:30");
    LocalDateTime.parse("2020-10-08 21:10:00", DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss")); 
    
    //java.util.Date -> LocalDateTime
    LocalDateTime.ofInstant(new Date().toInstant(), ZoneId.systemDefault());
    
    //java.sql.Date -> LocalDate
    new java.sql.Date(System.currentTimeMillis()).toLocalDate();
    
    
    //java.sql.Timestamp -> LocalDateTime
    new Timestamp(System.currentTimeMillis()).toLocalDateTime();
    
    //LocalDateTime -> LocalDate
    LocalDate.from(LocalDateTime.now());
    
    // LocalDate -> LocalDateTime
    LocalDate.now().atTime(21, 30);
```
***




[참고](https://jeong-pro.tistory.com/163)