---
title: "[알고리즘 학습] 01 - 선택 정렬(Selection Sort)"
toc: false
tags: [알고리즘,알고리즘 학습,정렬,Sort,선택 정렬,Selection Sort]
categories:
  - Algorithm
  - Study
date: 2020-07-27 02:50:00
thumbnail: /images/post_include/algorithm_study/poster.png
---
> 나동빈님의 [실전 알고리즘 강좌(Algorithm Programming Tutorial)](https://www.youtube.com/playlist?list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz)를 바탕으로 학습한 내용을 정리한 포스트입니다.  
> 실습 코드는 [WebKit's style guide](https://webkit.org/code-style-guidelines/)를 따라 C언어로 작성되었습니다.   
> 개인적으로 학습하며 작성한 포스트이기 때문에 <font color='red'>오류</font>가 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 소스코드
```c
#include <stdio.h>

int main(void)
{
    int i, j, min, index, temp;
    int array[10] = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };
    for (i = 0; i < 10; ++i) {
        min = 9999;
        for (j = i; j < 10; ++j) {
            if (min > array[j]) {
                min = array[j];
                index = j;
            }
        }
        temp = array[i];
        array[i] = array[index];
        array[index] = temp;
    }
    for (i = 0; i < 10; ++i) {
        printf("%d ", array[i]);
    }

    return 0;
}
```

# 개요
선택 정렬은 배열에서 가장 작은 값을 찾아 맨 앞부터 채워나가는 방식의 정렬입니다.  
소스코드에서 `min`은 가장 작은 숫자를 임시로 저장하는 변수이고, `temp`는 배열에서 두 숫자의 위치를 서로 바꾸기 위해 사용하는 변수입니다.

# 시간 복잡도
길이가 10인 배열을 정렬할 때 선택 정렬을 사용하는 `10+9+8+...+1=55`번 배열에 접근합니다.
  
이러한 등차수열은 `N*(N+1)/2` 즉, `10*(10+1)/2`로 구하는 방법도 있는데, N이 매우 큰 숫자일 경우 +1과 /2는 의미가 큰 의미가 없기 때문에 일반적으로 `N*N`번 접근한다고 이야기합니다.

이를 Big-O 표기법으로 표기하면 O(N*N) => O(N<sup>2</sup>)이 됩니다.

결론: 선택 정렬의 시간 복잡도는 **O(N<sup>2</sup>)**이다.