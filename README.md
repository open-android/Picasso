# 很简单的android图片加载框架Picasso
开源项目地址:[https://github.com/open-android/Picasso](https://github.com/open-android/Picasso)
# 运行效果
  ![](website/static/sample.png)
  * 更多干货请下载app


![黑马助手.png](http://upload-images.jianshu.io/upload_images/4037105-f777f1214328dcc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 使用步骤
### 1. 在project的build.gradle添加如下代码(如下图)

	allprojects {
	    repositories {
	        ...
	        maven { url "https://jitpack.io" }
	    }
	}
  
### 2. 在Module的build.gradle添加依赖

    compile 'com.github.open-android:Picasso:0.1.0'
### 3. Imageview加载图片

	   Picasso.with(context) //设置context
        .load(url) //图片url地址
        .placeholder(R.drawable.placeholder) //加载时显示的图片
        .error(R.drawable.error) //加载错误显示的图片
        .fit() //自动按照图片尺寸进行压缩
        .tag("image") //图片tag，便于控制图片加载和暂停加载
        .into(view);//图片显示的imageview
### 4. 控制图片加载和停止加载

	  我们在列表或者是gradview中显示图片时，滑动列表时可以暂停加载图片，等滑动结束后再加载
	  listView.setOnScrollListener(new AbsListView.OnScrollListener() {
            @Override
            public void onScrollStateChanged(AbsListView view, int scrollState) {
                final Picasso picasso = Picasso.with(SampleGridViewActivity.this);
                if (scrollState == SCROLL_STATE_IDLE || scrollState == SCROLL_STATE_TOUCH_SCROLL) {
                    picasso.resumeTag("image");//开始加载所有tag为image的imageview
                } else {
                    picasso.pauseTag("image");//开始加载所有tag为image的imageview
                }
            }
  ###在AndroidManifest.xml中配置网络权限

    <uses-permission android:name="android.permission.INTERNET" />
  
  
