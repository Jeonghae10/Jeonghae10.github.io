---
title: "[알고리즘]정렬알고리즘 05. 합병정렬(merge sort)"
date: 2020-02-05 11:30:00 +0800
categories: [Algorithm, Algorithm_theory]
tags: [algorithm, sorting, merge sort, 알고리즘, 합병정렬]
---
## 목표
> * 합병 정렬(merge sort) 알고리즘을 이해하고 코드로 구현할 수 있다.
> * 합병 정렬(merge sort) 알고리즘의 특징을 설명할 수 있다.
> * 합병 정렬(merge sort) 알고리즘의 시간복잡도를 계산할 수 있다.

##### 선수지식

* 정렬(sorting)이란?
  - 정렬(sorting): 여러 데이터들이 주어졌을 때 이를 정해진 순서대로 나열하는 것
  - 정렬 알고리즘의 종류 : [버블정렬], [선택정렬], [삽입정렬], [퀵정렬], [합병정렬] 등   

* 분할 정복 기법(Divide and Conquer)이란 ?
  - 문제를 나눌 수 없을 때까지 나눈 후 각각을 풀고 다시 합병하여 문제를 해결하는 알고리즘
  - 하향식 접근법으로 상위의 답을 구하기 위해 아래로 내려가면서 해답을 구하는 방식
    + 일반적으로 재귀함수로 구현

[버블정렬]: /posts/sorting-bubblesort
[선택정렬]:/posts/sorting-selectionsort
[삽입정렬]:/posts/sorting-insertionsort
[퀵정렬]:/posts/sorting-quicksort
[합병정렬]:/posts/sorting-mergesort
----------------------------------

### 1. 합병 정렬(merge sort) 이란 ?
* 리스트의 길이가 1이하가 될 때까지 나눈 후 합병하며 정렬하는 알고리즘
  1. 리스트의 길이가 1이하면 정렬된 것으로 간주
  2. 분할(divide) : 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다
  3. 정복(conquer) : 각 부분 리스트를 재귀적으로 합병 정렬을 이용하여 정렬한다
  4. 결합(combine) : 두 두분 리스트를 다시 하나의 정렬된 리스트로  **합병** 한다.

* 특징
  - 분할 정복 기법 중 하나이다.
  - 안정 정렬이다.
  - 비교 기반 정렬 알고리즘이다.
  - 어떤 자료구조를 쓰느냐에 따라 별로의 저장공간이 필요할 수 있다.
    + 배열로 구현시 임시 저장공간 필요
    + 링크드 리스트로 구현시 연결된 링크랑 변경해주면 되므로 별도 저장공간이 필요없음(in-place sort)

![](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif)

> 출처: <https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif>

### 2. 합병 정렬(merge sort) 예제

* 데이터가 [19, 30, 49, 21, 98, 54, 29, 70] 이라 가정하면(오름차순 정렬)
  - split 단계 : 데이터의 길이가 1이하가 될 때까지 두 개의 리스트로 나눔
  ![mergesort_split]({{"/assets/img/algorithm/mergesort/mergesort_split.png" | relative_url}}){:height="300" width="600"}

  - merge 단계 : 나눠진 리스트들을 정렬하며 합병
    + 나눠진 두 개의 리스트의 값들을 하나씩 비교해서 어느 한쪽의 데이터가 없을 때까지 반복하며 새로운 리스트에 저장
      + ex) [19, 21, 30, 49] & [29, 54, 70, 98]
        + step 1 : 19 vs 29 -> [19]
        + step 2 : 21 vs 29 -> [19, 21]
        + step 3 : 30 vs 29 -> [19, 21, 29]
        + step 4 : 30 vs 54 -> [19, 21, 29, 30]
        + step 5 : 49 vs 54 -> [19, 21, 29, 30, 49]
        + step 6: 왼쪽 리스트에 더 이상 비교할 것이 없으므로 오른쪽 리스트에 남아있는 데이터들 전부 새로운 리스트에 옮겨줌 [19, 21, 29, 30, 49, 54, 70, 98]

  ![mergesort_merge]({{"/assets/img/algorithm/mergesort/mergesort_merge.png" | relative_url}}){:height="300" width="600"}

> [참고] 그림으로 이해하기 : <https://visualgo.net/en/sorting>

### 3. 합병 정렬(merge sort) 코드로 구현하기

* in Python
```python
def merge(left, right):
    merged = list()                             # 합쳐진 리스트를 담을 임시 저장 공간
    leftPoint, rightPoint = 0, 0                # 현재 비교 데이터 위치

    # left, right 둘다 데이터가 있을때
    while len(left) > leftPoint and len(right) > rightPoint:
        if left[leftPoint] > right[rightPoint] :
            merged.append(right[rightPoint])
            rightPoint += 1
        else:
            merged.append(left[leftPoint])
            leftPoint += 1

    # left에만 데이터가 있을 때
    while len(left) > leftPoint:
        merged.append(left[leftPoint])
        leftPoint += 1

    # right에만 데이터가 있을 때
    while len(right) > rightPoint:
        merged.append(right[rightPoint])
        rightPoint += 1

    return merged

  # 리스트를 둘로 나눔
  def merge_split(data):
      if len(data) <= 1:
          return data
      middle = len(data) // 2

      # 리스트의 길이가 1이하가 될 때까지 재귀용법으로 반복
      left = merge_split(data[:middle])
      right = merge_split(data[middle:])
      return merge(left, right)

  def mergesort(data):
    return merge_split(data)

  data_list = [19, 30, 49, 21, 98, 54, 29, 70]
  data_list = mergesort(data_list)
  print(data_list)                  # 결과 [19, 21, 29, 30, 49, 54, 70, 98]
```

### 4. 합병 정렬(merge sort) 시간복잡도

* 퀵 정렬과 유사
* O(nlog n) = O(nlog n) + O(2nlog n)
  - 비교횟수 : n번씩 log n 만큼 비교 = O(nlog n)
  - 데이터 이동횟수 O(2nlog n)
    + 임시 리스트에 저장 후 재 복사 : 2n번
    + log n 번 반복
* 링크드 리스트 사용 시 데이터 이동이 없으므로 더 빠르게 동작

------------------------------------------------
## 참고자료
> * <https://fun-coding.org>
> * [합병정렬-위키백과]


[합병정렬-위키백과]:https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC
