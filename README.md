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

>	1. 如何在屏幕底部显示DialogFragment对话框，并且与屏幕等宽？
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

>2.GreenDao 如何支持模糊查询？
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