##Android  shrinkResources true 引发的血案
---------
1. 今天在众测我的App，发现我在代码里面动态调去取之前的图片资源时
一直报 Resources$NotFoundException: Resource ID #0x4 异常
。
但是我在正常debug情况下却没有这个问题

```java
	STEPS TO REPRODUCE:
1. Create a dummy app that uses appcompat (so there are resources to be removed)
2. In build.grade set 'minifyEnabled true' and 'shrinkResource true' 
3. Create the APK where unused resources are removed

EXPECTED RESULTS:
Application should start normally.

OBSERVED RESULTS:
Application crashes with following stacktrace:
android.content.res.Resources$NotFoundException: File res/drawable-xxhdpi-v4/abc_list_pressed_holo_light.9.png from drawable resource ID #0x7f020020
	at android.content.res.Resources$CRunnable_openmp.doOpenMP(Resources.java:1111)
	at android.content.res.Resources$__ompClass0.__doWork(Resources.java:1043)
	at com.samsung.javaomp.runtime.__OMPThread.run(Unknown Source)
Caused by: java.io.FileNotFoundException: res/drawable-xxhdpi-v4/abc_list_pressed_holo_light.9.png
	at android.content.res.AssetManager.openNonAssetNative(Native Method)
	at android.content.res.AssetManager.openNonAsset(AssetManager.java:408)
	at android.content.res.Resources$CRunnable_openmp.doOpenMP(Resources.java:1106)
	... 2 more
java.io.FileNotFoundException: res/drawable-xxhdpi-v4/abc_list_pressed_holo_light.9.png
	at android.content.res.AssetManager.openNonAssetNative(Native Method)
	at android.content.res.AssetManager.openNonAsset(AssetManager.java:408)
	at android.content.res.Resources$CRunnable_openmp.doOpenMP(Resources.java:1106)
	at android.content.res.Resources$__ompClass0.__doWork(Resources.java:1043)
	at com.samsung.javaomp.runtime.__OMPThread.run(Unknown Source)
```

2. 后来我反编译我的apk，找到资源文件夹发现，我需要的图片资源被移除了。我想到我在代码里开启了shrinkResources

-----------------------------
```gradle
	
		 buildTypes {
        release {
            // 不显示Log
            buildConfigField "boolean", "LOG_DEBUG", "false"
            shrinkResources true
            minifyEnabled true
            zipAlignEnabled true
            // 移除无用的resource文件
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'

            applicationVariants.all { variant ->
                variant.outputs.each { output ->
                    def outputFile = output.outputFile
                    if (outputFile != null && outputFile.name.endsWith('.apk')) {
                        // 输出apk名称为boohee_v1.0_2015-01-15_wandoujia.apk
                        def fileName = "${variant.productFlavors[0].name}${defaultConfig.versionName}.apk"
                        output.outputFile = new File(outputFile.parent, fileName)
                    }
                }
            }
        }


```


google 翻墙找了一堆答案：<https://code.google.com/p/android/issues/detail?id=79325>

##写在最后：
* 现在依然无法解决这个问题：因为我的资源需要在服务端返回后动态绑定，现在不需要，我不可能在代码里预定义这个资源引用
* 发现关闭之后，程序打包出来增加了1M多，显然这不是我想要的结果，但面对崩溃，我只能先忍受解决崩溃带来的程序包体积增加。