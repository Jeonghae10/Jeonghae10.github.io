---
title: "[알고리즘]정렬알고리즘 04. 퀵정렬(quick sort)"
date: 2020-02-03 15:00:00 +0800
categories: [Algorithm, Algorithm_theory]
tags: [algorithm, sorting, quick sort, 알고리즘, 퀵정렬]
---
## 목표
> * 퀵 정렬(quick sort) 알고리즘을 이해하고 코드로 구현할 수 있다.
> * 퀵 정렬(quick sort) 알고리즘의 특징을 설명할 수 있다.
> * 퀵 정렬(quick sort) 알고리즘의 시간복잡도를 계산할 수 있다.

##### 선수지식

* 정렬(sorting)이란?
  - 정렬(sorting): 여러 데이터들이 주어졌을 때 이를 정해진 순서대로 나열하는 것
  - 정렬 알고리즘의 종류 : [버블정렬], [선택정렬], [삽입정렬], [퀵정렬], [병합정렬] 등

* 분할 정복 기법(Divide and Conquer)이란 ?
  - 문제를 나눌 수 없을 때까지 나눈 후 각각을 풀고 다시 합병하여 문제를 해결하는 알고리즘
  - 하향식 접근법으로 상위의 답을 구하기 위해 아래로 내려가면서 해답을 구하는 방식
    + 일반적으로 재귀함수로 구현

[버블정렬]: /posts/sorting-bubblesort
[선택정렬]:/posts/sorting-selectionsort
[삽입정렬]:/posts/sorting-insertionsort
[퀵정렬]:/posts/sorting-quicksort
[병합정렬]:/posts/sorting-mergesort

----------------------------------------------------------------

### 1. 퀵 정렬(quick sort) 이란 ?

* 기준점(pivot)을 정하여 기준점보다 작은 데이터는 왼쪽, 큰 데이터는 오른쪽으로 나눠 정렬하는 알고리즘
  1. 리스트에서 기준점(pivot)을 하나 고른다.(일반적으로 맨처음 or 중간에 있는 데이터를 고름)
  2. 피벗을 기준으로 작은 데이터는 왼쪽에, 큰 데이터는 오른쪽으로 나눔
    - 이 과정이 **분할**
    - 분할을 마친 뒤에 피벗은 더 이상 움직이지 않음
  3. 나눠진 리스트에 대해서 데이터의 길이가 0이나 1이 될 때까지 위 과정(1~2)을 반복

* 특징
  - 분할 정복 기법 중에 하나이다.
  - 불안정 정렬이다.
  - 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬이다.
  - 일반적으로 다른 O(nlogn) 알고리즘에 비해 빠르다(퀵정렬 최악의 경우 제외)
    + 한 번 반복이 끝날 때마다 최소한 하나의 원소의 위치가 정해져 정렬 갯수가 줄어들기 때문

### 2. 퀵 정렬(quick sort) 예제

* 데이터가 [19, 30, 49, 21, 11, 16, 15] 라고 가정하면(오름차순 정렬)
  - step 1
    + pivot : 19
    ![quicksort_step1]({{"/assets/img/algorithm/quicksort_step1.png" | relative_url}})
    + [11, 16, 15] , pivot(19) , [30, 49, 21]
    ![quicksort_step1_result]({{"/assets/img/algorithm/quicksort_step1_result.png" | relative_url}})
  - step 2
    + 첫번째 분할에서 나눠진 왼쪽, 오른쪽 데이터에 대해 각각 분할 반복
    ![quicksort_step2]({{"/assets/img/algorithm/quicksort_step2.png" | relative_url}})
    + 왼쪽 : [], pivot(11), [16, 15]
    ![quicksort_step2_left]({{"/assets/img/algorithm/quicksort_step2_leftresult.png" | relative_url}})
    + 오른쪽 : [21], pivot(30), [49]
    ![quicksort_step2_right]({{"/assets/img/algorithm/quicksort_step2_rightresult.png" | relative_url}})
  - step 3
    + 나눠진 리스트에 대해서 데이터의 길이가 0이나 1이 될 때까지 반복
    + [15], pivot(16), []
    ![quicksort_step3]({{"/assets/img/algorithm/quicksort_step3.png" | relative_url}})
  - 최종결과
    ![quicksort_result]({{"/assets/img/algorithm/quicksort_result.png" | relative_url}})

  - 전체 과정 한번에 보기
   ![quicksort]({{"/assets/img/algorithm/quicksort.png" | relative_url}})

> [참고] 그림으로 이해하기 : <https://visualgo.net/en/sorting>

### 3. 퀵 정렬(quick sort) 코드로 구현하기

* in Python
```python
def quick_sort(data):
    if len(data) <= 1 :
        return data

    left, right = list(), list()
    pivot = data[0]

    for i in range(1, len(data)):
        if pivot > data[i]:
            left.append(data[i])
        else:
            right.append(data[i])

    return quick_sort(left) + [pivot] + quick_sort(right)

  data_list = [19, 30, 49, 21, 11, 16, 15]
  quick_sort(data_list)
  print(data_list)                # 결과 [11, 15, 16, 19, 21, 30, 49]
```

### 4. 퀵 정렬(quick sort) 시간복잡도

* <p>평균적인 경우</p>
  - 다음 그림에서 depth를 i라 가정하면 (0부터 시작)
    + 각 단계의 노드의 갯수(k) : 2^i
    + 각 단계의 노드안에 있는 리스트의 길이 : n / 2^i
    + 따라서, 각 단계별 비교 횟수는 2^i * (n / 2^i) = O(n)
    + 단계가 늘어날 수록 노드의 갯수는 log n개 만큼 만들어짐
    + 퀵 정렬 전체 시간복잡도: O(n) * O(log n) = O(nlog n)

![quicksort_result_complexity]({{"/assets/img/algorithm/binarytree_complexity.png" | relative_url}}){:height="300" width="400"}
  -
* 최악의 경우 O(n^2)
  - 리스트가 불균형하게 나눠지는 경우
    + pivot이 가장 작거나 큰 값일 때
    + 이미 정렬되어 있는 데이터의 경우

------------------------------------------------
## 참고자료
> * <https://fun-coding.org>
> * [퀵정렬-위키백과]

[퀵정렬-위키백과]:https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC
