---
layout: post
title: "Parcelableを自動生成する"
date: 2014-01-13 12:28:21 +0900
comments: true
categories: android androidstudio
---

ParcelableはSerializableより制約が少なくていいんですが自分で直列化処理を書かないといけないのでだるいです。

Android Studioで利用できるプラグイン「[Android Parcelable code generator](https://github.com/mcharmas/android-parcelable-intellij-plugin)」を使えば簡単にParcelableを自動生成できます。

<!-- more -->

## インストール

Android Studioを起動して、[Preference]-[Plugins]を開き、`Browse repositories…`を押下してください。

![01](/images/2014-01-08-android-selector-chapek/01.png)

Browse Repositoriesで`parcelable code gen`で絞り込むとpluginが見つかるので、ダブルクリックしてインストールしてください。

![02](/images/2014-01-13-parcel-generator/01.png)


## 対象クラスを作る

Parcelableにしたいクラスを作っていきます。よくあるUserクラスとかにしておきます。

```java
package com.example.app;

public class User {

  private int mId;

  private String mName;

  public User(int id, String name){
    mId = id;
    mName = name;
  }

}
```

## Parcelableを生成する

エディタの中で右クリックするとコンテキストメニューに「Generate...」があるので選択します。

![03](/images/2014-01-13-parcel-generator/02.png)

Generateの項目のうち「Generate Parcelable」を選択します。

![04](/images/2014-01-13-parcel-generator/03.png)

Parcelableで保存する対象となるフィールドを選択します。基本的に全部選択しておけばよいでしょう。

![05](/images/2014-01-13-parcel-generator/04.png)

するとParcelableの実装が生成されます。

```java
package com.example.app;

import android.os.Parcel;
import android.os.Parcelable;

public class User implements Parcelable {

    private int mId;

    private String mName;

    public User(int id, String name){
        mId = id;
        mName = name;
    }

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeInt(this.mId);
        dest.writeString(this.mName);
    }

    private User(Parcel in) {
        this.mId = in.readInt();
        this.mName = in.readString();
    }

    public static Parcelable.Creator<User> CREATOR = new Parcelable.Creator<User>() {
        public User createFromParcel(Parcel source) {
            return new User(source);
        }

        public User[] newArray(int size) {
            return new User[size];
        }
    };
}
```

## おわりに

楽ちん！