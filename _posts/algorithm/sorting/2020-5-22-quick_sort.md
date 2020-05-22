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



