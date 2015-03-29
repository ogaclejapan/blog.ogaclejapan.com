---
layout: post
title: Androidライブラリ「ArcLayout」を本日公開しました
tags: [android]
image:  'https://raw.githubusercontent.com/ogaclejapan/ArcLayout/master/art/icon.png'
---

昨年末に公開したQiita非公式クライアント「[Qiitanium](https://github.com/ogaclejapan/Qiitanium)」
のデザイン刷新版v0.2に実装するために夜な夜な作っていたライブラリ第一号「ArcLayout」をようやくリリースしました。

https://github.com/ogaclejapan/ArcLayout

↓こんな感じで弧に沿ってビューを配置することができます
![Arc Layout Demo1](https://raw.githubusercontent.com/ogaclejapan/ArcLayout/master/art/demo1.gif)

応用例としてTumblrやPathみたいなサンプルも用意してます
![Arc Layout Demo2](https://raw.githubusercontent.com/ogaclejapan/ArcLayout/master/art/demo2.gif)


## 使い方

### Step1

build.gradleにライブラリを追加します

```
dependencies {
    compile 'com.ogaclejapan.arclayout:library:1.0.0@aar'
}
```

### Step2

他のレイアウト系クラスと同じくArcLayout内に子ビューを追加するだけです。
原点(arc_origin)を決めると形状が決まり、デフォルトだと子ビューは均等角度で弧に沿って配置されます。

![Attribute Overview](https://raw.githubusercontent.com/ogaclejapan/ArcLayout/master/art/attrs.png)

```xml

<com.ogaclejapan.arclayout.ArcLayout
        android:id="@id/arc_layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:arc_origin="bottom"
        app:arc_color="#4D000000"
        app:arc_radius="168dp"
        app:arc_axisRadius="120dp"
        app:arc_freeAngle="false"
        app:arc_reverseAngle="false"
        >

    <Button
        android:layout_width="48dp"
        android:layout_height="48dp"
        android:gravity="center"
        android:text="A"
        android:textColor="#FFFFFF"
        android:background="#03A9F4"
        app:arc_origin="center"
        />

    <Button
        android:layout_width="48dp"
        android:layout_height="48dp"
        android:gravity="center"
        android:text="B"
        android:textColor="#FFFFFF"
        android:background="#00BCD4"
        app:arc_origin="center"
        />

    <Button
        android:layout_width="48dp"
        android:layout_height="48dp"
        android:gravity="center"
        android:text="C"
        android:textColor="#FFFFFF"
        android:background="#009688"
        app:arc_origin="center"
        />

</com.ogaclejapan.arclayout.ArcLayout>

```

## おわりに

`arc_origin`の全パターンはデモアプリで確認できます。
他に指定できるカスタム属性などはGitHubページを参照ください。

https://github.com/ogaclejapan/ArcLayout

気に入ったらGitHubスターをポチッとお願いします

(　ﾟ∀ﾟ)o彡°Star！Star！
