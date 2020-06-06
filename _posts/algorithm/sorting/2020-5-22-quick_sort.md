---
title: 퀵소트 구현하기
published: true
updated: 2020-5-22
tags: [python, algorithm, quicksort]
categories: [development]
---

그래프에서 최소 비용 문제를 풀어보자

퀵소트를 구현해보자.



오름차순으로 코드를 작성하면 다음과 같다.

```python
def q_sort(arr: list, left, right):
    if left < right:
        pivot, lp, rp = left, left, right
        while lp < rp:
            while lp < right and arr[lp] >= arr[pivot]:
                lp += 1
            while rp > left and arr[rp] < arr[pivot]:
                rp -= 1
            if lp < rp:
                arr[lp], arr[rp] = arr[rp], arr[lp]
        if arr[pivot] <= arr[rp]:
            arr[rp], arr[pivot] = arr[pivot], arr[rp]
        q_sort(arr, left, rp - 1)
        q_sort(arr, rp + 1, right)


def quicksort(arr: list):
    q_sort(arr, 0, len(arr) - 1)
```



\+ 리버스가 구현된 코드

```python
def q_sort(arr, left, right, reverse):
    if left < right:
        pivot, lp, rp = left, left, right
        while lp < rp:
            while lp < right and (arr[lp] <= arr[pivot] if not reverse else arr[lp] >= arr[pivot]):
                lp += 1
            while rp > left and (arr[rp] > arr[pivot] if not reverse else arr[rp] < arr[pivot]):
                rp -= 1
            if lp < rp:
                arr[lp], arr[rp] = arr[rp], arr[lp]
        if arr[rp] <= arr[pivot] if not reverse else arr[rp] >= arr[pivot]:
            arr[rp], arr[pivot] = arr[pivot], arr[rp]
        q_sort(arr, left, rp - 1, reverse)
        q_sort(arr, rp + 1, right, reverse)


def quicksort(arr: list, reverse=False):
    q_sort(arr, 0, len(arr) - 1, reverse)
```



\+ 조건을 따로 주어서 코드를 짜는 방법

```python
def condition(arr, piv, point):
    if arr[piv] >= arr[point]:
        return True
    else:
        return False


def q_sort(arr, left, right):
    if left < right:
        pivot, lp, rp = left, left, right
        while lp < rp:
            while lp < right and condition(arr, pivot, lp):
                lp += 1
            while rp > left and not condition(arr, pivot, rp):
                rp -= 1
            if lp < rp:
                arr[lp], arr[rp] = arr[rp], arr[lp]
        if condition(arr, pivot, rp):
            arr[pivot], arr[rp] = arr[rp], arr[pivot]
        q_sort(arr, left, rp - 1)
        q_sort(arr, rp + 1, right)


def quicksort(arr):
    q_sort(arr, 0, len(arr) - 1)


quicksort(array)
```

> 위의 코드는 오름차순을 기준으로 작성된 코드다. condition의 조건을 변경하여 내가 원하는 대로 정렬이 가능하다. 
>
> 가령, 정렬의 기준이 복잡할 경우 condition 함수에서 처리를 해주면 간단하다.