---
title: "[알고리즘 학습] 06 - 병합 정렬(Merge Sort)"
toc: false
tags: [알고리즘,알고리즘 학습,정렬,Sort,병합 정렬,Merge Sort]
categories:
  - Algorithm
  - Study
date: 2020-07-29 00:29:00
thumbnail: /images/post_include/algorithm_study/poster.png
---
> 나동빈님의 [실전 알고리즘 강좌(Algorithm Programming Tutorial)](https://www.youtube.com/playlist?list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz)를 바탕으로 학습한 내용을 정리한 포스트입니다.  
> 실습 코드는 [WebKit's style guide](https://webkit.org/code-style-guidelines/)를 따라 C언어로 작성되었습니다.   
> 개인적으로 학습하며 작성한 포스트이기 때문에 <font color='red'>오류</font>가 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 소스코드
```c
#include <stdio.h>

#define number 8

int sorted[8]; // 정렬 결과가 담길 배열, 불필요한 메모리 사용 이슈를 최소화하기 위해 전역 선언

// m = 시작점, middle = 중간점, n = 끝점
void merge(int* a, int m, int middle, int n)
{
    int i = m;
    int j = middle + 1;
    int k = m;

    // 작은 순서대로 배열에 삽입
    while (i <= middle && j <= n) {
        if (a[i] <= a[j]) {
            sorted[k] = a[i];
            ++i;
        } else {
            sorted[k] = a[j];
            ++j;
        }
        ++k;
    }
    // 남은 데이터를 삽입
    if (i > middle) {
        for (int t = j; t <= n; ++t) {
            sorted[k] = a[t];
            ++k;
        }
    } else {
        for (int t = i; t <= middle; ++t) {
            sorted[k] = a[t];
            ++k;
        }
    }
    // 정렬된 배열을 삽입
    for (int t = m; t <= n; ++t) {
        a[t] = sorted[t];
    }
}

void mergeSort(int* a, int m, int n)
{
    // 크기가 1보다 큰 경우
    if (m < n) {
        int middle = (m + n) / 2;
        mergeSort(a, m, middle);
        mergeSort(a, middle + 1, n);
        merge(a, m, middle, n);
    }
}

int main(void)
{
    int array[number] = { 7, 6, 5, 8, 3, 5, 9, 1 };
    mergeSort(array, 0, number - 1);
    for (int i = 0; i < number; ++i) {
        printf("%d ", array[i]);
    }
    return 0;
}
```

# 개요
이전에 O(N<sup>2</sup>)의 시간 복잡도를 가진 선택 정렬, 버블 정렬, 삽입 정렬과 O(N*logN)의 시간 복잡도를 가진 퀵 정렬에 대해 공부했습니다.

병합 정렬은 퀵 정렬과 동일하게 O(N*logN)의 시간 복잡도를 가지고 있습니다.

위 소스코드에서는 정렬 결과가 담길 배열 sorted를 5번째 줄에 전역 변수로 선언했는데요. 이 배열은 반드시 전역으로 선언해야만합니다.

만약 이 배열을 함수 안에서 선언할 경우 매 함수 호출시 마다 배열을 재선언하기 때문에 메모리 낭비가 극심해질 수 있기 때문입니다.  

# 작동 원리
1. 배열을 절반으로 나눕니다.
2. 나눠진 배열의 왼쪽과 오른쪽을 다시 절반으로 나누며 정렬을 수행합니다.

> 이때, 최소 단위부터 정렬을 수행하기 때문에 왼쪽과 오른쪽 배열의 원소를 순차적으로 탐색하며 작은 수를 병합 결과 배열에 넣는것만으로 정렬이 가능합니다. 
 

# 시간 복잡도
병합 정렬은 퀵 정렬과 동일한 O(N*logN)의 시간 복잡도를 가집니다.

퀵 정렬이 최악의 경우 O(N<sup>2</sup>)의 시간 복잡도를 가지는것에 비해 병합 정렬은 어떤 상황에서도 정확히 절반을 나누며 정렬을 수행하기 때문에 최상, 평균, 최악 모두 O(N*logN)을 보장해준다는 특징이 있습니다.

일반적으로는 퀵정렬보다 느리지만 반드시 O(N*logN)을 보장해주기때문에 훌륭한 알고리즘이라고 평가받습니다.

결론: 병합 정렬의 시간 복잡도는 '항상' <strong>O(N*logN)</strong>이다.

