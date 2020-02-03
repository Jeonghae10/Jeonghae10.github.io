---
title: "[알고리즘]정렬알고리즘 02. 선택정렬(selction sort)"
date: 2020-02-03 11:00:00 +0800
categories: [Algorithm, Algorithm_theory]
tags: [algorithm, sorting, selection sort, 알고리즘, 선택정렬]
---
## 목표
> * 선택 정렬(selction sort) 알고리즘을 이해하고 코드로 구현할 수 있다.   
> * 선택 정렬(selction sort) 알고리즘의 특징을 설명할 수 있다.   
> * 선택 정렬(selction sort) 알고리즘의 시간복잡도를 계산할 수 있다.

##### 선수지식

* 정렬(sorting)이란?
  - 정렬(sorting): 여러 데이터들이 주어졌을 때 이를 정해진 순서대로 나열하는 것
  - 정렬 알고리즘의 종류 : [버블정렬], [선택정렬], [삽입정렬], [퀵정렬], [병합정렬] 등

[버블정렬]: /posts/sorting-bubblesort
[선택정렬]:/posts/sorting-selectionsort
[삽입정렬]:/posts/sorting-insertionsort
[퀵정렬]:/posts/sorting-quicksort
[병합정렬]:/posts/sorting-mergesort

----------------------------------------------------------------
### 1. 선택 정렬(selection sort)이란 ?

* 정렬되지 않은 리스트 중에서 최솟값을 선택하여 정렬하는 알고리즘
  1. 주어진 리스트 중에 최솟값을 찾는다
  2. 그 값을 맨 앞에 위치한 값과 교환한다(swap)
  3. 맨 처음 위치를 뺀 나머지 리스트에 대해서 위 과정(1~2)을 반복한다.   

* 특징
  - 제자리 정렬 알고리즘 중 하나이다.
    + 사용할 수 있는 메모리가 제한적인 경우에 사용시 성능상의 이점이 있다.



  ![](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)

  > 출처: <https://en.wikipedia.org/wiki/Selection_sort>

### 2. 선택 정렬(selection sort) 예제
 * 데이터가 [9, 20, 12, 5] 라고 가정하면
    - 1회전
      + 리스트의 최솟값 : 5
      + 맨 앞 데이터인 9 와 자리바꿈 : [<U>5</U>, 20, 12, <U>9</U>]
      + 5 정렬 완료 [**5**, 20, 12, 9]
    - 2회전
      + 정렬되지 않은 리스트(5를 제외한 나머지)에서 최솟값 : 9
      + 맨 앞 데이터인 20 과 자리바꿈 : [5, <U>9</U>, 12, <U>20</U>]
      + 5, 9 정렬 완료 [**5**, **9**, 12, 20]
    - 3회전
      + 정렬되지 않은 리스트(5, 9를 제외한 나머지)에서 최솟값: 12
      + 12는 이미 맨 앞이므로 변화 없음
      + 마지막 데이터는 비교할 게 없으므로 반복 종료
      + 전체 정렬 완료 [**5**, **9**, **12**, **20**]

> [참고] 그림으로 이해하기 : <https://visualgo.net/en/sorting>

### 3. 선택 정렬(selection sort) 코드로 구현하기

* in Python
```python
def selection_sort(data):
    for i in range(len(data)-1):
        min_index = i
        for j in range(i+1, len(data)):
            if data[min_index] > data[j]:
                min_index = j
        data[i], data[min_index] = data[min_index], data[i]

  data_list = [9, 20, 12, 5]
  selection_sort(data_list)
  print(data_list)                # 결과 [5, 9, 12, 20]
```

### 4. 선택 정렬(selection sort) 시간복잡도

* n(n-1)/2 번 비교 = O(n^2)
  - 교환은 n-1번

------------------------------------------------
## 참고자료
> * <https://fun-coding.org>
> * [선택정렬-위키백과]

[선택정렬-위키백과]:https://ko.wikipedia.org/wiki/%EA%B1%B0%ED%92%88_%EC%A0%95%EB%A0%AC
