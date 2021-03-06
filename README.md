# MotionEventPopupWindow
类似微信根据手指长按位置精准弹出的PopupWindow，自动根据左右上下边距调整显示的方向。[APK体验包](https://github.com/KCrason/MotionEventPopupWindow/blob/master/apk/app-debug.apk)

### 准备工作

1、导入依赖

```
implementation 'com.kcrason:motionevent-popupwindow:1.0.0'
```

### 简单使用(纯微信效果)

1、在需要显示的Activity重写dispatchTouchEvent，并设置一个变量用于保存motionEvent。（如果需要设置一个全局的MotionEvent，则需要在BaseActivity重写dispatchTouchEvent并提供一个方法获取motionEvent对象即可）

```
override fun dispatchTouchEvent(ev: MotionEvent?): Boolean {
        this.mMotionEvent = ev
        return super.dispatchTouchEvent(ev)
    }
```

2、给需要触发显示popupwindow的view设置单击或长按时显示popupwindow，显示popupwindow时，将motionEvent变量传递进去。

```
txtCenterClick.setOnLongClickListener {
            CommonMotionEventPopupWindow(this)
                .showOptions(arrayListOf("复制", "粘贴", "发送", "翻译", "发送给好友"))
                .setOnClickItemOptionsListener { position, optionName ->
                    Toast.makeText(this, "this is $position , optionName:$optionName", Toast.LENGTH_SHORT).show()
                }
                .showMotionEventPopupWindow(it, mMotionEvent)
            return@setOnLongClickListener true
        }
```

### 自定义界面的Popupwindow

1、创建新类继承BaseMotionEventPopupWindow即可。

```
class CustomMotionEventPopupWindow(context: Context) :BaseMotionEventPopupWindow(context) {
    override fun init() {
        //初始化一些参数
    }

    override fun getContainerLayoutId(): Int {
        //返回你需要显示的popupwindow xml
    }

    override fun getRealPopupWindowHeight(): Int {
        //返回popupwindow真实的高度，该高度在计算显示popupwindow的位置时需要用到，必须保证其准确性。
    }

    override fun getWindowWidth(): Int {
        //返回popupwindow的宽度，一般使用固定的值即可。
    }
}
```
2、在需要显示的地方调用``` showMotionEventPopupWindow(anchor: View?, currentMotionEvent: MotionEvent?) ```方法显示popupwindow

### 效果展示

<img width="270" height="585" src="https://s31.aconvert.com/convert/p3r68-cdx67/tpv68-1z756.gif"/><img width="270" height="585" src="https://github.com/KCrason/MotionEventPopupWindow/blob/master/screenshot/2%20(2).jpg"/><img width="270" height="585" src="https://github.com/KCrason/MotionEventPopupWindow/blob/master/screenshot/2%20(3).jpg"/>


### 其他

有问题欢迎提交issue，没问题欢迎给个start
