---
title: "[알고리즘 학습] 07 - C++ STL sort() 파헤치기(1)"
toc: false
tags: [알고리즘,알고리즘 학습,정렬,Sort,C++,Sort,STL]
categories:
  - Algorithm
  - Study
date: 2020-07-29 19:30:00
thumbnail: /images/post_include/algorithm_study/poster.png
---
> 나동빈님의 [실전 알고리즘 강좌(Algorithm Programming Tutorial)](https://www.youtube.com/playlist?list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz)를 바탕으로 학습한 내용을 정리한 포스트입니다.  
> 실습 코드는 [WebKit's style guide](https://webkit.org/code-style-guidelines/)를 따라 C언어로 작성되었습니다.   
> 개인적으로 학습하며 작성한 포스트이기 때문에 <font color='red'>오류</font>가 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
이전까지 선택 정렬, 버블 정렬, 삽입 정렬, 퀵 정렬, 병합 정렬까지 다양한 정렬 알고리즘에 대해 학습을 했었습니다.

하지만 알고리즘 대회나 실무에서 정렬을 하고자 긴 코드를 작성하는것은 매우 비효율적이라고 할 수 있습니다.

C++를 비롯해 대부분의 프로그래밍 언어들은 최적화된 정렬 함수를 제공합니다. 이 포스트에서는 C++의 algorithm 헤더에 있는 sort() 함수에 대해 다룹니다.

# sort() 함수의 기본 사용법
```cpp
#include <algorithm>
#include <iostream>

using namespace std;

int main(void)
{
    int a[10] = { 9, 3, 5, 4, 1, 10, 8, 6, 7, 2 };
    sort(a, a + 10);

    for (int i = 0; i < 10; ++i) {
        cout << a[i] << ' ';
    }

    return 0;
}
```

9번째 라인과 같이 배열의 시작점 주소와 마지막 주소 + 1를 함수의 실인자로 넘겨주면 됩니다. 기본적으로 배열을 오름차순으로 정렬해줍니다.

# sort() 함수의 추가 기능
sort() 함수는 기본적으로 배열을 오름차순으로 정렬합니다. 만약 내림차순으로 정렬하려면 어떻게 해야할까요?

이때 sort() 함수의 세 번째 인자를 사용할 수 있습니다. 세 번째 인자로 배열의 요소를 비교하기 위한 compare() 함수를 작성하여 전달해주면, 해당 함수의 반환 값에 맞게 정렬이 동작합니다.

```cpp
#include <algorithm>
#include <iostream>

using namespace std;

bool compare(int a, int b)
{
    return a > b;
}

int main(void)
{
    int a[10] = { 9, 3, 5, 4, 1, 10, 8, 6, 7, 2 };
    sort(a, a + 10, compare);

    for (int i = 0; i < 10; ++i) {
        cout << a[i] << ' ';
    }

    return 0;
}
```

6~9라인에 compare() 함수가 추가되었고, 14라인의 sort() 함수 호출 시 세 번째 인자로 compare() 함수를 전달해줍니다.

compare() 함수는 내부적으로 a가 b보다 큰 경우 true를 반환합니다. 만약 false를 반환한다면 a와 b를 swap해주어 정렬을 수행하기에 큰 수부터 작은 수까지 정렬할 수 있습니다.

# 데이터를 묶어서 정렬하기
지금까지 배열에 저장된 단순 정수형 데이터를 정렬하는 방법에 대해서 알아봤습니다. 하지만 실무에서 사용되는 데이터는 이름, 주소, 휴대전화번호, 성적 등이 복합적으로 묶여있는 데이터입니다.

아래는 name, score 요소를 가진 객체를 score가 작은 순서부터 오름차순으로 졍렬하는 예시입니다.

```cpp
#include <algorithm>
#include <iostream>

using namespace std;

class Student {
public:
    string name;
    int score;
    Student(string name, int score)
    {
        this->name = name;
        this->score = score;
    }
    // 정렬 기준은 '점수가 작은 순서'
    bool operator<(Student& student)
    {
        return this->score < student.score;
    }
};

int main(void)
{
    Student students[] = {
        Student("진태양", 90),
        Student("나동빈", 93),
        Student("박한울", 97),
        Student("이태일", 87),
        Student("강종구", 92)
    };

    sort(students, students + 5);

    for (int i = 0; i < 5; ++i) {
        cout << students[i].name << ':' << students[i].score << '\n';
    }

    return 0;
}
```

큰(Greater, >) 연산자를 좌항, 우항의 score를 비교하게끔 오버로딩해 score를 기준으로 정렬할 수 있게 합니다.