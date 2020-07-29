---
title: "[알고리즘 학습] 08 - C++ STL sort() 파헤치기(2)"
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
이전에는 클래스(Class)를 정의해서 여러 개의 변수가 존재하는 상황에서 **'특정한 변수'**를 기준으로 정렬하는 방법에 대해 다뤘습니다. 하지만 실제 대회에서 문제 하나를 풀기 위해 클래스를 정의하는 것은 효율적이지 못합니다.

쉽게 말해 클래스를 이용하는 방식은 실무에 적합한 방식이며, 일반적으로 프로그래밍 대회와 같이 빠른 개발이 필요할 때는 페어(Pair) 라이브러리를 사용하는 것이 더 효율적입니다.

# STL vector
```cpp
#include <algorithm>
#include <iostream>
#include <vector>

using namespace std;

int main(void)
{
    vector<pair<int, string>> v;
    v.push_back(pair<int, string>(90, "진태양"));
    v.push_back(pair<int, string>(85, "이태일"));
    v.push_back(pair<int, string>(82, "나동빈"));
    v.push_back(pair<int, string>(98, "강종구"));
    v.push_back(pair<int, string>(79, "이상욱"));

    sort(v.begin(), v.end());
    for (int i = 0; i < v.size(); ++i) {
        cout << v[i].second << ':' << v[i].first << '\n';
    }

    return 0;
}
```
벡터(Vector) 라이브러리와 페어(Pair) 라이브러리를 이용해 지난 시간에 배열과 클래스를 이용했던 방식을 대체하였습니다.

벡터(Vector) STL은 배열과 같이 작동하는데 원소를 선택적으로 삽입(Push) 및 삭제(Pop) 할 수 있습니다. 즉, 단순한 배열을 보다 사용하기 쉽게 개편한 자료구조라고 할 수 있습니다.

페어(Pair) STL은 한 쌍의 데이터를 처리할 수 있도록 해주는 자료구조입니다.

# 정렬 기준이 2개일 경우
앞서 Pair의 First 요소에 대해 정렬하는 소스코드를 작성해보았습니다.

이때, First 요소(점수)가 동일한 경우가 발생할 수 있습니다. 그럴 경우 생년월일을 비교하여 나이가 더 어린 학생이 더 우선순위가 높게끔 정렬해보겠습니다.

Pair안에 Pair를 포함해 3개의 요소를 갖는 형태로 구조를 설계하였으며 compare() 함수에서 기준이되는 요소를 비교합니다. 

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

using namespace std;

bool compare(pair<string, pair<int, int>> a, pair<string, pair<int, int>> b)
{
    if (a.second.first == b.second.first) {
        return a.second.second > b.second.second;
    } else {
        return a.second.first > b.second.first;
    }
}

int main(void)
{
    vector<pair<string, pair<int, int>>> v;
    v.push_back(pair<string, pair<int, int>>("진태양", pair<int, int>(90, 19960813)));
    v.push_back(pair<string, pair<int, int>>("이태일", pair<int, int>(97, 19930518)));
    v.push_back(pair<string, pair<int, int>>("박한울", pair<int, int>(95, 19930203)));
    v.push_back(pair<string, pair<int, int>>("이상욱", pair<int, int>(90, 19921207)));
    v.push_back(pair<string, pair<int, int>>("강종구", pair<int, int>(88, 19900302)));

    sort(v.begin(), v.end(), compare);
    for (int i = 0; i < v.size(); ++i) {
        cout << v[i].first << '(' << v[i].second.second << ") : " << v[i].second.first << '\n';
    }

    return 0;
}
```