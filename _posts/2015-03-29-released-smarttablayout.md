---
layout: post
title: Androidライブラリ「SmartTabLayout」を本日公開しました
tags: [android]
image:  'https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/icon.png'
---

昨年末に公開したQiita非公式クライアント「[Qiitanium](https://github.com/ogaclejapan/Qiitanium)」
のデザイン刷新版v0.2に実装するために夜な夜な作っていたライブラリ第二号「SmartTabLayout」をようやくリリースしました。

<https://github.com/ogaclejapan/SmartTabLayout>

Google SamplesとしてGitHubに公開されているの
「[android-SlidingTabBasic](https://github.com/googlesamples/android-SlidingTabsBasic)」
をベースにViewPagerStrip系で一番有名な「PagerSlidingTabStrip」と同等の機能を実装した感じです。

独自な機能として、Indicatorの挙動を多少カスタマイズできます。デフォルトでは２種類組み込んでます。

Indicatorが伸びてから縮みます  
(`stl_indicatorInterpolation="smart"`)
![SmartTabLayout Demo1](https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo1.gif)

こちらは一般的な通常の動き  
(`stl_indicatorInterpolation="linear"`)
![SmartTabLayout Demo1](https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo3.gif)

Indicatorを極端に太くして透過色をMixするとこんな動きもできます  
(…使いどころは未知数)
![SmartTabLayout Demo3](https://raw.githubusercontent.com/ogaclejapan/SmartTabLayout/master/art/demo4.gif)


## 使い方

### Step1

build.gradleにライブラリを追加します

```

dependencies {
    compile 'com.ogaclejapan.smarttablayout:library:1.0.0@aar'

    //Optional
    compile 'com.ogaclejapan.smarttablayout:utils-v4:1.0.0@aar'

    //Optional
    compile 'com.ogaclejapan.smarttablayout:utils-v13:1.0.0@aar'
}

```

※OptionalではViewPagerを使う上で必ず実装が必要になる[PagerAdapter](http://developer.android.com/reference/android/support/v4/view/PagerAdapter.html)の実装クラスを別ライブラリとして提供しています。
経験的には大体同じような実装コードをみんな書いてる気がするので、特に理由がなければ一緒に使うことをオススメします。

### Step2

レイアウト定義は他で公開されているTabStrip系と同じです。
ViewPagerの上に配置して使うのが一般的ですね。

```xml

<com.ogaclejapan.smarttablayout.SmartTabLayout
    android:id="@+id/viewpagertab"
    android:layout_width="match_parent"
    android:layout_height="48dp"
    app:stl_indicatorAlwaysInCenter="false"
    app:stl_indicatorInFront="false"
    app:stl_indicatorInterpolation="smart"
    app:stl_indicatorColor="#40C4FF"
    app:stl_indicatorThickness="4dp"
    app:stl_indicatorCornerRadius="2dp"
    app:stl_underlineColor="#4D000000"
    app:stl_underlineThickness="1dp"
    app:stl_dividerColor="#4D000000"
    app:stl_dividerThickness="1dp"
    app:stl_defaultTabTextAllCaps="true"
    app:stl_defaultTabTextColor="#FC000000"
    app:stl_defaultTabTextSize="12sp"
    app:stl_defaultTabTextHorizontalPadding="16dp"
    app:stl_defaultTabTextMinWidth="0dp"
    app:stl_distributeEvenly="false"
    />

<android.support.v4.view.ViewPager
    android:id="@+id/viewpager"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_below="@id/viewpagertab"
    />

```

### Step3

onCreateなどのView初期化あたりでAdapterにタイトルとページ（この例だとFragment）のセットを追加していきます。
次にViewPagerにAdapterをセットした上でSmartTabLayoutにViewPagerをセットします。

```java

//↓これ、オプションライブラリとして公開しているPagerAdapterの実装クラス
FragmentPagerItemAdapter adapter = new FragmentPagerItemAdapter(
        getSupportFragmentManager(), FragmentPagerItems.with(this)
        .add(R.string.titleA, PageFragment.class)
        .add(R.string.titleB, PageFragment.class)
        .create());

ViewPager viewPager = (ViewPager) findViewById(R.id.viewpager);
viewPager.setAdapter(adapter);

SmartTabLayout viewPagerTab = (SmartTabLayout) findViewById(R.id.viewpagertab);
viewPagerTab.setViewPager(viewPager);

```

#### 補足

`PagerSlidingTabStrip`も同じですが、
`OnPageChangeListener`を使う場合は必ずSmartTabLayoutにListenerをセットする必要があります。
ViewPagerに直接Listenerをセットするとライブラリが正しくイベントを検知できなくなりますのでご注意ください。

```java

viewPagerTab.setOnPageChangeListener(mPageChangeListener);

```

あとオプションライブラリを使った場合に特典が２つあります

Fragment系のPagerAdapterのみページFragment側で自分のpositionが取得できます。
Marketアプリでも実装されているViewPagerのヘッダーParallaxですが、
このpositionがあると実装するときに幸せになれたりします。
(Qiitaniumのコードでもこのpositionは使っています)

```java

int position = FragmentPagerItem.getPosition(getArguments());

```

ページが生成されて破棄されてるまではAdapterからposition指定でページを取得できます。

```java

public void onPageSelected(int position) {

  Fragment page = adapter.getPage(position);

}

```

## おわりに

均等配置やIndicatorの真ん中表示など、
PagerSlidingTabStripと同等の機能は実装したつもりです。

指定できるカスタム属性の詳細はGitHubページを参照ください。

<https://github.com/ogaclejapan/SmartTabLayout>

気に入ったらGitHubスターをポチッとお願いします

(　ﾟ∀ﾟ)o彡°Star！Star！
