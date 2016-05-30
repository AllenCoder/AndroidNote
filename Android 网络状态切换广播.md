#Android网络切换状态广播
```java

	*package com.juyoulicai.forexproduct.Service;
	
	import android.content.BroadcastReceiver;
	import android.content.Context;
	import android.content.Intent;
	import android.net.ConnectivityManager;
	import android.net.NetworkInfo;
	import android.widget.Toast;
	
	import com.juyoulicai.eventbus.ForexDateEvent;
	import com.juyoulicai.util.MLog;
	
	import org.greenrobot.eventbus.EventBus;
	
	/**
	 * 作者: allen on 16/5/30.
	 */
	public class ConnectionChangeReceiver extends BroadcastReceiver {
	    private static  final String TAG =ConnectionChangeReceiver.class.getSimpleName();
	    @Override
	    public void onReceive(Context context, Intent intent) {
	        MLog.d(TAG,"网络状态改变");
	        boolean success =false;
	        /**
	         * 获得网络连接服务
	         */
	        ConnectivityManager connectivityManager = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
	        NetworkInfo.State state =connectivityManager.getNetworkInfo(ConnectivityManager.TYPE_WIFI).getState();
	        if (NetworkInfo.State.CONNECTED==state){
	            success =true;
	        }
	        state =connectivityManager.getNetworkInfo(ConnectivityManager.TYPE_MOBILE).getState();
	        if (NetworkInfo.State.CONNECTED==state){
	            success =true;
	        }
	        if (!success){
	            Toast.makeText(context,"网络连接失败",Toast.LENGTH_LONG).show();
	            EventBus.getDefault().post(new ForexDateEvent(ForexDateEvent.NetworkInfoState,false));
	        } else {
	            EventBus.getDefault().post(new ForexDateEvent(ForexDateEvent.NetworkInfoState,true));
	        }
	    }
	}

```

**记得在Manifest文件里面进行权限声明，和广播接收器注册。**

< !-- Needed to check when the network connection changes -->   

	< uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>   
	< receiver android:name="you_package_name.ConnectionChangeReceiver"   android:label="NetworkConnection">   
	< intent-filter>   
	      < action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>   
	< /intent-filter>   
	< /receiver> 

** 使用方式一：**

1. 在Activity的onCreate中:
//注册网络监听 

		IntentFilter filter = new IntentFilter();  
		filter.addAction(ConnectivityManager.CONNECTIVITY_ACTION); 
		registerReceiver(mNetworkStateReceiver, filter); 
	
2. 在Activity中的onDestroy中:
//取消监听

		unregisterReceiver(mNetworkStateReceiver); 

**使用方式二：**
1. 应用启动时，启动Service，在Service的onCreate方法中注册网络监听：
//注册网络监听 

	IntentFilter filter = new IntentFilter();  
	filter.addAction(ConnectivityManager.CONNECTIVITY_ACTION); 
	registerReceiver(mNetworkStateReceiver, filter); 
2. 应用退出时，Service关闭，在Service的onDestroy方法中取消监听：
//取消监听

		unregisterReceiver(mNetworkStateReceiver); 
