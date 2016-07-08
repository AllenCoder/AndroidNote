# Android 屏幕方向改变全屏和 actionBar 变化处理


> 配置屏幕变化，不重新实例化生命周期
```
	 android:configChanges="keyboardHidden|orientation|screenSize"
```
> 重写配置改变的事件监听
```
@Override 
    public void onConfigurationChanged(Configuration newConfig) { 
        super.onConfigurationChanged(newConfig); 
 
       if (newConfig.orientation == Configuration.ORIENTATION_LANDSCAPE) { 
		    getActionBar().hide();
		    getWindow().addFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN);
		} else if (newConfig.orientation == Configuration.ORIENTATION_PORTRAIT) { 
		    getActionBar().show();
		    getWindow().clearFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN);
		} 
    } 

```
