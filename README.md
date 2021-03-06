# MNProgressDialog [![](https://jitpack.io/v/maning0303/MNProgressHUD.svg)](https://jitpack.io/#maning0303/MNProgressHUD)
一个常用的自定义弹框封装,加载ProgressDialog,状态显示的StatusDialog和自定义Toast,全部支持背景颜色,圆角,边框和文字的自定义,构建者模式,链式调用。


## 截图：
### MProgressDialog
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_dialog_001.png)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_dialog_002.png)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_dialog_006.png)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_dialog_003.png)

### MProgressBarDialog (水平进度条和圆形进度条)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_progressbar_dialog_003.jpg)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_progressbar_dialog_004.jpg)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_progressbar_dialog_002.jpg)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_progressbar_dialog_001.jpg)

### MStatusDialog
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_dialog_004.png)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_dialog_005.png)

### MSToast
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_toast_001.png)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_toast_002.png)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_toast_003.png)
![](https://github.com/maning0303/MNProgressHUD/raw/master/screenshots/mn_toast_004.png)


## 如何添加
### 1:Gradle添加：
#### 1.在Project的build.gradle中添加仓库地址

``` gradle
	allprojects {
		repositories {
			...
			maven { url "https://jitpack.io" }
		}
	}
```

#### 2.在app目录下的build.gradle中添加依赖
``` gradle
	dependencies {
	     compile 'com.github.maning0303:MNProgressHUD:V1.0.7'
	}
```

### 2:源码Module添加：
#### 直接关联mndialoglibrary

``` gradle

	compile project(':mndialoglibrary')

```


## 使用方法(查看Demo详情):

### 1:MProgressDialog 加载Dialog代码使用:
``` java
        
        //默认
        MProgressDialog.showProgress(this);
        //自定义文字
        MProgressDialog.showProgress(this,"自定义文字");
        //不需要文字
        MProgressDialog.showProgress(this,"");
        
        //自定义背景
        MDialogConfig mDialogConfig = new MDialogConfig.Builder()
                 //点击外部是否可以取消
                 .isCanceledOnTouchOutside(true)
                 //全屏背景窗体的颜色
                 .setBackgroundWindowColor(getMyColor(R.color.colorDialogWindowBg))
                 //View背景的颜色
                 .setBackgroundViewColor(getMyColor(R.color.colorDialogViewBg))
                 //View背景的圆角
                 .setCornerRadius(20)
                 //View 边框的颜色
                 .setStrokeColor(getMyColor(R.color.colorAccent))
                 //View 边框的宽度
                 .setStrokeWidth(2)
                 //Progress 颜色
                 .setProgressColor(getMyColor(R.color.colorDialogProgressBarColor))
                 //Progress 宽度
                 .setProgressWidth(3)
                 //Progress 内圈颜色
                 .setProgressRimColor(Color.YELLOW)
                 //Progress 内圈宽度
                 .setProgressRimWidth(4)
                 //文字的颜色
                 .setTextColor(getMyColor(R.color.colorDialogTextColor))
                 //ProgressBar 颜色
                 .setProgressColor(Color.GREEN)
                 //关闭的监听
                 .setOnDialogDismissListener(new OnDialogDismissListener() {
                     @Override
                     public void onDismiss() {
                         MToast.makeTextShort(mContext,"监听到了ProgressDialog关闭了");
                     }
                 })
                 .build();
        MProgressDialog.showProgress(this,"数据上传中...",mDialogConfig);


```


### 2:MStatusDialog 状态Dialog代码使用:
``` java
        //默认
        new MStatusDialog(this).show("保存成功", mContext.getResources().getDrawable(R.drawable.mn_icon_dialog_ok));
        
        //自定义
        MDialogConfig mDialogConfig = new MDialogConfig.Builder()
                        //全屏背景窗体的颜色
                        .setBackgroundWindowColor(getMyColor(R.color.colorDialogWindowBg))
                        //View背景的颜色
                        .setBackgroundViewColor(getMyColor(R.color.colorDialogViewBg2))
                        //字体的颜色
                        .setTextColor(getMyColor(R.color.colorAccent))
                        //View边框的颜色
                        .setStrokeColor(getMyColor(R.color.white))
                        //View边框的宽度
                        .setStrokeWidth(2)
                        //View圆角大小
                        .setCornerRadius(10)
                        //关闭的监听
                        .setOnDialogDismissListener(new OnDialogDismissListener() {
                            @Override
                            public void onDismiss() {
                                MToast.makeTextShort(mContext,"监听到了MStatusDialog关闭了");
                            }
                        })
                        .build();
        new MStatusDialog(mContext,mDialogConfig).show("提交数据失败,请重新尝试!", mContext.getResources().getDrawable(R.mipmap.ic_launcher), 1000);

```

### 3:MToast 代码使用:
``` java

        MToastConfig config = new MToastConfig.Builder()
                //设置显示的位置
                .setGravity(MToastConfig.MToastGravity.CENTRE)
                //文字的颜色
                .setTextColor(getMyColor(R.color.colorAccent))
                //背景色
                .setBackgroundColor(getMyColor(R.color.colorDialogTest))
                //背景圆角
                .setBackgroundCornerRadius(10)
                //背景边框的颜色
                .setBackgroundStrokeColor(Color.WHITE)
                //背景边框的宽度
                .setBackgroundStrokeWidth(1)
                .build();

        //多种方法
        MToast.makeTextShort(mContext, "Toast", config);
        MToast.makeTextShort(mContext, "Toast");

```

### 4:MProgressBarDialog 进度条Dialog代码使用:
``` java

        //新建一个Dialog
        mProgressBarDialog = new MProgressBarDialog.Builder(mContext)
               .setStyle(MProgressBarDialog.MProgressBarDialogStyle_Circle)
               //全屏背景窗体的颜色
               .setBackgroundWindowColor(getMyColor(R.color.colorDialogWindowBg))
               //View背景的颜色
               .setBackgroundViewColor(getMyColor(R.color.colorDialogViewBg2))
               //字体的颜色
               .setTextColor(getMyColor(R.color.colorAccent))
               //View边框的颜色
               .setStrokeColor(getMyColor(R.color.white))
               //View边框的宽度
               .setStrokeWidth(2)
               //View圆角大小
               .setCornerRadius(10)
               //ProgressBar背景色
               .setProgressbarBackgroundColor(Color.BLUE)
               //ProgressBar 颜色
               .setProgressColor(Color.GREEN)
               //圆形内圈的宽度
               .setCircleProgressBarWidth(4)
               //圆形外圈的宽度
               .setCircleProgressBarBackgroundWidth(4)
               //水平进度条Progress圆角
               .setProgressCornerRadius(0)
               //水平进度条的高度
               .setHorizontalProgressBarHeight(10)
               .build();
        mMProgressDialog.show();


```


## 感谢：
#### 源码里面使用了下面库,改了个名字,以免冲突，非常感谢!
#### [materialish-progress](https://github.com/pnikosis/materialish-progress)
#### [CircularProgressBar](https://github.com/lopspower/CircularProgressBar)


## 推荐:
Name | Describe |
--- | --- |
[GankMM](https://github.com/maning0303/GankMM) | （Material Design & MVP & Retrofit + OKHttp & RecyclerView ...）Gank.io Android客户端：每天一张美女图片，一个视频短片，若干Android，iOS等程序干货，周一到周五每天更新，数据全部由 干货集中营 提供,持续更新。 |
[MNUpdateAPK](https://github.com/maning0303/MNUpdateAPK) | Android APK 版本更新的下载和安装,适配7.0，8.0,简单方便。 |
[MNImageBrowser](https://github.com/maning0303/MNImageBrowser) | 交互特效的图片浏览框架,微信向下滑动动态关闭 |
[MNCalendar](https://github.com/maning0303/MNCalendar) | 简单的日历控件练习，水平方向日历支持手势滑动切换，跳转月份；垂直方向日历选取区间范围。 |
[MClearEditText](https://github.com/maning0303/MClearEditText) | 带有删除功能的EditText |
[MNCrashMonitor](https://github.com/maning0303/MNCrashMonitor) | Debug监听程序崩溃日志,展示崩溃日志列表，方便自己平时调试。 |
[MNProgressHUD](https://github.com/maning0303/MNProgressHUD) | MNProgressHUD是对常用的自定义弹框封装,加载ProgressDialog,状态显示的StatusDialog和自定义Toast,支持背景颜色,圆角,边框和文字的自定义。 |
[MNXUtilsDB](https://github.com/maning0303/MNXUtilsDB) | xUtils3 数据库模块单独抽取出来，方便使用。 |
[MNVideoPlayer](https://github.com/maning0303/MNVideoPlayer) | SurfaceView + MediaPlayer 实现的视频播放器，支持横竖屏切换，手势快进快退、调节音量，亮度等。------代码简单，新手可以看一看。 |
[MNZXingCode](https://github.com/maning0303/MNZXingCode) | 快速集成二维码扫描和生成二维码 |
[MNChangeSkin](https://github.com/maning0303/MNChangeSkin) | Android夜间模式，通过Theme实现 |
[SwitcherView](https://github.com/maning0303/SwitcherView) | 垂直滚动的广告栏文字展示。 |
[MNPasswordEditText](https://github.com/maning0303/MNPasswordEditText) | 类似微信支付宝的密码输入框。 |
[MNSwipeToLoadDemo](https://github.com/maning0303/MNSwipeToLoadDemo) | 利用SwipeToLoadLayout实现的各种下拉刷新效果（饿了吗，京东，百度外卖，美团外卖，天猫下拉刷新等）。 |

