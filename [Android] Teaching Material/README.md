# ■ Android <kbd>[Kyungpook National University](http://www.knu.ac.kr/wbbs/)</kbd>

* 안드로이드(영어: Android)는 휴대 전화를 비롯한 휴대용 장치를 위한 운영 체제와 미들웨어, 사용자 인터페이스 그리고 표준 응용 프로그램(웹 브라우저, 이메일 클라이언트, 단문 메시지 서비스(SMS), 멀티미디어 메시지 서비스(MMS)등)을 포함하고 있는 소프트웨어 스택이자 모바일 운영 체제이다. 안드로이드는 개발자들이 자바 와 코틀린 언어로 응용 프로그램을 작성할 수 있게 하였으며, 컴파일된 바이트코드를 구동할 수 있는 런타임 라이브러리를 제공한다. 또한 안드로이드 소프트웨어 개발 키트(SDK)를 통해 응용 프로그램을 개발하는 데 필요한 각종 도구와 응용 프로그램 인터페이스(API)를 제공한다.</br></br>안드로이드는 리눅스 커널 위에서 동작하며, 자바와 코틀린으로 앱을 만들어 동작한다. 또한 다양한 안드로이드 시스템 구성 요소에서 사용되는 C/C++ 라이브러리들을 포함하고 있다. 안드로이드는 기존의 자바 가상 머신과는 다른 가상 머신인 안드로이드 런타임을 통해 자바와 코틀린으로 작성된 응용 프로그램을 별도의 프로세스에서 실행하는 구조로 되어 있다.

## 📣 액티비티 생명주기 (Activity Lifecycle)

<p align="center">
  <img src="https://developer.android.com/guide/components/images/activity_lifecycle.png" />
</p>

### 📜 onCreate()

* You must implement this callback, which fires when the system first creates the activity. On activity creation, the activity enters the Created state. In the onCreate() method, you perform basic application startup logic that should happen only once for the entire life of the activity. For example, your implementation of onCreate() might bind data to lists, associate the activity with a ViewModel, and instantiate some class-scope variables. This method receives the parameter savedInstanceState, which is a Bundle object containing the activity's previously saved state. If the activity has never existed before, the value of the Bundle object is null.

##### 📄 onCreate() Syntax

```Kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        /*
            1. Activity가 생성되어 시작될 때, 처음으로 호출되는 Method
            2. Activity의 리소스 초기화, 레이아웃 및 데이터 바인딩 등의 초기 설정 작업 수행
            3. onCreate() 메소드에서는 Bundle 객체를 매개변수로 받아오는데, 새로 시작된 Activity의 경우 null 값이 전달됨.

            * 홈화면에서 종료가 아닌 재진입의 경우 실행되지 않는다.
        */
        Toast.makeText(this, "OnCreate() 함수 호출", Toast.LENGTH_LONG).show()
    }
```

### 📜 onRestart()

* When the activity enters the Resumed state, it comes to the foreground, and then the system invokes the onResume() callback. This is the state in which the app interacts with the user. The app stays in this state until something happens to take focus away from the app. Such an event might be, for instance, receiving a phone call, the user’s navigating to another activity, or the device screen’s turning off.

##### 📄 onRestart() Syntax

```Kotlin
override fun onRestart() {
        super.onRestart()

        /*
            1. Activity가 더 이상 화면에 보이지 않게 되었다가 다시 화면을 보여줘야 할 때 호출되는 메소드이며 onStart()가 호출되기 전에 필요한 작업을 수행
        */
        
        Toast.makeText(this, "onRestart() 함수 호출", Toast.LENGTH_LONG).show()
    }
```

### 📜 onStart()

* When the activity enters the Started state, the system invokes this callback. The onStart() call makes the activity visible to the user, as the app prepares for the activity to enter the foreground and become interactive. For example, this method is where the app initializes the code that maintains the UI. </br></br> When the activity moves to the started state, any lifecycle-aware component tied to the activity's lifecycle will receive the ON_START event. </br></br> The onStart() method completes very quickly and, as with the Created state, the activity does not stay resident in the Started state. Once this callback finishes, the activity enters the Resumed state, and the system invokes the onResume() method.

##### 📄 onStart() Syntax

```Kotlin
override fun onStart() {
        super.onStart()

        /*
            1. Activity가 사용자에게 화면을 보여줄 준비가 되었을 때 호출되는 메소드
            2. 주로 사용자에게 Activity를 보여주기 위해 필요한 리소스들을 설정함.

            * The onStart() call makes the activity visible to the user, as the app prepares for the activity to enter the foreground and become interactive.
            For example, this method is where the app initializes the code that maintains the UI.
        */
        Toast.makeText(this, "onStart() 함수 호출", Toast.LENGTH_LONG).show()
    }
```

### 📜 onResume()

* When the activity enters the Resumed state, it comes to the foreground, and then the system invokes the onResume() callback. This is the state in which the app interacts with the user. The app stays in this state until something happens to take focus away from the app. Such an event might be, for instance, receiving a phone call, the user’s navigating to another activity, or the device screen’s turning off.

##### 📄 onResume() Syntax

```Kotlin
override fun onResume() {
        super.onResume()

        /*
            1. Activity가 Activity Stack의 최상위에 놓여서 사용자에게 화면을 보여주고 사용자의 입력을 처리할 수 있을 때 호출되는 메소드
            2. 오디오나 동영상, 애니메이션 등과 같이 화면 맨 앞에서 실행되고 있을 때만 필요한 리소스들을 설정하기 좋은 메소드
        */
        Toast.makeText(this, "onResume() 함수 호출", Toast.LENGTH_LONG).show()
    }
```

### 📜 onPause()

* The system calls this method as the first indication that the user is leaving your activity (though it does not always mean the activity is being destroyed); it indicates that the activity is no longer in the foreground (though it may still be visible if the user is in multi-window mode). Use the onPause() method to pause or adjust operations that should not continue (or should continue in moderation) while the Activity is in the Paused state, and that you expect to resume shortly.

##### 📄 onPause() Syntax

```Kotlin
override fun onPause() {
        super.onPause()

        /*
            1. Activity가 Background 상태에 진입하여 Activity가 Foreground 상태가 해제 된 경우 호출되는 메서드 (the user is leaving your activity)

            * onResume() <~~~~~~~~> onPause() 사이의 Lifecycle은 Foreground Lifecycle 이다.

            * onResume() 메소드에서 설정했던 리소스들은 반드시 onPause() 메소드에서 해제해야 한다.
            예) onResume() 메소드에서 재생을 시작한 오디오나 동영상, 애니메이션을 중단해야 하고, DB와 같은 리소스들도 해제해야 함.
         */
        Toast.makeText(this, "onPause() 함수 호출", Toast.LENGTH_LONG).show()
    }
```

### 📜 onStop()

* When your activity is no longer visible to the user, it has entered the Stopped state, and the system invokes the onStop() callback. This may occur, for example, when a newly launched activity covers the entire screen. The system may also call onStop() when the activity has finished running, and is about to be terminated. </br></br> When the activity moves to the stopped state, any lifecycle-aware component tied to the activity's lifecycle will receive the ON_STOP event. This is where the lifecycle components can stop any functionality that does not need to run while the component is not visible on the screen.

##### 📄 onStop() Syntax

```Kotlin
override fun onStop() {
        super.onStop()

        /*
            1. 다른 Activity가 Activity Stack의 최상위에 놓이면서, 현재 Activity는 더 이상 화면에 보이질 않게 될 때 호출되는 메소드

            In the onStop() method, the app should release or adjust resources that are not needed while the app is not visible to the user.
            For example, your app might pause animations or switch from fine-grained to coarse-grained location updates.
            Using onStop() instead of onPause() ensures that UI-related work continues, even when the user is viewing your activity in multi-window mode.

            * onStart() <~~~~~~~~> onStop() 사이의 Lifecycle은 Visible Lifecycle 이다.
            * onStart() 메소드에서 설정했던 리소스들(사용자에게 Activity를 보여주기 위해 설정한 리소스들)은 반드시 onStop() 메소드에서 해제해야 한다.
         */
        Toast.makeText(this, "onStop() 함수 호출", Toast.LENGTH_LONG).show()
    }
```

### 📜 onDestroy()

* onDestroy() is called before the activity is destroyed. The system invokes this callback either because: </br></br>ⓐ the activity is finishing (due to the user completely dismissing the activity or due to finish() being called on the activity), or </br></br>ⓑ the system is temporarily destroying the activity due to a configuration change (such as device rotation or multi-window mode) </br></br>When the activity moves to the destroyed state, any lifecycle-aware component tied to the activity's lifecycle will receive the ON_DESTROY event. This is where the lifecycle components can clean up anything it needs to before the Activity is destroyed. </br></br> In the onStop() method, the app should release or adjust resources that are not needed while the app is not visible to the user. For example, your app might pause animations or switch from fine-grained to coarse-grained location updates. Using onStop() instead of onPause() ensures that UI-related work continues, even when the user is viewing your activity in multi-window mode. </br></br> You should also use onStop() to perform relatively CPU-intensive shutdown operations. For example, if you can't find a more opportune time to save information to a database, you might do so during onStop(). The following example shows an implementation of onStop() that saves the contents of a draft note to persistent storage:

##### 📄 onDestroy() Syntax

```Kotlin
override fun onDestroy() {
        super.onDestroy()
        /*
            1. Activity가 파괴되기 전에 호출되는 Method (사용자가 직접 종료하는 경우, 메모리 부족으로 OS가 강제 종료하는 경우)
         */
        Toast.makeText(this, "onDestroy() 함수 호출", Toast.LENGTH_LONG).show()
    }
```

## 📣 [Android API (Application Programming Interface, 응용 프로그램 프로그래밍 인터페이스) Level](https://developer.android.com/guide/topics/manifest/uses-sdk-element.html)

<p align="center">
  <img src="https://user-images.githubusercontent.com/20036523/59984272-3b294580-9663-11e9-8472-490d26e185bd.png" />
</p>

* API 레벨은 Android 플랫폼 버전에서 제공되는 프레임워크 API 수정 버전을 고유하게 식별하는 정수 값입니다.

* Android 플랫폼은 애플리케이션이 기본 Android 시스템과 상호작용하는 데 사용할 수 있는 프레임워크 API를 제공합니다. 프레임워크 API는 다음 요소로 구성되어 있습니다.

  001. 핵심 패키지 및 클래스 집합

  002. 매니페스트 파일을 선언하는 데 사용되는 XML 요소 및 특성 집합

  003. 리소스를 선언 및 액세스하는 데 사용되는 XML 요소 및 특성 집합

  004. 인텐트 집합

  005. 애플리케이션이 요청할 수 있는 권한 및 시스템에 포함된 권한 적용 집합

* `android:minSdkVersion` - 애플리케이션이 실행할 수 있는 최소 API 레벨을 지정합니다. 기본값은 "1"입니다. 또한, 선언하지 않는 경우 시스템은 애플리케이션이 API 레벨 1을 필요로 한다고 가정합니다.

* `android:targetSdkVersion` - 애플리케이션이 실행되는 API 레벨을 지정합니다. 경우에 따라, 최소 API 레벨에 정의된 것만 사용하도록 제한하기보다는 애플리케이션이 대상 API 레벨에서 정의된 매니페스트 요소나 동작을 사용하도록 허용해야 할 수도 있습니다.

* `android:maxSdkVersion` - 애플리케이션이 실행할 수 있는 최대 API 레벨을 지정합니다.

##### 📄 Android API (Application Programming Interface, 응용 프로그램 프로그래밍 인터페이스) Syntax

```XML
<manifest>
  <uses-sdk android:minSdkVersion="5" />
  ...
</manifest>
```

## 📣 [Android NDK (Native Development Kit)](https://developer.android.com/ndk)

* NDK(Native Development Kit)는 Android에서 C 및 C++ 코드를 사용할 수 있게 해주는 일련의 도구 모음으로, 네이티브 액티비티를 관리하고 센서 및 터치 입력과 같은 물리적 기기 구성요소에 액세스하는 데 사용할 수 있는 플랫폼 라이브러리를 제공합니다.

* Android 스튜디오 2.2 이상을 사용하면 C 및 C++ 코드를 네이티브 라이브러리로 컴파일하고 IDE의 내장 빌드 시스템인 Gradle을 사용하여 APK로 패키징할 때 NDK를 이용할 수 있습니다.

* Android 스튜디오에서 네이티브 라이브러리를 컴파일하는 기본 빌드 도구는 CMake입니다.

#### 💡 Android NDK (Native Development Kit) TIP

* JNI는 Java Native Interface의 약어입니다. Android가 Java 또는 Kotlin 프로그래밍 언어로 작성된 관리 코드에서 컴파일하는 바이트코드가 C/C++로 작성된 네이티브 코드와 상호 작용할 수 있는 방법을 정의합니다. JNI는 공급업체 중립적이고, 동적 공유 라이브러리에서 코드를 로드할 수 있도록 지원합니다.

* Java 프로그래밍 언어는 UTF-16을 사용합니다. 편의상, JNI는 Modified UTF-8에서도 작동하는 메서드를 제공합니다.

##### 📄 JNI (Java Native Interface) Data Type

```C++
/* Primitive types that match up with Java equivalents. */
typedef uint8_t  jboolean; /* unsigned 8 bits */
typedef int8_t   jbyte;    /* signed 8 bits */
typedef uint16_t jchar;    /* unsigned 16 bits */
typedef int16_t  jshort;   /* signed 16 bits */
typedef int32_t  jint;     /* signed 32 bits */
typedef int64_t  jlong;    /* signed 64 bits */
typedef float    jfloat;   /* 32-bit IEEE 754 */
typedef double   jdouble;  /* 64-bit IEEE 754 */
```

###### 🔨 [Android NDK (Native Development Kit) Installation](https://developer.android.com/ndk)

|📷 NDK Installation Image 001|📷 NDK Installation Image 002|
|:----------------------------:|:---------------------------:|
|![](https://developer.android.com/studio/images/projects/ndk-install_2-2_2x.png)|![](https://user-images.githubusercontent.com/20036523/59902872-59602d00-943a-11e9-9e36-7e6b4351fb22.png)|

001. 열려 있는 프로젝트의 기본 메뉴에서 Tools > Android > SDK Manager를 선택합니다.

002. SDK Tools 탭을 클릭합니다.

003. 그림에서와 같이 LLDB, CMake, NDK 옆에 있는 체크박스를 선택합니다.

004. Apply를 클릭한 후 다음 대화상자에서 OK를 클릭합니다.

005. 설치가 완료되면 Finish와 OK를 차례로 클릭합니다.

###### 🔨 How To Use Android NDK (Native Development Kit)

001. Java 파일 내에서 표준 System.loadLibrary를 사용하여 공유 라이브러리에서 C++ 코드를 불러옵니다.

##### 📄 Android NDK (Native Development Kit) Source Code 001

```JAVA
    // Used to load the 'Here NDK File Name' library on application startup.
    static {
        System.loadLibrary("Here NDK File Name");
    }
```

002. C++ Native File 내에 정의 된 Method를 사용할 수 있도록 Java 파일 내에 선언합니다. `[Access Modifier] native [Return Type] Method Name (Parameters)`의 형식으로 정의합니다.

<p align="center">
  <img src="https://user-images.githubusercontent.com/20036523/59902873-59602d00-943a-11e9-9f61-fa5dd97c487a.png" />
</p>

##### 📄 Android NDK (Native Development Kit) Source Code 002

```JAVA
      /*
      * A native method that is implemented by the 'Here NDK File Name' native library,
      * which is packaged with this application.
      */
     
    public native String stringFromJNI();
    public native double doubleFromJNI();
    public native int addTargetFromJNI(int left, int right);
```

003. C++ Native File을 열어서 `#include <jni.h>` 선언하고 `extern "C" JNIEXPORT [JNI RETURN TYPE] JNICALL`을 함수 정의 위에 작성합니다. 이후 `Java_[ANDROID_PACKGE_PATH]_[ACTIVITY_NAME]_[METHOD NAME](JNIEnv * env, jobject instance, [OPTIONAL])` 의 형태로 함수를 정의합니다.

<p align="center">
  <img src="https://user-images.githubusercontent.com/20036523/59904104-a42f7400-943d-11e9-83c1-66cfd2104c4e.png" />
</p>

##### 📄 Android NDK (Native Development Kit) Source Code 003

```C++
#include <jni.h>
#include <string>
#include <iostream>

extern "C" JNIEXPORT jstring JNICALL
Java_com_example_myapplication_MainActivity_stringFromJNI(JNIEnv * env, jobject instance) {
    // MARK: JNIEnv*는 VM을 가리키는 포인터이고 jobject는 자바 측으로부터 전달된 암시적 this 객체를 가리키는 포인터입니다.
    std::string hello = "Hello from C++";
    return env->NewStringUTF(hello.c_str());
} extern "C"

JNIEXPORT jdouble JNICALL
Java_com_example_myapplication_MainActivity_doubleFromJNI(JNIEnv *env, jobject instance) {
    return 3.14;
} extern "C"

JNIEXPORT jint JNICALL
Java_com_example_myapplication_MainActivity_addTargetFromJNI(JNIEnv *env,  jobject instance, jint left, jint right) {
    return left + right;
} extern "C";
```

## 📣 [연락처 제공자 (Contact Provider)](https://developer.android.com/guide/topics/providers/contacts-provider?hl=ko)

* The Contacts Provider is a powerful and flexible Android component that manages the device's central repository of data about people. The Contacts Provider is the source of data you see in the device's contacts application, and you can also access its data in your own application and transfer data between the device and online services. The provider accommodates a wide range of data sources and tries to manage as much data as possible for each person, with the result that its organization is complex.

|📷 Contact Provider Image 001|📷 Contact Provider Image 002|
|:----------------------------:|:---------------------------:|
|![](https://developer.android.com/images/providers/ContactsDataFlow.png?hl=ko)|![](https://developer.android.com/images/providers/contacts_structure.png?hl=ko)|

##### 📄 연락처 제공자 (Contact Provider) Manifest Source Code

```JAVA
<uses-permission android:name="android.permission.READ_CONTACTS"/>    // Read Permission
<uses-permission android:name="android.permission.WRITE_CONTACTS"/>   // Write Permission
```

##### 📄 연락처 제공자 (Contact Provider) Source Code

```JAVA
final Cursor cursor = getContentResolver().query(
                ContactsContract.CommonDataKinds.Phone.CONTENT_URI,     // 조회할 컬럼명
                null,
                null,
                null,
                null
);

cursor.moveToFirst();
do {
          final Pair<Integer, Integer> index = Pair.create(
                    cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME),
                    cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.NUMBER)
          );

          System.out.println( String.format("※ TEL -> Name: %s, Phone: %s", cursor.getString(index.first), cursor.getString(index.second)) );
          
} while ( cursor.moveToNext() );
```

## 📣 [Content Provider](https://developer.android.com/guide/topics/providers/content-provider-basics.html#java)

* 서로 다른 앱에서 데이터를 공유하기 위해서 Content Provider 컴포넌트를 이용하는 방법이 있다. Content Provider는 특정 앱에서 사용하는 데이터베이스 데이터를 공유하기 위해 사용하는 컴포넌트로서 서버-클라이언트 구조로 구성되어 있다. 데이터를 제공하는 앱이 서버 앱이 되며 서버에서 Content Provider를 정의한다. 데이터를 공유받는 앱은 클라이언트 앱이 되어 Content Resolver를 통해 서버 앱의 데이터를 사용한다. 특정 Content Provider를 식별하기 위해서는 URI라는 것을 사용한다. URL 뿐만 아니라 Permission을 통해서도 Content Provider에 접근을 제어할 수 있다.

|📷 Content Provider Image 001|📷 Content Provider Image 002|📷 Content Provider Image 003|
|:----------------------------:|:---------------------------:|:----------------------------:|
|![](https://developer.android.com/guide/topics/providers/images/content-provider-tech-stack.png)|![](https://developer.android.com/guide/topics/providers/images/content-provider-interaction.png)|![](https://s3.amazonaws.com/oodles-technologies1/blog-images/2fa348bd-589d-45dd-bb22-1678e09f8738.png)|

* Content providers let you centralize content in one place and have many different applications access it as needed. A content provider behaves very much like a database where you can query it, edit its content, as well as add or delete content using insert(), update(), delete(), and query() methods. In most cases this data is stored in an SQlite database.

<p align="center">
  <img src="https://en.proft.me/media/android/android_content_provider.jpg" />
</p>


## ★ REFERENCE

* [안드로이드 (운영 체제) - 위키백과](https://android-developers.googleblog.com/)

## ★ Developer Information

|:rocket: Github QR Code|:pencil: Naver-Blog QR Code|:eyeglasses: Linked-In QR Code|
|:---------------------:|:-------------------------:|:----------------------------:|
|![](https://user-images.githubusercontent.com/20036523/50044128-60406880-00c2-11e9-8d57-ea1cb8e6b2a7.jpg)|![](https://user-images.githubusercontent.com/20036523/50044131-60d8ff00-00c2-11e9-818c-cf5ad97dc76e.jpg)|![](https://user-images.githubusercontent.com/20036523/50044130-60d8ff00-00c2-11e9-991a-107bffa2bf57.jpg)|
