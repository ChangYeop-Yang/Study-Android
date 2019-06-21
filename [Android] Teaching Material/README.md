# ■ Android (operating system) <kbd>[Kyungpook National University](http://www.knu.ac.kr/wbbs/)</kbd>

* 안드로이드(영어: Android)는 휴대 전화를 비롯한 휴대용 장치를 위한 운영 체제와 미들웨어, 사용자 인터페이스 그리고 표준 응용 프로그램(웹 브라우저, 이메일 클라이언트, 단문 메시지 서비스(SMS), 멀티미디어 메시지 서비스(MMS)등)을 포함하고 있는 소프트웨어 스택이자 모바일 운영 체제이다. 안드로이드는 개발자들이 자바 와 코틀린 언어로 응용 프로그램을 작성할 수 있게 하였으며, 컴파일된 바이트코드를 구동할 수 있는 런타임 라이브러리를 제공한다. 또한 안드로이드 소프트웨어 개발 키트(SDK)를 통해 응용 프로그램을 개발하는 데 필요한 각종 도구와 응용 프로그램 인터페이스(API)를 제공한다.</br></br>안드로이드는 리눅스 커널 위에서 동작하며, 자바와 코틀린으로 앱을 만들어 동작한다. 또한 다양한 안드로이드 시스템 구성 요소에서 사용되는 C/C++ 라이브러리들을 포함하고 있다. 안드로이드는 기존의 자바 가상 머신과는 다른 가상 머신인 안드로이드 런타임을 통해 자바와 코틀린으로 작성된 응용 프로그램을 별도의 프로세스에서 실행하는 구조로 되어 있다.

## 📣 액티비티 생명주기 (Activity Lifecycle)

<p align="center">
  <img src="https://developer.android.com/guide/components/images/activity_lifecycle.png" />
</p>

### 📜 onCreate()

* You must implement this callback, which fires when the system first creates the activity. On activity creation, the activity enters the Created state. In the onCreate() method, you perform basic application startup logic that should happen only once for the entire life of the activity. For example, your implementation of onCreate() might bind data to lists, associate the activity with a ViewModel, and instantiate some class-scope variables. This method receives the parameter savedInstanceState, which is a Bundle object containing the activity's previously saved state. If the activity has never existed before, the value of the Bundle object is null.

```JAVA
TextView textView;

// some transient state for the activity instance
String gameState;

@Override
public void onCreate(Bundle savedInstanceState) {
    // call the super class onCreate to complete the creation of activity like
    // the view hierarchy
    super.onCreate(savedInstanceState);

    // recovering the instance state
    if (savedInstanceState != null) {
        gameState = savedInstanceState.getString(GAME_STATE_KEY);
    }

    // set the user interface layout for this activity
    // the layout file is defined in the project res/layout/main_activity.xml file
    setContentView(R.layout.main_activity);

    // initialize member TextView so we can manipulate it later
    textView = (TextView) findViewById(R.id.text_view);
}

// This callback is called only when there is a saved instance that is previously saved by using
// onSaveInstanceState(). We restore some state in onCreate(), while we can optionally restore
// other state here, possibly usable after onStart() has completed.
// The savedInstanceState Bundle is same as the one used in onCreate().
@Override
public void onRestoreInstanceState(Bundle savedInstanceState) {
    textView.setText(savedInstanceState.getString(TEXT_VIEW_KEY));
}

// invoked when the activity may be temporarily destroyed, save the instance state here
@Override
public void onSaveInstanceState(Bundle outState) {
    outState.putString(GAME_STATE_KEY, gameState);
    outState.putString(TEXT_VIEW_KEY, textView.getText());

    // call superclass to save any view hierarchy
    super.onSaveInstanceState(outState);
}
```

### 📜 onStart()

### 📜 onResume()

### 📜 onPause()

### 📜 onStop()

### 📜 onDestroy()

## ★ REFERENCE
* [안드로이드 (운영 체제) - 위키백과](https://android-developers.googleblog.com/)

## ★ Developer Information

|:rocket: Github QR Code|:pencil: Naver-Blog QR Code|:eyeglasses: Linked-In QR Code|
|:---------------------:|:-------------------------:|:----------------------------:|
|![](https://user-images.githubusercontent.com/20036523/50044128-60406880-00c2-11e9-8d57-ea1cb8e6b2a7.jpg)|![](https://user-images.githubusercontent.com/20036523/50044131-60d8ff00-00c2-11e9-818c-cf5ad97dc76e.jpg)|![](https://user-images.githubusercontent.com/20036523/50044130-60d8ff00-00c2-11e9-991a-107bffa2bf57.jpg)|
