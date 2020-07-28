---
title: "[알고리즘 학습] 05 - 기본 정렬 알고리즘 문제풀이"
toc: false
tags: [알고리즘,알고리즘 학습,정렬,Sort,알고리즘,문제풀이]
categories:
  - Algorithm
  - Study
date: 2020-07-28 03:35:00
thumbnail: /images/post_include/algorithm_study/poster.png
---
> 나동빈님의 [실전 알고리즘 강좌(Algorithm Programming Tutorial)](https://www.youtube.com/playlist?list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz)를 바탕으로 학습한 내용을 정리한 포스트입니다.  
> 실습 코드는 [WebKit's style guide](https://webkit.org/code-style-guidelines/)를 따라 C언어로 작성되었습니다.   
> 개인적으로 학습하며 작성한 포스트이기 때문에 <font color='red'>오류</font>가 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 백준 2752
링크: [백준 2752 - 세수정렬](https://www.acmicpc.net/problem/2752)
```c
#include <stdio.h>

int array[3];

int main(void)
{
    int i, j, min, index, temp;

    for (i = 0; i < 3; ++i) {
        scanf("%d", &array[i]);
    }

    for (i = 0; i < 3; ++i) {
        min = 1000001;
        for (j = i; j < 3; ++j) {
            if (array[j] < min) {
                min = array[j];
                index = j;
            }
        }
        temp = array[i];
        array[i] = array[index];
        array[index] = temp;
    }

    for (i = 0; i < 3; ++i)
        printf("%d ", array[i]);

    return 0;
}
```

# 백준 2750
링크: [백준 2750 - 수 정렬하기](https://www.acmicpc.net/problem/2750)
```c
#include <stdio.h>

int array[1001];

int main(void)
{
    int number, i, j, min, index, temp;
    scanf("%d", &number);

    for (i = 0; i < number; ++i) {
        scanf("%d", &array[i]);
    }

    for (i = 0; i < number; ++i) {
        min = 1001;
        for (j = i; j < number; ++j) {
            if (array[j] < min) {
                min = array[j];
                index = j;
            }
        }
        temp = array[i];
        array[i] = array[index];
        array[index] = temp;
    }

    for (i = 0; i < number; ++i)
        printf("%d ", array[i]);

    return 0;
}
```

# 백준 2751
링크: [백준 2751 - 수 정렬하기2](https://www.acmicpc.net/problem/2751)
```c
#include <stdio.h>

int array[1000001];

void quickSort(int* data, int pos_start, int pos_end)
{
    int mLeft = pos_start, mRight = pos_end;
    int pivot = data[(pos_start + pos_end) / 2];
    int temp;

    while (mLeft <= mRight) {
        while (pivot > data[mLeft])
            mLeft++;
        while (pivot < data[mRight])
            mRight--;

        if (mLeft <= mRight) {
            temp = data[mLeft];
            data[mLeft] = data[mRight];
            data[mRight] = temp;
            mLeft++, mRight--;
        }
    }

    if (pos_start < mRight)
        quickSort(data, pos_start, mRight);
    if (mLeft < pos_end)
        quickSort(data, mLeft, pos_end);
}

int main(void)
{
    int number, i;

    scanf("%d", &number);

    for (i = 0; i < number; ++i) {
        scanf("%d", &array[i]);
    }

    quickSort(array, 0, number - 1);

    for (i = 0; i < number; ++i)
        printf("%d\n", array[i]);

    return 0;
}
```