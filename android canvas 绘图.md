## android canvas 绘图

***1.PathEffect类***
**画虚线**
------------------------

```
 Paint p = new Paint(Paint.ANTI_ALIAS_FLAG);
        p.setStyle(Paint.Style.STROKE);
        p.setColor(Color.WHITE);
        p.setStrokeWidth(1);
        PathEffect effect = new DashPathEffect(new float[]{getDip2px(4), getDip2px(4), getDip2px(4), getDip2px(4)}, 1);
        p.setPathEffect(effect);
        p.setAlpha(125);//透明度50%
        p.setColor(getResources().getColor(R.color.line_chart_dash_line));
        canvas.drawLine(0, ScreenHeight / 2, ScreenWidth, ScreenHeight / 2, p);
        canvas.drawLine(ScreenWidth / 2, 0, ScreenWidth / 2, getBottom() - getDip2px(25), p);
```

***2.android onMeasure***

***3.android BlurMaskFilter***
	
	***Android MaskFilter的基本使用：***

	MaskFilter类可以为Paint分配边缘效果。
	        对MaskFilter的扩展可以对一个Paint边缘的alpha通道应用转换。Android包含了下面几种MaskFilter：
	
	        BlurMaskFilter   指定了一个模糊的样式和半径来处理Paint的边缘。
	        EmbossMaskFilter  指定了光源的方向和环境光强度来添加浮雕效果。
	
	        要应用一个MaskFilter，可以使用setMaskFilter方法，并传递给它一个MaskFilter对象。下面的例子是对一个已经存在的Paint应用一个EmbossMaskFilter：


Android MaskFilter的基本使用：

	MaskFilter类可以为Paint分配边缘效果。
        对MaskFilter的扩展可以对一个Paint边缘的alpha通道应用转换。Android包含了下面几种MaskFilter：

        BlurMaskFilter   指定了一个模糊的样式和半径来处理Paint的边缘。
        EmbossMaskFilter  指定了光源的方向和环境光强度来添加浮雕效果。

        要应用一个MaskFilter，可以使用setMaskFilter方法，并传递给它一个MaskFilter对象。下面的例子是对一个已经存在的Paint应用一个EmbossMaskFilter：
 [关于设置硬件加速不能用的方法](http://blog.csdn.net/hqdoremi/article/details/8307496)
**LAYER_TYPE_NONE**

**LAYER_TYPE_SOFTWARE**

**LAYER_TYPE_HARDWARE**

	View级别
	您可以在运行时用以下的代码关闭单个view的硬件加速：
	
	myView.setLayerType(View.LAYER_TYPE_SOFTWARE, null);
	注：您不能在view级别开启硬件加速
	
	为什么需要这么多级别的控制？
	很明显，硬件加速能够带来性能提升，android为什么要弄出这么多级别的控制，而不是默认就是全部硬件加速呢？原因是并非所有的2D绘图操作支持硬件加速，如果您的程序中使用了自定义视图或者绘图调用，程序可能会工作不正常。如果您的程序中只是用了标准的视图和Drawable，放心大胆的开启硬件加速吧！具体是哪些绘图操作不支持硬件加速呢?以下是已知不支持硬件加速的绘图操作：
	
	Canvas
	clipPath()
	clipRegion()
	drawPicture()
	drawPosText()
	drawTextOnPath()
	drawVertices()
	Paint
	setLinearText()
	setMaskFilter()
	setRasterizer()
	另外还有一些绘图操作，开启和不开启硬件加速，效果不一样：
	
	Canvas
	clipRect()： XOR, Difference和ReverseDifference裁剪模式被忽略，3D变换将不会应用在裁剪的矩形上。
	drawBitmapMesh()：colors数组被忽略
	drawLines()：反锯齿不支持
	setDrawFilter()：可以设置，但无效果
	Paint
	setDither()： 忽略
	setFilterBitmap()：过滤永远开启
	setShadowLayer()：只能用在文本上
	ComposeShader
	ComposeShader只能包含不同类型的shader (比如一个BitmapShader和一个LinearGradient，但不能是两个BitmapShader实例)
	ComposeShader不能包含ComposeShader
	如果应用程序受到这些影响，您可以在受影响的部分调用setLayerType(View.LAYER_TYPE_SOFTWARE, null)，这样在其它地方仍然可以享受硬件加速带来的好处

----------------


 **2.Paint（画笔）类**

	 　　要绘制图形，首先得调整画笔，按照自己的开发需要设置画笔的相关属性。Pain类的常用属性设置方法如下：
	
	　　setAntiAlias();            //设置画笔的锯齿效果
	
	　　setColor();                 //设置画笔的颜色
	
	　　setARGB();                 //设置画笔的A、R、G、B值
	
	　　setAlpha();                 //设置画笔的Alpha值
	
	　　setTextSize();             //设置字体的尺寸
	
	　　setStyle();                  //设置画笔的风格（空心或实心）
	
	　　setStrokeWidth();        //设置空心边框的宽度
	
	　　getColor();                  //获取画笔的颜色
	　　
------------------------
　**3.Canvas（画布）类**

	　　画笔属性设置好之后，还需要将图像绘制到画布上。Canvas类可以用来实现各种图形的绘制工作，如绘制直线、矩形、圆等等。Canvas绘制常用图形的方法如下：
	
	　　绘制直线：canvas.drawLine(float startX, float startY, float stopX, float stopY, Paint paint);
	
	　　绘制矩形：canvas.drawRect(float left, float top, float right, float bottom, Paint paint);
	
	　　绘制圆形：canvas.drawCircle(float cx, float cy, float radius, Paint paint);
	
	　　绘制字符：canvas.drawText(String text, float x, float y, Paint paint);
	
	　　绘制图形：canvas.drawBirmap(Bitmap bitmap, float left, float top, Paint paint);


Shader

渐变色设置

```java
 //设置渐变器后绘制
        //为Paint设置渐变器
        Shader mShasder = new LinearGradient(0, 0, 40, 60, new int[]{Color.RED,Color.GREEN,Color.BLUE,Color.YELLOW}, null, Shader.TileMode.REPEAT);
        mPaint.setShader(mShasder);
        //设置阴影
        mPaint.setShadowLayer(45, 10, 10, Color.GRAY);
```

	Paint.Style.FILL    :填充内部
	Paint.Style.FILL_AND_STROKE  ：填充内部和描边
	Paint.Style.STROKE  ：仅描边

**Region 判断是否在路径范围内**

"onTouchEvent 在自定义View 中"


    @Override  
    public boolean onTouchEvent(MotionEvent event) {  
        switch (event.getAction()) {  
        case MotionEvent.ACTION_DOWN:  
            // 按下  
            cx = (int) event.getX();  
            cy = (int) event.getY();  
            // 通知重绘  
            postInvalidate();   //该方法会调用onDraw方法，重新绘图  
            break;  
        case MotionEvent.ACTION_MOVE:  
            // 移动  
            cx = (int) event.getX();  
            cy = (int) event.getY();  
            // 通知重绘  
            postInvalidate();  
            break;  
        case MotionEvent.ACTION_UP:  
            // 抬起  
            cx = (int) event.getX();  
            cy = (int) event.getY();  
            // 通知重绘  
            postInvalidate();  
            break;  
        }  
          
        /* 
         * 备注1：此处一定要将return super.onTouchEvent(event)修改为return true，原因是： 
         * 1）父类的onTouchEvent(event)方法可能没有做任何处理，但是返回了false。 
         * 2)一旦返回false，在该方法中再也不会收到MotionEvent.ACTION_MOVE及MotionEvent.ACTION_UP事件。 
         */  
        //return super.onTouchEvent(event);  
        return true;    
    }  

---------------------
RectF

	Android Rect和RectF的区别
	1、精度不一样，Rect是使用int类型作为数值，RectF是使用float类型作为数值
	2、两个类型提供的方法也不是完全一致
	
	Rect：
	equals(Object obj)   (for some reason it as it's own implementation of equals)
	exactCenterX()
	exactCenterY()
	flattenToString()
	toShortString()
	unflattenFromString(String str)
	
	RectF：
	round(Rect dst)
	roundOut(Rect dst)
	set(Rect src)


**Shader**
	    

```
//设置渐变器后绘制
        //为Paint设置渐变器
        Shader mShasder = new LinearGradient(0, 0, 40, 60, new int[]{Color.RED,Color.GREEN,Color.BLUE,Color.YELLOW}, null, Shader.TileMode.REPEAT);
        mPaint.setShader(mShasder);
        //设置阴影
        mPaint.setShadowLayer(45, 10, 10, Color.GRAY);
```


```
Paint p=new Paint();
LinearGradient lg=new LinearGradien(0,0,100,100,Color.RED,Color.BLUE,Shader.TileMode.MIRROR);  
```

	参数一为渐变起初点坐标x位置，参数二为y轴位置，参数三和四分辨对应渐变终点，最后参数为平铺方式，这里设置为镜像
	Gradient是基于Shader类，所以我们通过Paint的setShader方法来设置这个渐变，代码如下: mPaint.setShader(lg);
	canvas.drawCicle(0,0,200,mPaint); //参数3为画圆的半径，类型为float型。
	 
	它除了定义开始颜色和结束颜色以外还可以定义，多种颜色组成的分段渐变效果
	LinearGradient shader = new LinearGradient(0, 0, endX, endY, new int[]{startColor, midleColor, endColor},new float[]{0 , 0.5f, 1.0f}, TileMode.MIRROR);
	其中参数new int[]{startColor, midleColor, endColor}是参与渐变效果的颜色集合，
	其中参数new float[]{0 , 0.5f, 1.0f}是定义每个颜色处于的渐变相对位置，
	这个参数可以为null，如果为null表示所有的颜色按顺序均匀的分布


LinearGradient有两个构造函数;
public LinearGradient(float x0, float y0, float x1, float y1, int[] colors, float[] positions,Shader.TileMode tile) 
参数:
float x0: 渐变起始点x坐标
float y0:渐变起始点y坐标
float x1:渐变结束点x坐标
float y1:渐变结束点y坐标
int[] colors:颜色 的int 数组
float[] positions: 相对位置的颜色数组,可为null,  若为null,可为null,颜色沿渐变线均匀分布
Shader.TileMode tile: 渲染器平铺模式

public LinearGradient(float x0, float y0, float x1, float y1, int color0, int color1,Shader.TileMode tile)
float x0: 渐变起始点x坐标
float y0:渐变起始点y坐标
float x1:渐变结束点x坐标
float y1:渐变结束点y坐标
int color0: 起始渐变色
int color1: 结束渐变色
Shader.TileMode tile: 渲染器平铺模式


Android 透明度渐变


**android 代码截屏**

```
 /**
     * Returns the bitmap that represents the chart.
     *
     * @return
     */
    public Bitmap getChartBitmap() {
        // Define a bitmap with the same size as the view
        Bitmap returnedBitmap = Bitmap.createBitmap(getWidth(), getHeight(), Bitmap.Config.RGB_565);
        // Bind a canvas to it
        Canvas canvas = new Canvas(returnedBitmap);
        // Get the view's background
        Drawable bgDrawable = getBackground();
        if (bgDrawable != null)
            // has background drawable, then draw it on the canvas
            bgDrawable.draw(canvas);
        else
            // does not have background drawable, then draw white background on
            // the canvas
            canvas.drawColor(Color.WHITE);
        // draw the view on the canvas
        draw(canvas);
        // return the bitmap
        return returnedBitmap;
    }
```

```
 /**
     * Returns the bitmap that represents the chart.
     *
     * @return
     */
    public Bitmap getChartBitmap() {
        // Define a bitmap with the same size as the view
        Bitmap returnedBitmap = Bitmap.createBitmap(getWidth(), getHeight(), Bitmap.Config.RGB_565);
        // Bind a canvas to it
        Canvas canvas = new Canvas(returnedBitmap);
        // Get the view's background
        Drawable bgDrawable = getBackground();
        if (bgDrawable != null)
            // has background drawable, then draw it on the canvas
            bgDrawable.draw(canvas);
        else
            // does not have background drawable, then draw white background on
            // the canvas
            canvas.drawColor(Color.WHITE);
        // draw the view on the canvas
        draw(canvas);
        // return the bitmap
        return returnedBitmap;
    }
```

*##对canvas的translate()方法的理解*

        

```
canvas.save();//锁画布(为了保存之前的画布状态)
        canvas.translate(10, 10);//把当前画布的原点移到(10,10),后面的操作都以(10,10)作为参照点，默认原点为(0,0)
        drawScene(canvas);
        canvas.restore();//把当前画布返回（调整）到上一个save()状态之前

        canvas.save();//锁画布(为了保存之前的画布状态)
        canvas.translate(160, 10);//把当前画布的原点移到(160,10),后面的操作都以(160,10)作为参照点，
        canvas.clipRect(10, 10, 90, 90);//这里的真实坐标为左上(170,170)、右下(250,250)
        canvas.clipRect(30, 30, 70, 70, Region.Op.DIFFERENCE);
        drawScene(canvas);
        canvas.restore();
```


*图片镜像*

```
public Bitmap convertBmp(Bitmap bmp) {  
        int w = bmp.getWidth();  
        int h = bmp.getHeight();  
  
        Matrix matrix = new Matrix();  
        matrix.postScale(-1, 1); // 镜像水平翻转  
        Bitmap convertBmp = Bitmap.createBitmap(bmp, 0, 0, w, h, matrix, true);  
          
        return convertBmp;  
    }  
```