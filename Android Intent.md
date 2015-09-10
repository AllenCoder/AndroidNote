
> 隐式Intent 的action 匹配 只需要一个满足条件即可
> category 必须全部符合条件 必须加上<category android:name="android.intent.category.DEFAULT"></category>
> data 匹配规则类似于action满足一个条件即可。
-------------------------------
每一个通过 startActivity() 方法发出的隐式 Intent 都至少有一个 category，就是 "android.intent.category.DEFAULT"，所以只要是想接收一个隐式 Intent 的 Activity 都应该包括 "android.intent.category.DEFAULT" category，不然将导致 Intent 匹配失败。

<activity
    android:name=".Main3Activity"
    android:launchMode="singleTask"
    android:taskAffinity="com.allen.androidtest.task1"
    android:label="@string/title_activity_main3" >
    <intent-filter>
        <action android:name="com.allen.test"></action>
        <category android:name="android.intent.category.DEFAULT"></category>
        <category android:name="com.category.c"></category>
		</intent-filter>
</activity>

 				Intent intent = new 	Intent("com.allen.test");

                intent.addCategory("com.category.c");

                startActivity(intent);

