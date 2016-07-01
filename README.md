# Android Note
>这是我的个人笔记收藏,部分内容可能出自高人博客或链接，如果侵犯，请联系我更正。


## 地址链接
- [个人站点]( www.devcoder.cn)
- [lizhangqu Github 资源链接主页](https://github.com/lizhangqu/CoreLink)
- [Android 开发中的日常积累](https://github.com/AllenCoder/AndroidNote/blob/master/AndroidResourceLink.md)
- [沪深300指数走势图 Android 版](https://github.com/AllenCoder/AndroidDevCoder/tree/master/linechart)
- [Android小知识库](http://wuxiaolong.me/2015/08/10/android-small-knowledge-base/)
- [Android下列表视图的性能优化
](http://boxcounter.com/technique/2015-08-01-Android%E4%B8%8B%E5%88%97%E8%A1%A8%E8%A7%86%E5%9B%BE%E7%9A%84%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96/)

##Android Tips

><font color=red>	1. 如何在屏幕底部显示DialogFragment对话框，并且与屏幕等宽？</font>

	答：这应该就是你想实现的位于底部、与屏幕等宽的DiaglogFragment了。
	（你问题描述里的“适应屏幕”，我理解的是“与屏幕等宽”）
	自定义一个位于屏幕底部、与屏幕等宽的DialogFragment
	

```
public class DatePickerDialog extends DialogFragment {
	  @Override
	  public Dialog onCreateDialog(Bundle savedInstanceState) {
	    // 使用不带theme的构造器，获得的dialog边框距离屏幕仍有几毫米的缝隙。
	    // Dialog dialog = new Dialog(getActivity());
	    Dialog dialog = new Dialog(getActivity(), R.style.CustomDatePickerDialog);
	    dialog.requestWindowFeature(Window.FEATURE_NO_TITLE); // must be called before set content
	    dialog.setContentView(R.layout.dialog_datepicker);
	    dialog.setCanceledOnTouchOutside(true);
	    
	    // 设置宽度为屏宽、靠近屏幕底部。
	    Window window = dialog.getWindow();
	    WindowManager.LayoutParams wlp = window.getAttributes();
	    wlp.gravity = Gravity.BOTTOM;
	    wlp.width = WindowManager.LayoutParams.MATCH_PARENT;
	    window.setAttributes(wlp);
	 
	    return dialog;
	  }
	<!-- res/values/styles.xml -->
	    <style name="CustomDatePickerDialog" parent="@style/AppTheme">
	        <item name="android:layout_width">match_parent</item>
	        <item name="android:layout_height">wrap_content</item>
	        <item name="android:windowIsFloating">true</item>
	    </style>
	    

	
```

><font color=red>2.GreenDao 如何支持模糊查询？</font>
答：	
```
	Query<TestEntity> query = dao.queryBuilder().where(Properties.SimpleString.like("%robot")).build();
	TestEntity entity2 = query.uniqueOrThrow();
	assertEquals(entity.getId(), entity2.getId());
	query.setParameter(0, "green%"); 
	entity2 = query.uniqueOrThrow();
	assertEquals(entity.getId(), entity2.getId()); 
	query.setParameter(0, "%enrob%"); 
	entity2 = query.uniqueOrThrow();
	assertEquals(entity.getId(), entity2.getId());	
```

-[stackflow解释](http://stackoverflow.com/questions/12927859/why-greendao-doesnt-support-like-operator-completely)

><font color=red>3.Android 横屏模式下，怎么使用键盘不被覆盖掉？</font>
-[](http://stackoverflow.com/questions/4336762/disabling-the-fullscreen-editing-view-for-soft-keyboard-input-in-landscape)
```
    

    editText.setImeOptions(EditorInfo.IME_FLAG_NO_EXTRACT_UI);
```
#或者

```
    <?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"         
    >

    <EditText
        android:imeOptions="flagNoExtractUi"
        android:id="@+id/etTextInAct"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10" >   
        <requestFocus />
    </EditText>

</LinearLayout>
```

><font color=red>4.一个 byte 字节数组的大小是-128 ~ 127？</font>

>其原因在于:
	1.byte的大小为8bits而int的大小为32bits
	2.java的二进制采用的是补码形式

	在这里先温习下计算机基础理论

	byte是一个字节保存的，有8个位，即8个0、1。
	8位的第一个位是符号位， 
	也就是说0000 0001代表的是数字1 
	1000 0000代表的就是-1 
	所以正数最大位0111 1111，也就是数字127 
	负数最大为1111 1111，也就是数字-128


><font color=red>5.Android 富文本</font>


```
	//设置字体(加粗斜体)
	textview4 = (TextView) findViewById(R.id.text4);
	SpannableStringBuilder spannableStringBuilder4 = new SpannableStringBuilder("Android");
	StyleSpan styleSpan = new StyleSpan(Typeface.BOLD_ITALIC);
	spannableStringBuilder4.setSpan(styleSpan, 0, 3, Spannable.SPAN_EXCLUSIVE_INCLUSIVE);
	textview4.setText(spannableStringBuilder4);
```
><font color=red>6.DialogFragment 指定位置，指定大小，指定进入退出动画</font>

```
	/* 方法1：
         * 将对话框的大小按屏幕大小的百分比设置
         */
        WindowManager m = getWindowManager();
        Display d = m.getDefaultDisplay(); // 获取屏幕宽、高用
        WindowManager.LayoutParams p = getWindow().getAttributes(); // 获取对话框当前的参数值
         p.height = (int) (d.getHeight() * 0.5); // 高度设置为屏幕的0.5
        p.width = (int) (d.getWidth() * 0.8); // 宽度设置为屏幕的0.8
        dialog.show().getWindow().setAttributes(p);
```

```
	        /*  方法2:
         * 获取对话框的窗口对象及参数对象以修改对话框的布局设置,
         * 可以直接调用getWindow(),表示获得这个Activity的Window
         * 对象,这样这可以以同样的方式改变这个Activity的属性.
         */
        Window dialogWindow = dialog.show().getWindow();
        WindowManager.LayoutParams lp = dialogWindow.getAttributes();
       dialogWindow.setGravity(CENTER_HORIZONTAL | Gravity.CENTER_VERTICAL);
 
        /*
         * lp.x与lp.y表示相对于原始位置的偏移.
         * 当参数值包含Gravity.LEFT时,对话框出现在左边,所以lp.x就表示相对左边的偏移,负值忽略.
         * 当参数值包含Gravity.RIGHT时,对话框出现在右边,所以lp.x就表示相对右边的偏移,负值忽略.
         * 当参数值包含Gravity.TOP时,对话框出现在上边,所以lp.y就表示相对上边的偏移,负值忽略.
         * 当参数值包含Gravity.BOTTOM时,对话框出现在下边,所以lp.y就表示相对下边的偏移,负值忽略.
         * 当参数值包含Gravity.CENTER_HORIZONTAL时
         * ,对话框水平居中,所以lp.x就表示在水平居中的位置移动lp.x像素,正值向右移动,负值向左移动.
         * 当参数值包含Gravity.CENTER_VERTICAL时
         * ,对话框垂直居中,所以lp.y就表示在垂直居中的位置移动lp.y像素,正值向右移动,负值向左移动.
         * gravity的默认值为Gravity.CENTER,即Gravity.CENTER_HORIZONTAL |
         * Gravity.CENTER_VERTICAL.
         * 
         * 本来setGravity的参数值为Gravity.LEFT | Gravity.TOP时对话框应出现在程序的左上角,但在
         * 我手机上测试时发现距左边与上边都有一小段距离,而且垂直坐标把程序标题栏也计算在内了,
         * Gravity.LEFT, Gravity.TOP, Gravity.BOTTOM与Gravity.RIGHT都是如此,据边界有一小段距离
         */
        lp.x = 100; // 新位置X坐标
        lp.y = 100; // 新位置Y坐标
        lp.width = 300; // 宽度
        lp.height = 300; // 高度
        lp.alpha = 0.7f; // 透明度
 
        // 当Window的Attributes改变时系统会调用此函数,可以直接调用以应用上面对窗口参数的更改,也可以用setAttributes
        // dialog.onWindowAttributesChanged(lp);
        dialogWindow.setAttributes(lp);
```

```
    多个点可以连成一个折线,如何将折线的拟合处变为曲线,使得整个线看上去更加平滑呢?

方法1:

Paint.setStrokeJoin(Paint.Join.ROUND)
这个方法可以将path中所有线段的Join方式设置为ROUND,实际效果就是拟合处变成了更加平滑的曲线;
方法2:

CornerPathEffect cornerPathEffect = new CornerPathEffect(200);
Paint.setPathEffect(cornerPathEffect);
此处的200就是平滑的度数;
```