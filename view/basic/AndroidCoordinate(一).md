# Android坐标系

###  一、   getX()、getRawX()、getLeft()的区别

![image](https://raw.githubusercontent.com/androidtodolist/AndroidReview/master/view/basic/resource/AndroidCoordinate_1.png）

-   View提供的获取的坐标以及距离的方法：    
        `getTop()`      获取到的是view自身的顶边到其父布局顶边的距离    
        `getLeft()`     获取到的是view自身的左边到其父布局左边的距离    
        `getRight()`    获取到的是view自身的右边到其父布局左边的距离    
        `getBottom()`   获取到的是view自身底边到其父布局顶边的距离  

-   MotionEvent提供的方法：     
        `getX()`        获取点击事件距离控件左边的距离，即视图坐标
        `getY()`        获取点击事件距离控件顶边的距离，即视图坐标
        `getRawX()`     获取到的是点击事件距离整个屏幕左边的距离，即绝对坐标   
        `getRawY()`     获取到的是点击事件距离整个屏幕顶边的距离，即绝对坐标

-   从 Android 3.0 开始，View 增加了 x，y，translationX 和 translationY。
    x，y 同样是 View 左上角相对父容器的坐标，但不同于 left 和 top ，这两个坐标点的值并一定都是相等的。而不相等的情况是由 translationX 和 translationY 值的设置引起的。

### 二、getScrollX() getTranslationX()

![image](https://raw.githubusercontent.com/androidtodolist/AndroidReview/master/view/basic/resource/AndroidCoordinate_2.png）

![image](https://raw.githubusercontent.com/androidtodolist/AndroidReview/master/view/basic/resource/AndroidCoordinate_2.png）

-   View的scrollTo()和scrollBy()是用于滑动View中的内容，而不是把某个View的位置进行改变。`scrollTo(int x, int y) `是将View中内容滑动到相应的位置，参考的坐标系原点为parent View的左上角

-   如果想改变莫个View在屏幕中的位置，可以使用如下的方法。调用`public void offsetLeftAndRight(int offset)`用于左右移动方法或`public void offsetTopAndBottom(int offset)`用于上下移动。
-   translationX 和 translationY 是 View 左上角相对父容器左上角的偏移量，translationX 和 translationY 默认值都为 0。
    `x = left + translationX`

总结：
-   left/top，right/bottom 的值都是相对父容器而言的，具体为父容器的左上角，而 translationX/Y 可以移动这个参照点（父容器左上角），通过改变参照点的位置来改变 View 的位置。
-   这里要注意的是 translationX/Y 改变参照点的位置是理论上的改变，只是子 View 参照的位置变了，父容器左上角的实际坐标是没有变化的。
-   在这种情况下（translationX/Y 均不为 0，即子 View 的参照点位置变了），x/y 和 left/top 的值就不相等了，此时 x/y 的值是参照父容器左上角实际位置的坐标，而 left/top 是参照 translationX/Y 变化后的坐标点的值。