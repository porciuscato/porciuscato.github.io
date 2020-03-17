---
comments: true
title: javascript, python, C++, java collection 연습
published: false
updated: 2020-3-17
tags: [javascript, python, C++, java]
categories: [development]
---

collection 연습



# Collection

다음의 javascript 코드는 중복이 많다. 이를 Collection을 통해 간단화시켜보자.

```javascript
const date = new Date()
const year = date.getFullYear()
const month = date.getMonth()
let days = null

switch(month) {
    case 0:
    case 2:
    case 4:
    case 6:
    case 7:
    case 9:
    case 11:
        days = 31
        break
    case 3:
    case 5:
    case 8:    
    case 10:
        days = 30
        break
    case 1:
        if ((year % 4 == 0) && (year % 100 != 0) || (year % 400) == 0) days = 29
        else days = 28
        break
}

console.log(days + ' days for ' + year + '-' + (month + 1))
```



## Javascript

### 방법 1) 1차 배열

```javascript
const date = new Date()
const year = date.getFullYear()
const month = date.getMonth()
let days = null

function Feb(year) {
    if ((year % 4 == 0) && (year % 100 != 0) || (year % 400) == 0) return 29
    else return 28
}

let days_array = [31, Feb(year), 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

days = days_array[month]

console.log(days + ' days for ' + year + '-' + (month + 1))
```

### 방법 2) 2차 배열

```javascript
const date = new Date()
const year = date.getFullYear()
const month = date.getMonth()
let days = null

function Feb(year) {
    if ((year % 4 == 0) && (year % 100 != 0) || (year % 400) == 0) return 29
    else return 28
}

let days_list = [
    [[0, 2, 4, 6, 7, 9, 11], 31],
    [[3, 5, 8, 10], 30],
    [[1], Feb(year)]
]

for (let idx in days_list){
    if (month in days_list[idx][0]){
        days = days_list[idx][1]
        break
    }
}

console.log(days + ' days for ' + year + '-' + (month + 1))
```

### 방법 3) 오브젝트

```javascript
const date = new Date()
const year = date.getFullYear()
const month = date.getMonth()
let days = null

function Feb(year) {
    if ((year % 4 == 0) && (year % 100 != 0) || (year % 400) == 0) return 29
    else return 28
}

let days_object = {
    0: 31, 2: 31, 4: 31, 6: 31, 7: 31, 9: 31, 11: 31,
    3: 30, 5: 30, 8: 30, 10: 30, 1: Feb(year)
}

days = days_object[month]

console.log(days + ' days for ' + year + '-' + (month + 1))
```



## Python

### 방법 1) 1차 배열

```python
import datetime

NOW = datetime.datetime.now()
YEAR = NOW.year
MONTH = NOW.month
days = None

def Feb(year):
    if (year % 4 == 0) and (year % 100 != 0) or (year % 400) == 0:
        return 29
    else:
        return 28

days_list = [31, Feb(YEAR), 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

days = days_list[MONTH - 1]

print('{} days for {}-{}'.format(days, YEAR, MONTH))
```

### 방법 2) 2차 배열

```python
import datetime

NOW = datetime.datetime.now()
YEAR = NOW.year
MONTH = NOW.month
days = None

def Feb(year):
    if (year % 4 == 0) and (year % 100 != 0) or (year % 400) == 0:
        return 29
    else:
        return 28

days_list = [
    [[1, 3, 5, 7, 8, 10, 12], 31],
    [[4, 6, 9, 11], 30],
    [[2], Feb(YEAR)]
]

for val in days_list:
    if MONTH in val[0]:
        days = val[1]
        break

print('{} days for {}-{}'.format(days, YEAR, MONTH))
```

### 방법 3) 오브젝트

```python
import datetime

NOW = datetime.datetime.now()
YEAR = NOW.year
MONTH = NOW.month
days = None

def Feb(year):
    if (year % 4 == 0) and (year % 100 != 0) or (year % 400) == 0:
        return 29
    else:
        return 28

days_object = {
    1: 31, 3: 31, 5: 31, 7: 31, 8: 31, 10: 31, 12: 31,
    4: 30, 6: 30, 9: 30, 11: 30, 2: Feb(YEAR)
}

days = days_object[MONTH]

print('{} days for {}-{}'.format(days, YEAR, MONTH))
```



## C++

### 방법 1) 1차 배열

```cpp
#include <iostream>
#include <string>
#include <ctime>
using namespace std;

int Feb(int year) {
    if ((year % 4 == 0) && (year % 100 != 0) || (year % 400) == 0){
        return 29;
    }
    else return 28;
}

int main() {
    time_t now = time(0);

    tm *ltm = localtime(&now);
    int year = ltm->tm_year + 1900;
    int month = ltm->tm_mon + 1;
    int days;
    
    int days_array[12] = {31, Feb(year), 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
    days = days_array[month - 1];
    cout << days << " days for " << year << "-" << month;
}
```

### 

## Java

### 방법 1) 1차 배열

```java
import java.time.LocalDate;

public class java_1 {
	public static void main(String[] args) {
		LocalDate NOW = LocalDate.now();
		int year = NOW.getYear();
		int month = NOW.getMonthValue();
		int days;
		
		int[] days_list = {31, Feb(year), 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
		
		days = days_list[month - 1];
		
		System.out.printf("%d days for %d-%d\n", days, year, month);
	}
	public static int Feb(int year) {
	    if ((year % 4 == 0) && (year % 100 != 0) || (year % 400) == 0){
	        return 29;
	    }
	    else return 28;
	}
}
```