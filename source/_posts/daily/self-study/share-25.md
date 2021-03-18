---
title: "[자율 공부방] 학습(작업) 내용 공유 - 25"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2021-03-18 22:10:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2021년 03월 18일 목요일
* 내용
    * 교과목 융합스프링프레임워크 강의를 듣고 관련 내용을 정리하며 학습했습니다.

# 융합스프링프레임워크
## 리싸이클러뷰의 이벤트 리스너

* `OnPersonItemClickListener`Interface에서 클릭 이벤트 처리 메소드 정의
* `PersonAdapter` Class에서 Interface 구현
* `PersonAdapter` Class에서 아이템 뷰에 대한 OnClickListener 등록
* `MainActivity`에서 adapter.setOnItemClickListener 등록

## 스피너

스피너는 일반적으로 Windows OS에서 콤보박스로 불린다. Android에서 스피너를 사용하기 위해서는 <Spinner> 태그를 레이아웃에 추가하면 된다.

### 값 할당

```java
Spinner spinner = findViewById(R.id.spinner);
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, android.R.layout.simple_spinner_item, items);

spinner.setAdapter(adapter);
```

### Item 선택 이벤트

```java
spinner.setOnItemClickListener(new AdapterView.OnItemClickListener() {
    @Override
    public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
        textView.setText(items[position]);
    }

    public void onNothingSelected(AdapterView<?> adapterView) {
        textView.setText("");
    }
});
```

## 애니메이션

scale, translate와 같이 다양한 애니메이션/속성 지원

### visibility

* visible: 보임
* invisible: 안보임(자리차지)
* gone: 안보임(자리차지X)

### 애니메이션 실행

```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Animation animation = AnimationUtils.loadAnimation(getApplicationContext(), R.anim.scale);
        v.startAnimation(animation);
    }
});
```

```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        if (isPageOpen) {
            page.startAnimation(translateRightAnim);
        } else {
            page.setVisibility(View.VISIBLE);
            page.startAnimation(translateLeftAnim);
        }
    }
});
```

## 웹브라우저

```java
WebSettings webSettings = webView.getSettings();
webSettings.setJavaScriptEnabled(true);

webView.setWebViewClient(new ViewClient());

Button button = findViewById(R.id.button);
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        webView.loadUrl(editText.getText().toString());
    }
});
```

```java
private class ViewClient extends WebViewClient {
    @Override
    public boolean shouldOverrideUrlLoading(WebView view, final String url) {
        view.loadUrl(url);

        return true;
    }
}
```

## 시커

```java
SeekBar seekBar = findViewById(R.id.seekBar);

seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
    @Override
    public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
        setBrightness(progress);
        textView.setText("변경된 값: " + progress);
    }

    @Override
    public void onStartTrackingTouch(SeekBar seekBar) {

    }

    @Override
    public void onStopTrackingTouch(SeekBar seekBar) {

    }
});
```

## 키패드 제어

...

## 과제
* 도전과제 14(p.441)
