##Android比例布局

1.使用方法：
	在app目录下的build.gradle中 添加以下引用 库
	
```

 compile 'com.android.support:percent:22.2.0'
 
```

2.新建xml文件


```
<android.support.percent.PercentRelativeLayout

    xmlns:android="http://schemas.android.com/apk/res/android"

    xmlns:app="http://schemas.android.com/apk/res-auto"

    android:layout_width="match_parent"

    android:layout_height="match_parent">


    <View

        android:id="@+id/top_left"

        android:layout_width="0dp"

        android:layout_height="0dp"

        android:layout_alignParentTop="true"

        android:background="#ff0000"

        app:layout_heightPercent="30%"
        app:layout_widthPercent="70%"/>


    <View

        android:id="@+id/top_right"

        android:layout_width="0dp"

        android:layout_height="0dp"

        android:layout_alignParentTop="true"

        android:layout_toRightOf="@+id/top_left"

        android:background="#00ff00"

        app:layout_heightPercent="30%"

        app:layout_widthPercent="30%"/>


    <View

        android:id="@+id/centre"

        android:layout_width="match_parent"

        android:layout_height="0dp"

        android:layout_below="@+id/top_left"

        android:background="#0000ff"

        app:layout_heightPercent="40%"

        app:layout_marginBottomPercent="10%"

        app:layout_marginLeftPercent="10%"

        app:layout_marginRightPercent="20%"

        app:layout_marginTopPercent="10%"/>


    <View

        android:id="@+id/bottom"

        android:layout_width="match_parent"

        android:layout_height="0dp"

        android:layout_alignParentLeft="true"

        android:layout_alignParentStart="true"

        android:layout_below="@+id/centre"

        android:background="#00f0ff"

        app:layout_heightPercent="10%"/>


</android.support.percent.PercentRelativeLayout>

```

