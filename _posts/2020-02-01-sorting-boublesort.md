---
title: "[알고리즘]기본정렬01. 버블정렬(bubble sort)"
date: 2020-02-01 01:00:00
categories: [Algorithm, Algorithm_theory]
tags: [algorithm, sorting, bubble sort, 알고리즘, 버블정렬]
---
## 목표
> * 버블 정렬(bubble sort) 알고리즘을 이해하고 코드로 구현할 수 있다.   
> * 버블 정렬(bubble sort) 알고리즘의 특징을 설명할 수 있다.   
> * 버블 정렬(bubble sort) 알고리즘의 시간복잡도를 계산할 수 있다.

들어가기 전

* 정렬(sorting)이란?
  - 정렬(sorting): 여러 데이터들이 주어졌을 때 이를 정해진 순서대로 나열하는 것
  - 정렬 알고리즘의 종류 : 버블정렬, 선택정렬, 삽입정렬, 퀵정렬, 병합정렬   

------------------------------------------------------

### 1. 버블 정렬(bubble sort)이란?
* 두 개의 인접한 데이터를 비교해서 정렬하는 알고리즘
  - 인접한 2개의 데이터 중 앞 데이터가 정렬 기준 순서에서 뒤면 위치를 바꾼다

* 특징
  - 구현이 간단하지만 시간복잡도가 O(n^2)으로 매우 느리다.

![](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)


> 출처: <https://en.wikipedia.org/wiki/Bubble_sort>

### 2. 버블 정렬(bubble sort) 예제
* 데이터가 4개일 때 [9, 20, 12, 5]
  - 1회전
    + 9 와 20을 비교
      + 9가 20보다 더 작으므로 변화없음 : [9, 20, 12, 5]
    + 20 과 12를 비교
      + 20이 12보다 더 크므로 자리바꿈 : [9, 12, 20, 5]
    + 20 과 5를 비교
      + 20이 5보다 더 크므로 자리바꿈: [9, 12, 5, 20]
      + 20은 정렬 완료
  - 2회전
    + 9와 12를 비교
      + 9가 12보다 더 작으므로 변화없음 : [9, 12, 5, 20]
    + 12 와 5를 비교
      + 12가 5보다 더 크므로 자리바꿈 : [9, 5, 12, 20]
    + 20은 이미 정렬된 상태이므로 더 이상 비교할 필요 없음
    + 12, 20 정렬 완료
  - 3회전
    + 9 와 5를 비교
      + 9가 5보다 더 크므로 자리바꿈 : [5, 9, 12, 20]
    + 12와 20은 이미 정렬된 상태이므로 더 이상 비교할 필요 없음
    + 전체 정렬 완료

> [참고] 그림으로 이해하기 : <https://visualgo.net/en/sorting>

### 3. 버블 정렬(bubble sort) 코드로 구현하기

* in Python
```python
def bubble_sort(data):
    for i in range(len(data)-1):
        swap = False
        for j in range(len(data)-i-1):
            if data[j] > data[j+1]:
                data[j], data[j+1] = data[j+1], data[j]
                swap = True

        if swap == False:           # 이미 다 정렬됨
            break

  data_list = [9, 20, 12, 5]
  bubble_sort(data_list)
  print(data_list)                # 결과 [5, 9, 12, 20]
```

### 4. 버블 정렬(bubble sort) 시간복잡도

* n-1, n-2, n-3, ..., 2, 1 번 비교
  - n(n-1)/2 = O(n^2)

* 이미 정렬이 되어 있는 경우라면 n-1번 비교
  - O(n)
