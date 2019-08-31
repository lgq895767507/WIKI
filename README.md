
#### 算法：
* 排序，查找，红黑树 
* https://lgq895767507.github.io

#### 设计模式：

##### 面向对象6大原则：
* 单一原则：就一个类而言，，应该仅有一个引起他变化的原因。
* 开闭原则：对于扩展是开放的，对于修改是封闭的
* 里氏替换原则：所有引用基类的地方必须透明的使用其子类的对象。
* 依赖倒置原则：调用端不依赖于实现端，而应该依赖其抽象，细节应该依赖于抽象。
* 接口隔离原则：类的依赖应该建立在最小接口之上。
* 迪米特原则：最少知识原则。一个类对另外一个类了解的越少越好，则耦合度就越小。

* 单例

```java

//双重校验锁:第一层是主要判断为了避免不必要的同步，第二层的判断是为了在null的情况下创建实例。使用最多方式，也值得推荐


//静态内部类：推荐方式

//源码ServiceFetcher是通过容器hashMap的方式来创建单例的

```

* Builder
  * 将一个复杂的对象的构建与表示分离
  * 源码AlertDialog

* 工厂模式
  * onCreate相当于就是一个工厂方法

* 策略模式
  * 算法独立于他的客户而独立的变化，相互可替换
  * 属性动画插值器

* 状态模式
  * 当一个对象的内在状态改变时允许改变其行为，这个对象看起来像是改变了其类。
  * wifi管理

* 责任链模式
  * 使得多个对象都有机会处理请求，从而避免请求的发送者和接收者之间的耦合关系。将这些对象连成一条链，并沿着这条链传递改请求，直到有对象处理它为止。
  * view的事件分发

* 观察者模式
  * 定义对象间一种一对多的依赖关系，使得每当一个对象改变状态，则所有依赖的对象都会得到通知并自动更新。
  * listview adapter

* 代理模式
  * 为其他对象提供一种代理以控制对这个对象的访问。
  * 动态代理：反射生成代理对象
  * 静态代理：内部生成代理类
  * activityManagerProxy 

* 适配器模式
  * 使原本因接口不匹配而无法工作的两个类能够在一起工作。

* 装饰模式
  * 动态的给一个对象添加一些额外的职责
  * contextWrapper

* 桥接模式
  * 将抽象与实现部分分离，使他们都可以独立的进行变化。

* Paint画笔高级应用
  * paint的api

```java

        mPaint = new Paint(); //初始化
        mPaint.setColor(Color.RED);// 设置颜色
        mPaint.setARGB(255, 255, 255, 0); // 设置 Paint对象颜色,范围为0~255
        mPaint.setAlpha(200); // 设置alpha不透明度,范围为0~255
        mPaint.setAntiAlias(true); // 抗锯齿
        mPaint.setStyle(Paint.Style.FILL); //描边效果
        mPaint.setStrokeWidth(4);//描边宽度
        mPaint.setStrokeCap(Paint.Cap.ROUND); //圆角效果
        mPaint.setStrokeJoin(Paint.Join.MITER);//拐角风格
        mPaint.setShader(new SweepGradient(200, 200, Color.BLUE, Color.RED)); //设置环形渲染器
        mPaint.setXfermode(new PorterDuffXfermode(PorterDuff.Mode.DARKEN)); //设置图层混合模式
        mPaint.setColorFilter(new LightingColorFilter(0x00ffff, 0x000000)); //设置颜色过滤器
        mPaint.setFilterBitmap(true); //设置双线性过滤
        mPaint.setMaskFilter(new BlurMaskFilter(10, BlurMaskFilter.Blur.NORMAL));//设置画笔遮罩滤镜 ,传入度数和样式
        mPaint.setTextScaleX(2);// 设置文本缩放倍数
        mPaint.setTextSize(38);// 设置字体大小
        mPaint.setTextAlign(Paint.Align.LEFT);//对其方式
        mPaint.setUnderlineText(true);// 设置下划线

        String str = "Android高级工程师";
        Rect rect = new Rect();
        mPaint.getTextBounds(str, 0, str.length(), rect); //测量文本大小，将文本大小信息存放在rect中
        mPaint.measureText(str); //获取文本的宽
        mPaint.getFontMetrics(); //获取字体度量对象


```

* 渲染器shader

```java

   
//         * 1.线性渲染,LinearGradient(float x0, float y0, float x1, float y1, @NonNull @ColorInt int colors[], @Nullable float positions[], @NonNull TileMode tile)
//         * (x0,y0)：渐变起始点坐标
//         * (x1,y1):渐变结束点坐标
//         * color0:渐变开始点颜色,16进制的颜色表示，必须要带有透明度
//         * color1:渐变结束颜色
//         * colors:渐变数组
//         * positions:位置数组，position的取值范围[0,1],作用是指定某个位置的颜色值，如果传null，渐变就线性变化。
//         * tile:用于指定控件区域大于指定的渐变区域时，空白区域的颜色填充方法
//         */
//        mShader = new LinearGradient(0, 0, 500, 500, new int[]{Color.RED, Color.BLUE, Color.GREEN}, new float[]{0.f,0.7f,1}, Shader.TileMode.REPEAT);
//        mPaint.setShader(mShader);
////        canvas.drawCircle(250, 250, 250, mPaint);
//        canvas.drawRect(0,0,1000,1000, mPaint);

//        //        /**
////         * 环形渲染，RadialGradient(float centerX, float centerY, float radius, @ColorInt int colors[], @Nullable float stops[], TileMode tileMode)
////         * centerX ,centerY：shader的中心坐标，开始渐变的坐标
////         * radius:渐变的半径
////         * centerColor,edgeColor:中心点渐变颜色，边界的渐变颜色
////         * colors:渐变颜色数组
////         * stoops:渐变位置数组，类似扫描渐变的positions数组，取值[0,1],中心点为0，半径到达位置为1.0f
////         * tileMode:shader未覆盖以外的填充模式。
////         */
//        mShader = new RadialGradient(250, 250, 250, new int[]{Color.GREEN, Color.YELLOW, Color.RED}, null, Shader.TileMode.CLAMP);
//        mPaint.setShader(mShader);
//        canvas.drawCircle(250, 250, 250, mPaint);


//        //        /**
////         * 扫描渲染，SweepGradient(float cx, float cy, @ColorInt int color0,int color1)
////         * cx,cy 渐变中心坐标
////         * color0,color1：渐变开始结束颜色
////         * colors，positions：类似LinearGradient,用于多颜色渐变,positions为null时，根据颜色线性渐变
////         */
//        mShader = new SweepGradient(250, 250, Color.RED, Color.GREEN);
//        mPaint.setShader(mShader);
//        canvas.drawCircle(250, 250, 250, mPaint);

////        //        /**
//////         * 位图渲染，BitmapShader(@NonNull Bitmap bitmap, @NonNull TileMode tileX, @NonNull TileMode tileY)
//////         * Bitmap:构造shader使用的bitmap
//////         * tileX：X轴方向的TileMode
//////         * tileY:Y轴方向的TileMode
////               REPEAT, 绘制区域超过渲染区域的部分，重复排版
////               CLAMP， 绘制区域超过渲染区域的部分，会以最后一个像素拉伸排版
////               MIRROR, 绘制区域超过渲染区域的部分，镜像翻转排版
//////         */
//        mShader = new BitmapShader(mBitmap, Shader.TileMode.REPEAT, Shader.TileMode.MIRROR);
//        mPaint.setShader(mShader);
//        canvas.drawRect(0,0,500, 500, mPaint);
////        canvas.drawCircle(250, 250, 250, mPaint);


        /**
         * 组合渲染，
         * ComposeShader(@NonNull Shader shaderA, @NonNull Shader shaderB, Xfermode mode)
         * ComposeShader(@NonNull Shader shaderA, @NonNull Shader shaderB, PorterDuff.Mode mode)
         * shaderA,shaderB:要混合的两种shader
         * Xfermode mode： 组合两种shader颜色的模式
         * PorterDuff.Mode mode: 组合两种shader颜色的模式
         */
        BitmapShader bitmapShader = new BitmapShader(mBitmap, Shader.TileMode.REPEAT, Shader.TileMode.REPEAT);
        LinearGradient linearGradient = new LinearGradient(0, 0, 1000, 1600, new int[]{Color.RED, Color.GREEN, Color.BLUE}, null, Shader.TileMode.CLAMP);
        mShader = new ComposeShader(bitmapShader, linearGradient, PorterDuff.Mode.MULTIPLY);
        mPaint.setShader(mShader);
        canvas.drawCircle(250, 250, 250, mPaint);


  ```

* 图层混合模式

```java

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);

        //1.ComposeShader
        //2.画笔Paint.setXfermode()
        //3.PorterDuffColorFilter

        //禁止硬件加速
        setLayerType(View.LAYER_TYPE_SOFTWARE, null);

        setBackgroundColor(Color.GRAY);

//        //离屏绘制
//        int layerId = canvas.saveLayer(0,0, getWidth(), getHeight(), mPaint, Canvas.ALL_SAVE_FLAG);

//        //目标图
        canvas.drawBitmap(createRectBitmap(mWidth, mHeight), 0, 0, mPaint);
//        //设置混合模式
        mPaint.setXfermode(new PorterDuffXfermode(PorterDuff.Mode.DST_IN));
//        //源图，重叠区域右下角部分
        canvas.drawBitmap(createCircleBitmap(mWidth, mHeight), 0, 0, mPaint);
//        //清除混合模式
        mPaint.setXfermode(null);
//
//        canvas.restoreToCount(layerId);

    }


```

* Canvas离屏缓冲
  * 离屏缓冲：通过离屏缓冲，把想要绘制的内容单独绘制在缓冲层，保证Xfremode的使用不会出错错误的结果。

```java

        //使用离屏绘制，可以做短时的离屏缓冲，在绘制之前保存，绘制之后恢复
        int layerID = canvas.saveLayer(0, 0, getWidth(), getHeight(), mPaint, Canvas.ALL_SAVE_FLAG);

        //先将路径绘制到 bitmap上
        Canvas dstCanvas = new Canvas(mDstBmp);
        dstCanvas.drawPath(mPath, mPaint);

        //绘制 目标图像
        canvas.drawBitmap(mDstBmp, 0, 0, mPaint);
        //设置 模式 为 SRC_OUT, 擦橡皮区域为交集区域需要清掉像素
        mPaint.setXfermode(new PorterDuffXfermode(PorterDuff.Mode.SRC_OUT));
        //绘制源图像
        canvas.drawBitmap(mSrcBmp, 0, 0, mPaint);

        mPaint.setXfermode(null); //用完及时清除Xfremode

        canvas.restoreToCount(layerID);


```

* ColorFilter滤镜效果

```java

    /**
         * R' = R * mul.R / 0xff + add.R
         * G' = G * mul.G / 0xff + add.G
         * B' = B * mul.B / 0xff + add.B
         */
        //红色去除掉
//        LightingColorFilter lighting = new LightingColorFilter(0x00ffff,0x000000);
//        mPaint.setColorFilter(lighting);
//        canvas.drawBitmap(mBitmap, 0,0, mPaint);

//        //原始图片效果
//        LightingColorFilter lighting = new LightingColorFilter(0xffffff,0x000000);
//        mPaint.setColorFilter(lighting);
//        canvas.drawBitmap(mBitmap, 0,0, mPaint);

//        //绿色更亮
//        LightingColorFilter lighting = new LightingColorFilter(0xffffff,0x003000);
//        mPaint.setColorFilter(lighting);
//        canvas.drawBitmap(mBitmap, 0,0, mPaint);

//        PorterDuffColorFilter porterDuffColorFilter = new PorterDuffColorFilter(Color.RED, PorterDuff.Mode.DARKEN);
//        mPaint.setColorFilter(porterDuffColorFilter);
//        canvas.drawBitmap(mBitmap, 100, 0, mPaint);

        float[] colorMatrix = {
                2,0,0,0,0,   //red
                0,1,0,0,0,   //green
                0,0,1,0,0,   //blue
                0,0,0,1,0    //alpha
        };

        ColorMatrix cm = new ColorMatrix();
//        //亮度调节
//        cm.setScale(1,2,1,1); //红r绿g蓝b前三个分量

//        //饱和度调节0-无色彩， 1- 默认效果， >1饱和度加强
//        cm.setSaturation(2);

        //色调调节
        cm.setRotate(0, 45);

        mColorMatrixColorFilter = new ColorMatrixColorFilter(cm);
        mPaint.setColorFilter(mColorMatrixColorFilter);
        canvas.drawBitmap(mBitmap, 100, 0, mPaint);



```

* canvas

```java

/        //1，平移操作
//        canvas.drawRect(0,0, 400, 400, mPaint);
//        canvas.translate(50, 50);
//        mPaint.setColor(Color.GRAY);
//        canvas.drawRect(0,0, 400, 400, mPaint);
//        canvas.drawLine(0, 0, 600,600, mPaint);

//        //缩放操纵
//        canvas.drawRect(200,200, 700,700, mPaint);
////        canvas.scale(0.5f, 0.5f);
//        //先translate(px, py),再scale(sx, sy),再反响translate
//        //canvas.scale(0.5f, 0.5f, 200,200);
//
//        canvas.translate(200, 200);
//        canvas.scale(0.5f, 0.5f);
//        canvas.translate(-200, -200);
//
//        mPaint.setColor(Color.GRAY);
//        canvas.drawRect(200,200, 700,700, mPaint);
//        canvas.drawLine(0,0, 400, 600, mPaint);

//        //旋转操作
//        canvas.translate(50,50);
//        canvas.drawRect(0,0, 700,700, mPaint);
//        canvas.rotate(45);
//        mPaint.setColor(Color.GRAY);
//        canvas.drawRect(0,0, 700,700, mPaint);

//        canvas.drawRect(400, 400, 900, 900, mPaint);
//        canvas.rotate(45, 650, 650); //px, py表示旋转中心的坐标
//        mPaint.setColor(Color.GRAY);
//        canvas.drawRect(400, 400, 900, 900, mPaint);

//        //倾斜操作
//        canvas.drawRect(0,0, 400, 400, mPaint);
////        canvas.skew(1, 0); //在X方向倾斜45度,Y轴逆时针旋转45
//        canvas.skew(0, 1); //在y方向倾斜45度， X轴顺时针旋转45
//        mPaint.setColor(Color.GRAY);
//        canvas.drawRect(0, 0, 400, 400, mPaint);

        //切割
//        canvas.drawRect(200, 200,700, 700, mPaint);
//        mPaint.setColor(Color.GRAY);
//        canvas.drawRect(200, 800,700, 1300, mPaint);
//        canvas.clipRect(200, 200,700, 700); //画布被裁剪
//        canvas.drawCircle(100,100, 100,mPaint); //坐标超出裁剪区域，无法绘制
//        canvas.drawCircle(300, 300, 100, mPaint); //坐标区域在裁剪范围内，绘制成功

//        canvas.drawRect(200, 200,700, 700, mPaint);
//        mPaint.setColor(Color.GRAY);
//        canvas.drawRect(200, 800,700, 1300, mPaint);
//        canvas.clipOutRect(200,200,700,700); //画布裁剪外的区域
//        canvas.drawCircle(100,100,100,mPaint); //坐标区域在裁剪范围内，绘制成功
//        canvas.drawCircle(300, 300, 100, mPaint);//坐标超出裁剪区域，无法绘制

        //矩阵
        canvas.drawRect(0,0,700,700, mPaint);
        Matrix matrix = new Matrix();
//        matrix.setTranslate(50,50);
//        matrix.setRotate(45);
        matrix.setScale(0.5f, 0.5f);
        canvas.setMatrix(matrix);
        mPaint.setColor(Color.GRAY);
        canvas.drawRect(0,0,700,700, mPaint);


          /**
         * 1.canvas内部对于状态的保存存放在栈中
         * 2.可以多次调用save保存canvas的状态，并且可以通过getSaveCount方法获取保存的状态个数
         * 3.可以通过restore方法返回最近一次save前的状态，也可以通过restoreToCount返回指定save状态。指定save状态之后的状态全部被清除
         * 4.saveLayer可以创建新的图层，之后的绘制都会在这个图层之上绘制，直到调用restore方法
         * 注意：绘制的坐标系不能超过图层的范围， saveLayerAlpha对图层增加了透明度信息
         */



```

* 贝塞尔曲线

```java

////        mPaint.setStyle(Paint.Style.FILL);
        //一阶贝塞尔曲线，表示的是一条直线
        mPath.moveTo(100, 70); //移动
//        mPath.lineTo(140, 800);//连线
        //等同于上一行代码效果
        mPath.rLineTo(40, 730);
//        mPath.lineTo(250, 600);
////        mPath.close();//设置曲线是否闭合

//        //添加子图形addXXX
//        //添加弧形
//        mPath.addArc(200, 200, 400, 400, -225, 225);
////
////        //Path.Direction.CW表示顺时针方向绘制，CCW表示逆时针方向
////        mPath.addRect(500, 500, 900, 900, Path.Direction.CW);
////        //添加一个圆
////        mPath.addCircle(700,700, 200, Path.Direction.CW);
////        //添加一个椭圆
////        mPath.addOval(0,0,500,300, Path.Direction.CCW);
//
//                //追加图形
//        //xxxTo画线
//        mPath.arcTo(400, 200, 600, 400, -180, 225, false);
////
//        //forceMoveTo，true，绘制时移动起点，false，绘制时连接最后一个点与圆弧起点
//        mPath.moveTo(0, 0);
//        mPath.lineTo(100, 100);
//        mPath.arcTo(400, 200, 600, 400, 0, 270, false);

//                //添加一个路径
//        mPath.moveTo(100, 70);
//        mPath.lineTo(140, 180);
//        mPath.lineTo(250, 330);
//        mPath.lineTo(400, 630);
//        mPath.lineTo(100, 830);
//
//        Path newPath = new Path();
//        newPath.moveTo(100, 1000);
//        newPath.lineTo(600, 1300);
//        newPath.lineTo(400, 1700);
//        mPath.addPath(newPath);

//                //添加圆角矩形， CW顺时针，CCW逆时针
//        RectF rectF5 = new RectF(200, 800, 700, 1200);
//        mPath.addRoundRect(rectF5, 20, 20, Path.Direction.CCW);

                //画二阶贝塞尔曲线
        mPath.moveTo(300, 500);
//        mPath.quadTo(500, 100, 800, 500);
        //参数表示相对位置，等同于上面一行代码
        mPath.rQuadTo(200, -400, 500, 0);
//
//
        //画三阶贝塞尔曲线
        mPath.moveTo(300, 500);
//        mPath.cubicTo(500, 100, 600, 1200, 800, 500);
        //参数表示相对位置，等同于上面一行代码
        mPath.rCubicTo(200, -400, 300, 700, 500, 0);


        canvas.drawPath(mPath, mPaint);

//贝塞尔曲线一阶公式：p(t) = p0 + (p1-p0)t = (1-t)p0 + p1*t


```

* PathMeasure: 路径测量，一个用来测量path的工具类

```java

canvas.drawLine(0, getHeight() / 2, getWidth(), getHeight() / 2, mLinePaint);
        canvas.drawLine(getWidth() / 2, 0, getWidth() / 2, getHeight(), mLinePaint);

        canvas.translate(getWidth() / 2, getHeight() / 2);

//        Path path = new Path();
//        path.lineTo(0,200);
//        path.lineTo(200,200);
//        path.lineTo(200,0);
//
//        /**
//         * pathMeasure需要关联一个创建好的path, forceClosed会影响Path的测量结果
//         */
//        PathMeasure pathMeasure = new PathMeasure();
//        pathMeasure.setPath(path, true);
//        Log.e("TAG", "onDraw:forceClosed=true "+ pathMeasure.getLength());
//
//        PathMeasure pathMeasure2 = new PathMeasure();
//        pathMeasure2.setPath(path, false);
//        Log.e("TAG", "onDraw:forceClosed=false "+ pathMeasure2.getLength());
//
//        PathMeasure pathMeasure1 = new PathMeasure(path, false);
//        Log.e("TAG", "onDraw:PathMeasure(path, false) "+ pathMeasure1.getLength());
//
//        path.lineTo(200, -200);
//
//        Log.e("TAG", "onDraw:PathMeasure(path, false) "+ pathMeasure1.getLength());
//        //如果Path进行了调整，需要重新调用setPath方法进行关联
//        pathMeasure1.setPath(path, false);
//
//        Log.e("TAG", "onDraw:PathMeasure(path, false) "+ pathMeasure1.getLength());

//        Path path = new Path();
//        path.addRect(-200,-200, 200,200, Path.Direction.CW);
//
//        Path dst = new Path();
//        dst.lineTo(-300,-300);//添加一条直线
//
//        PathMeasure pathMeasure = new PathMeasure(path, false);
//        //截取一部分存入dst中，并且使用moveTo保持截取得到的Path第一个点位置不变。
//        pathMeasure.getSegment(200, 1000, dst, true);
//
//
//
//        canvas.drawPath(path, mPaint);
//        canvas.drawPath(dst, mLinePaint);

//        Path path = new Path();
//        path.addRect(-100,-100,100,100, Path.Direction.CW);//添加一个矩形
//        path.addOval(-200,-200,200,200, Path.Direction.CW);//添加一个椭圆
//        canvas.drawPath(path, mPaint);
//        PathMeasure pathMeasure = new PathMeasure(path, false);
//        Log.e("TAG", "onDraw:forceClosed=false "+ pathMeasure.getLength());
//        //跳转到下一条曲线
//        pathMeasure.nextContour();
//        Log.e("TAG", "onDraw:forceClosed=false "+ pathMeasure.getLength());

        mPath.reset();
        mPath.addCircle(0,0,200, Path.Direction.CW);
        canvas.drawPath(mPath, mPaint);

        mFloat += 0.01;
        if (mFloat >= 1){
            mFloat = 0;
        }

//        PathMeasure pathMeasure = new PathMeasure(mPath, false);
/**
  * getPosTan
  * 这个API用于获取路径上某点的坐标及其切线的坐标，这个API非常强大，但是比较难理解，后面 会结合例子来讲解。简单的说，就是通过指定distance（0<distance<getLength），来获取坐标点和切线的坐标，并保存到pos[]和tan[]数组中。
*/
//        pathMeasure.getPosTan(pathMeasure.getLength() * mFloat,pos,tan);
//        Log.e("TAG", "onDraw: pos[0]="+pos[0]+";pos[1]="+pos[1]);
//        Log.e("TAG", "onDraw: tan[0]="+tan[0]+";tan[1]="+tan[1]);
//
//        //计算出当前的切线与x轴夹角的度数
//        double degrees = Math.atan2(tan[1], tan[0]) * 180.0 / Math.PI;
//        Log.e("TAG", "onDraw: degrees="+degrees);
//
//        mMatrix.reset();
//        //进行角度旋转
//        mMatrix.postRotate((float) degrees, mBitmap.getWidth() / 2, mBitmap.getHeight() / 2);
//        //将图片的绘制点中心与当前点重合
//        mMatrix.postTranslate(pos[0] - mBitmap.getWidth() / 2, pos[1]-mBitmap.getHeight() / 2);
//        canvas.drawBitmap(mBitmap,mMatrix, mPaint);

        PathMeasure pathMeasure = new PathMeasure(mPath, false);
        //将pos信息和tan信息保存在mMatrix中
        pathMeasure.getMatrix(pathMeasure.getLength() * mFloat, mMatrix, PathMeasure.POSITION_MATRIX_FLAG | PathMeasure.TANGENT_MATRIX_FLAG);
        //将图片的旋转坐标调整到图片中心位置
        mMatrix.preTranslate(-mBitmap.getWidth() / 2, -mBitmap.getHeight() / 2);

        canvas.drawBitmap(mBitmap,mMatrix, mPaint);

        invalidate();


```



* 事件分发机制
  * viewGroup事件分发，可以用以下伪代码表示：

```java

public boolean dispatchTouchEvent(MotionEvent ev){
    boolean consume = false;
    //调用onInterceptTouchEvent判断是否拦截
    if(onInterceptTouchEvent(ev)){
        //拦截则调用自身的onTouchEvent
        consume = onTouchEvent(ev);
    }else{
        //不拦截，将事件分发给子view
        consume = child.dispatchTouchEvent(ev);
    }
    return consume;
}

```


* 自定义像素适配

```java

public class Utils {

    private static Utils utils;

    //这里是设计稿参考宽高
    private static final float STANDARD_WIDTH = 1080;
    private static final float STANDARD_HEIGHT = 1920;

    //这里是屏幕显示宽高
    private int mDisplayWidth;
    private int mDisplayHeight;

    private Utils(Context context){
        //获取屏幕的宽高
        if(mDisplayWidth == 0 || mDisplayHeight == 0){
            WindowManager manager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
            if (manager != null){
                DisplayMetrics displayMetrics = new DisplayMetrics();
                manager.getDefaultDisplay().getMetrics(displayMetrics);
                if (displayMetrics.widthPixels > displayMetrics.heightPixels){
                    //横屏
                    mDisplayWidth = displayMetrics.heightPixels;
                    mDisplayHeight = displayMetrics.widthPixels;
                }else{
                    mDisplayWidth = displayMetrics.widthPixels;
                    mDisplayHeight = displayMetrics.heightPixels - getStatusBarHeight(context);
                }
            }
        }

    }

    public int getStatusBarHeight(Context context){
        int resID = context.getResources().getIdentifier("status_bar_height", "dimen", "android");
        if (resID > 0){
            return context.getResources().getDimensionPixelSize(resID);
        }
        return 0;
    }

    public static Utils getInstance(Context context){
        if (utils == null){
            utils = new Utils(context.getApplicationContext());
        }
        return utils;
    }

    //获取水平方向的缩放比例
    public float getHorizontalScale(){
        return mDisplayWidth / STANDARD_WIDTH;
    }

    //获取垂直方向的缩放比例
    public float getVerticalScale(){
        return mDisplayHeight / STANDARD_HEIGHT;
    }

}


```
  

* 头条density适配

```java

public class Density {

    private static final float  WIDTH = 320;//参考设备的宽，单位是dp 320 / 2 = 160

    private static float appDensity;//表示屏幕密度
    private static float appScaleDensity; //字体缩放比例，默认appDensity

    public static void setDensity(final Application application, Activity activity){
        //获取当前app的屏幕显示信息
        DisplayMetrics displayMetrics = application.getResources().getDisplayMetrics();
        if (appDensity == 0){
            //初始化赋值操作
            appDensity = displayMetrics.density;
            appScaleDensity = displayMetrics.scaledDensity;

            //添加字体变化监听回调
            application.registerComponentCallbacks(new ComponentCallbacks() {
                @Override
                public void onConfigurationChanged(Configuration newConfig) {
                    //字体发生更改，重新对scaleDensity进行赋值
                    if (newConfig != null && newConfig.fontScale > 0){
                        appScaleDensity = application.getResources().getDisplayMetrics().scaledDensity;
                    }
                }

                @Override
                public void onLowMemory() {

                }
            });
        }

        //计算目标值density, scaleDensity, densityDpi
        float targetDensity = displayMetrics.widthPixels / WIDTH; // 1080 / 360 = 3.0
        float targetScaleDensity = targetDensity * (appScaleDensity / appDensity);
        int targetDensityDpi = (int) (targetDensity * 160);

        //替换Activity的density, scaleDensity, densityDpi
        DisplayMetrics dm = activity.getResources().getDisplayMetrics();
        dm.density = targetDensity;
        dm.scaledDensity = targetScaleDensity;
        dm.densityDpi = targetDensityDpi;
    }

}

```

* 刘海屏适配

```java

@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        //1.设置全屏
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        Window window = getWindow();
        window.setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);

        //华为， 小米，oppo
        //1.判断手机厂商， 2，判断手机是否刘海， 3，设置是否让内容区域延伸进刘海 4，设置控件是否避开刘海区域  5， 获取刘海的高度

        //判断手机是否是刘海屏
        boolean hasDisplayCutout = hasDisplayCutout(window);
        if (hasDisplayCutout){
            //2.让内容区域延伸进刘海
            WindowManager.LayoutParams params = window.getAttributes();
            /**
             *  * @see #LAYOUT_IN_DISPLAY_CUTOUT_MODE_DEFAULT 全屏模式，内容下移，非全屏不受影响
             *  * @see #LAYOUT_IN_DISPLAY_CUTOUT_MODE_SHORT_EDGES 允许内容去延伸进刘海区
             *  * @see #LAYOUT_IN_DISPLAY_CUTOUT_MODE_NEVER 不允许内容延伸进刘海区
             */
            params.layoutInDisplayCutoutMode = WindowManager.LayoutParams.LAYOUT_IN_DISPLAY_CUTOUT_MODE_SHORT_EDGES;
            window.setAttributes(params);

            //3.设置成沉浸式
            int flags = View.SYSTEM_UI_FLAG_FULLSCREEN | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN;
            int visibility = window.getDecorView().getSystemUiVisibility();
            visibility |= flags; //追加沉浸式设置
            window.getDecorView().setSystemUiVisibility(visibility);
        }

        setContentView(R.layout.activity_main);

//        Button button = findViewById(R.id.button);
//        RelativeLayout.LayoutParams layoutParams = (RelativeLayout.LayoutParams) button.getLayoutParams();
//        layoutParams.topMargin = heightForDisplayCutout();
//        button.setLayoutParams(layoutParams);

        RelativeLayout layout = findViewById(R.id.container);
        layout.setPadding(layout.getPaddingLeft(), heightForDisplayCutout(), layout.getPaddingRight(), layout.getPaddingBottom());
    }

    private boolean hasDisplayCutout(Window window) {

        DisplayCutout displayCutout;
        View rootView = window.getDecorView();
        WindowInsets insets = rootView.getRootWindowInsets();
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.P && insets != null){
            displayCutout = insets.getDisplayCutout();
            if (displayCutout != null){
                if (displayCutout.getBoundingRects() != null && displayCutout.getBoundingRects().size() > 0 && displayCutout.getSafeInsetTop() > 0){
                    return true;
                }
            }
        }
        return true; //因为模拟器原因，这里设置成true
    }

    //通常情况下，刘海的高就是状态栏的高
    public int heightForDisplayCutout(){
        int resID = getResources().getIdentifier("status_bar_height", "dimen", "android");
        if (resID > 0){
            return getResources().getDimensionPixelSize(resID);
        }
        return 96;
    }


```

* 熟练自定义控件
  * 自绘控件
  * 组合控件
  * 继承控件
  * 事件类控件
  * 容器类控件


* 属性动画
  * vsync信号
  * 插值器：属性值从初始值过渡到结束值的变化规律
  * 估值器：属性值从初始值过渡到结束值的变化具体数值
  * ObjectAnimator是ValueAnimator的子类
  * ObjectAnimator objectAnimator = ObjectAnimator.ofFloat(textView, "translationX", -textView.getLeft(), mWidth, 0);
  * ValueAnimator.ofInt()
