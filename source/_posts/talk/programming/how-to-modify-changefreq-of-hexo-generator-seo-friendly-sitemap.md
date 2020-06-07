---
title: "Hexo 사이트맵 생성기 갱신주기(change freq), 우선순위(priority) 변경 방법"
toc: false
tags: [Hexo,Hexo 사이트맵,사이트맵,갱신주기,우선순위,change Freq, priority]
categories:
  - Talk
  - Programming
date: 2020-06-07 13:00:00
thumbnail: /images/post_include/how-to-modify-changefreq-of-hexo-generator-seo-friendly-sitemap/hexo_poster.png
---
> 나는 hexo를 이용하여 블로그를 서비스하면서 검색엔진 최적화(SEO)를 위해 사이트맵 생성 도구인 `hexo-generator-seo-friendly-sitemap` 모듈을 사용하고 있다.  
> 새롭게 작성한 게시글은 최대한 빨리 검색엔진에 반영되어 노출되는 것이 중요한데, 포스팅 후 며칠이 지나도록 구글의 크롤링 봇에서 색인을 하지 못하는 현상을 확인하였다.  
> 이 포스팅은 이를 확인하고, 해결한 내용을 다루고 있다.

## 문제 파악
문제가 무엇인지 확인하고자 생성된 sitemap.xml을 우선 확인해보았다.

![문제의 sitemap.xml](/images/post_include/how-to-modify-changefreq-of-hexo-generator-seo-friendly-sitemap/SITEMAP_weekly.JPG "문제의 sitemap.xml")

새롭게 작성한 게시글이 정상적으로 사이트맵에 생성되었있었다.

하지만 Ch.Freq. 즉, Change Frequency(갱신 주기)가 Weekly로 되어 있는 것을 확인할 수 있었다.

Prio의 경우 Priority(우선순위)인데 이는 크롤링 봇이 크롤링을 하는 데 있어 크게 영향을 미치지 않는다고 한다.

이를 바탕으로 문제를 해결해보고자 탐색을 시작했다.

## 문제 해결 과정
구글에 `how to modify change frequency in hexo-generator-seo-friendly-sitemap`, `how to modify change frequency in hexo sitemap` 등의 키워드로 검색을 해보았지만 유사 상황에 대한 Full Request나 Issues만 존재할 뿐 내 상황에 맞는 해결책은 없었다.

이에 node_modules에 적재된 `hexo-geneator-seo-freidny-sitemap` 모듈(이하 본 모듈)의 소스 코드 자체를 분석해보고자 생각했다.

본 모듈을 `--save`를 주어 설치하였을 경우 `node_modules/hexo-geneator-seo-friendly-sitemap` 폴더에 설치되어 있을 것이다. 폴더를 들어가 `lib/post.js` 소스 코드를 분석해보면 단순히 `post-sitemap.ejs` 템플릿을 바탕으로 sitemap.xml을 꾸리는 방식인 것을 확인할 수 있다.

그리고, `post-sitemap.ejs` 파일에는 아래와 같이 기술되어 있다.
```ejs
<changefreq>weekly</changefreq>
<priority>0.6</priority>
```
changefreq가 weekly, priority가 0.6인 것이다. 이를 각각 daily, 0.8로 변경하고 hexo-deploy 명령어를 이용하여 재배포 해보았다.

## 문제의 해결
![문제의 해결 sitemap.xml](/images/post_include/how-to-modify-changefreq-of-hexo-generator-seo-friendly-sitemap/SITEMAP_daily.JPG "문제의 해결 sitemap.xml")
`sitemap.xml`에 수정한 것과 같이 갱신주기가 daily, 우선순위가 0.8(80%)인 것을 확인할 수 있다.

**문제해결 끝!**

## 부가적인 Issue
문제가 완벽히 해결되었으면 좋았겠지만.. 검색엔진 최적화를 연구하고, 이에 대해 Article을 작성하고 있는 SEO SIREN에 따르면 잦은 갱신 요청은 오히려 부작용을 일으킬 수 있다고 한다.

2일에 한 번씩 포스팅한다고 가정해보자.

매일 갱신을 시도할 경우 1주일간 7회 갱신을 시도하며 실제 색인은 3~4건 이루어질 것이다.  
반면 1주일 간격으로 갱신을 시도할 경우 1주일간 1회 갱신을 시도하며 실제 색인은 1회 이루어진다.

여기서 추측해볼 수 있는 점은 갱신을 시도할 때 새로운 데이터에 대한 색인이 성공적으로 이루어지느냐, 만약 그렇다면 새롭게 색인 된 데이터의 질은 얼마나 좋은가? 등이 검색엔진 최적화에 영향을 미친다는 것이다.

7회 갱신을 시도하여 4회는 실패하였고, 3회는 성공하여 3개의 색인을 생성하였다면 갱신 시도당 색인율은 42.85%에 그친다.  
반면 1회 갱신을 시도하여 1회 성공하였고, 3개의 색인을 생성하였다면 갱신 시도당 색인율은 300%이다.

이는 단순 산술에 의한 계산 결과이지만, 충분히 후자가 더 좋은 평가를 받을 것이라고 예상할 수 있다.

참고: [SEO SIREN Articles](https://www.seosiren.com/changing-sitemap-articles-frequency-to-monthly/)

## 결론
만약 하루에 1개 이상의 포스팅을 진행할 자신이 있다면 change frequency를 daily로, 그렇지 않다면 weekly로 하는 것이 좋다고 생각한다.

이제 곧 시험 기간이기도 하고, 학습한 내용을 블로그에 꾸준히 작성하는 것을 목표로 하고 있기에 나는 daily로 유지하여 운영해보고자 한다.~~~~~~~~ 