---
title: "[알고리즘]정렬알고리즘 03. 삽입정렬(insertion sort)"
date: 2020-02-03 11:30:00 +0800
categories: [Algorithm, Algorithm_theory]
tags: [algorithm, sorting, insertion sort, 알고리즘, 삽입정렬]
---
## 목표
> * 삽입 정렬(insertion sort) 알고리즘을 이해하고 코드로 구현할 수 있다.
> * 삽입 정렬(insertion sort) 알고리즘의 특징을 설명할 수 있다.
> * 삽입 정렬(insertion sort) 알고리즘의 시간복잡도를 계산할 수 있다.

##### 선수지식

* 정렬(sorting)이란?
  - 정렬(sorting): 여러 데이터들이 주어졌을 때 이를 정해진 순서대로 나열하는 것
  - 정렬 알고리즘의 종류 : [버블정렬], [선택정렬], [삽입정렬], [퀵정렬], [합병정렬] 등

[버블정렬]: /posts/sorting-bubblesort
[선택정렬]:/posts/sorting-selectionsort
[삽입정렬]:/posts/sorting-insertionsort
[퀵정렬]:/posts/sorting-quicksort
[합병정렬]:/posts/sorting-mergesort
------------------------------------------------------
### 1. 삽입 정렬(insertion sort)이란 ?

* 데이터의 모든 요소를 앞에서부터 차례대로 이미 정렬된 부분과 비교하여 자신의 위치에 삽입하는 정렬 알고리즘
  1. 두번째 인덱스부터 시작한다
  2. 해당 인덱스(key값) 앞에 있는 데이터(B)부터 비교해서 key값이 더 작으면 B를 뒤로 shift
  3. key값보다 작은 데이터를 만나면 해당 데이터 뒤에 key값을 넣고 key값에는 다음인덱스에 있는 데이터를 넣는다.
  4. 정렬이 완료 될 때까지 위 과정(2~3)을 반복한다.

* 특징
  - 장점
    + 구현이 간단하다.
    + in-place 알고리즘이다.
    + 안정(stable) 정렬이다.
      + 동일한 키 값에 대해 기존의 순서가 유지되는 정렬방식
    + 시간복잡도가 같은 선택정렬이나 거품정렬과 같은 알고리즘에 비교하여 빠르다
  - 단점
    + 배열이 길어지면 효율이 떨어진다.

  ![](https://upload.wikimedia.org/wikipedia/commons/9/9c/Insertion-sort-example.gif)

> 출처: <https://commons.wikimedia.org/wiki/File:Insertion-sort-example.gif>

### 2. 삽입 정렬(insertion sort) 예제
* 데이터가 [9, 20, 12, 5] 라고 가정하면
  - 1회전
    + key : 20
    + 앞에 있는 데이터 9 와 비교 : 20(key)이 크므로 변화 없음
    + 9 정렬 완료 [**9**, 20, 12, 5]
  - 2회전
    + key : 12
    + 앞에 있는 데이터 20 과 비교 : 12(key)가 작으므로 20 shift [9, &nbsp;, <U>20</U>, 5]
    + 그 다음 앞에 있는 데이터 9 와 비교 : 12(key)가 크므로 9 뒤에 12 삽입
    + 9, 12 정렬 완료 [**9**, **12**, 20, 5]
  - 3회전
    + key : 20
    + 앞에 있는 데이터 12와 비교 : 20(key)이 크므로 반복 종료
      + 9 와 12는 이미 정렬 되어 있는 상태이므로 더 이상 비교할 필요가 없음
    + 9, 12, 20 정렬 완료 [**9**, **12**, **20**, 5]
  - 4회전
    + key : 5
    + 앞에 있는 데이터 20 과 비교 : 5(key)가 더 작으므로 20 shift [9, 12, &nbsp; , <U>20</U>]
    + 그 다음 앞에 있는 데이터 12 와 비교: 5(key)가 더 작으므로 12 shift [9, &nbsp; , <U>12</U>, 20]
    + 그 다음 앞에 있는 데이터 9 와 비교: 5(key)가 더 작으므로 9 shift [ &nbsp; ,<U>9</U>, 12, 20]
    + 더 이상 비교 대상 없으므로 5를 맨 앞자리에 삽입
    + 전체 정렬 완료 [**5**, **9**, **12**, **20**]

> [참고] 그림으로 이해하기 : <https://visualgo.net/en/sorting>

### 3. 삽입 정렬(insertion sort) 코드로 구현하기

* in Python
```python
# 삽입정렬(insertion sort)
def inserted_sort(data):
    for i in range(1,len(data)):
        key = data[i]
        j = i
        while j > 0 and data[j-1] > key:
            data[j] = data[j-1]
            j -= 1
        data[j] = key

  data_list = [9, 20, 12, 5]      # 결과 [5, 9, 12, 20]
  inserted_sort(data_list)
  print(data_list)
```   

### 4. 삽입 정렬(insertion sort) 시간 복잡도

* n(n-1)/2 번 비교 및 교환= O(n^2)
* 이미 정렬되어 있는 경우라면 n-1번 비교
  - O(n)

------------------------------------------------
## 참고자료
> * <https://fun-coding.org>
> * [삽입정렬-위키백과]

[삽입정렬-위키백과]:https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC
