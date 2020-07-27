---
title: "[알고리즘 학습] 04 - 퀵 정렬(Quick Sort)"
toc: false
tags: [알고리즘,알고리즘 학습,정렬,Sort,퀵 정렬,Quick Sort]
categories:
  - Algorithm
  - Study
date: 2020-07-28 03:35:00
thumbnail: /images/post_include/algorithm_study/poster.png
---
> 나동빈님의 [실전 알고리즘 강좌(Algorithm Programming Tutorial)](https://www.youtube.com/playlist?list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz)를 바탕으로 학습한 내용을 정리한 포스트입니다.  
> 실습 코드는 [WebKit's style guide](https://webkit.org/code-style-guidelines/)를 따라 C언어로 작성되었습니다.   
> 개인적으로 학습하며 작성한 포스트이기 때문에 <font color='red'>오류</font>가 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 소스코드
```C
#include <stdio.h>

static const int number = 10;
int data[10] = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };

void quickSort(int* data, int pos_start, int pos_end)
{
    if (pos_start >= pos_end) { // 정렬 하고자 하는 집단의 원소가 1개인 경우
        return;
    }

    int key = pos_start; // 키는 첫번째 원소
    int i = pos_start + 1;
    int j = pos_end;
    int temp;

    while (i <= j) { // 엇갈릴 때까지 반복
        while (data[i] <= data[key]) { // 키 값보다 큰 값을 만날 때까지 오른쪽으로 이동
            i++;
        }
        while (data[j] >= data[key] && j > pos_start) { // 키 값보다 작은 값을 만날 때까지 왼쪽으로 이동
            j--;
        }
        if (i > j) { // 현재 엇갈린 상태면 키 값과 교체
            temp = data[j];
            data[j] = data[key];
            data[key] = temp;
        } else {
            temp = data[j];
            data[j] = data[i];
            data[i] = temp;
        }

        quickSort(data, pos_start, j - 1);
        quickSort(data, j + 1, pos_end);
    }
}

int main(void)
{
    quickSort(data, 0, number - 1);

    for (int i = 0; i < number; i++) {
        printf("%d ", data[i]);
    }
    return 0;
}
```

# 개요
퀵 정렬은 특정한 값을 기준으로 해당 값보다 큰 숫자와 작은 숫자를 서로 교환하면서 정렬을 수행합니다.
퀵 정렬은 대표적인 분할 정복 알고리즘으로 평균적으로 선택 정렬, 버블 정렬, 삽입 정렬보다 월등히 빠르다는 특징을 가지고 있습니다.
    
위 세가지 정렬이 O(N<sup>2</sup>)인것에 비해 퀵 정렬은 O(N*logN)의 속도를 가지고 있기 때문입니다.



비교의 기준이 되는 특정한 값을 피봇(Pivot)이라고 부르며 보통 가장 앞에 있는 숫자를 Pivot으로 사용합니다.


# 작동 원리
1. 배열을 왼쪽에서 오른쪽으로 순회하면서 Pivot 보다 큰 수를 찾는다
2. 배열을 오른쪽에서 왼쪽으로 순회하면서 Pivot보다 작은 수를 찾는다.
3. 1의 결과와 2의 결과를 서로 Swap한다.
    > 단, 2의 결과가 1의 결과보다 더 왼쪽에 있을 경우 Pivot과 2의 결과(작은 수)를 서로 Swap한다.  
    이때, Pivot의 왼쪽은 Pivot보다 작고, 오른쪽은 Pivot보다 크다. 

# 시간 복잡도
퀵 정렬은 O(N*logN)의 시간 복잡도를 가집니다. 이게 O(N<sup>2</sup>)보다 얼마나 빠른지 감이 잘 안잡히시죠?

N이 1,000,000이라면?(정확한 차이는 아닙니다. 대략적으로 이해만 해주세요.)
* O(N<sup>2</sup>) : 1,000,000 * 1,000,000 = 1,000,000,000,000(1조)
* O(N*logN) : 1,000,000 * 약 20(log<sub>2</sub>1,000,000) = 20,000,000(2천만)

> 둘은 약 50,000배의 속도 차이가 난다.
 
이렇듯 퀵 정렬은 월등히 빠른 속도를 자랑합니다. 그러나 항상 O(N*logN)을 보장해주지는 않습니다.

`1,2,3,4,5,6,7,8,9,10`을 퀵 정렬로 정렬할 경우 `10+9+8+..+1`번 배열에 접근하므로 O(N<sup>2</sup>)의 시간 복잡도를 가집니다  
이를 삽입 정렬로 정렬할 경우 O(N)만에 정렬이 완료되게 됩니다.

이렇듯 '어떠한 방법이 가장 좋다.' 라고 확정지을 순 없으며 정렬하고자하는 대상에 따라 적절한 방법을 선택하는 것이 매우 중요합니다. 

결론: 퀵 정렬의 시간 복잡도는 <strong>O(N*logN)</strong>이다.


# 내림차순으로 퀵 정렬하기
> Pivot의 왼쪽에 Pivot보다 큰 수를, 오른쪽에 Pivot보다 작은 수를 배치하면 된다.  
> 그렇기에 18라인과 21라인의 부등호를 변경하면 내림차순 정렬을 수행할 수 있다.
```c
#include <stdio.h>

static const int number = 10;
int data[10] = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };

void quickSort(int* data, int pos_start, int pos_end)
{
    if (pos_start >= pos_end) { // 정렬 하고자 하는 집단의 원소가 1개인 경우
        return;
    }

    int key = pos_start; // 키는 첫번째 원소
    int i = pos_start + 1;
    int j = pos_end;
    int temp;

    while (i <= j) { // 엇갈릴 때까지 반복
        while (data[i] >= data[key]) { // 키 값보다 작은 값을 만날 때까지 오른쪽으로 이동
            i++;
        }
        while (data[j] <= data[key] && j > pos_start) { // 키 값보다 큰 값을 만날 때까지 왼쪽으로 이동
            j--;
        }
        if (i > j) { // 현재 엇갈린 상태면 키 값과 교체
            temp = data[j];
            data[j] = data[key];
            data[key] = temp;
        } else {
            temp = data[j];
            data[j] = data[i];
            data[i] = temp;
        }

        quickSort(data, pos_start, j - 1);
        quickSort(data, j + 1, pos_end);
    }
}

int main(void)
{
    quickSort(data, 0, number - 1);

    for (int i = 0; i < number; i++) {
        printf("%d ", data[i]);
    }
    return 0;
}
```