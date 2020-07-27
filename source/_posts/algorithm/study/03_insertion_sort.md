---
title: "[알고리즘 학습] 03 - 삽입 정렬(Insertion Sort)"
toc: false
tags: [알고리즘,알고리즘 학습,정렬,Sort,삽입 정렬,Insertion Sort]
categories:
  - Algorithm
  - Study
date: 2020-07-27 04:10:00
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
    int i, j, temp;
    int array[10] = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };
    for (i = 0; i < 9; ++i) {
        j = i;
        while (array[j] > array[j + 1]) {
            temp = array[j];
            array[j] = array[j + 1];
            array[j + 1] = temp;
            --j;
        }
    }

    for (i = 0; i < 10; ++i) {
        printf("%d ", array[i]);
    }

    return 0;
}
```

# 개요
삽입 정렬은 배열을 순회하면서 숫자를 가장 적절한 위치에 삽입하여 정렬을 수행하는 알고리즘입니다.  
`1, 10, 5, 8, 7, 6, 4, 3, 2, 9`를 정렬하다보면 5가 삽입될 수 있는 위치가 `_1_10_` 셋 중 하나입니다. 1 다음 10 이전이 가장 적절한 위치이기 때문에 해당 위치에 삽입하고 더 이상의 탐색은 하지 않습니다.

또한 어느정도 정렬이 되어있는 상태라면 삽입 정렬은 매우 빠른 속도로 정렬을 완료할 수 있다는 특징을 가지고 있습니다.


# 시간 복잡도
길이가 10인 배열을 정렬할 때 삽입 정렬을 사용하는 경우 `10+9+8+...+1=55`번 배열에 접근합니다.
  
이러한 등차수열은 `N*(N+1)/2` 즉, `10*(10+1)/2`로 구하는 방법도 있는데, N이 매우 큰 숫자일 경우 +1과 /2는 의미가 큰 의미가 없기 때문에 일반적으로 `N*N`번 접근한다고 이야기합니다.

이를 Big-O 표기법으로 표기하면 O(N*N) => O(N<sup>2</sup>)이 됩니다.

삽입 정렬은 선택 정렬이나 버블 정렬과 달리 이미 탐색한 원소는 탐색하지 않기 때문에 비교적 속도가 빠르지만 최악의 경우는 동일합니다.  

결론: 삽입 정렬의 시간 복잡도는 <strong>O(N<sup>2</sup>)</strong>이다.