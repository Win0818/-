## 第三章 View的事件体系

#### View的基础知识

View是Android中所有控件的基类，View是一种界面的控件的一种抽象。

ViewGroup继承了View，所以View本身就可以是单个控件也可以是多个控件组成的一组控件。

##### View的位置参数

​         View的位置主要由四个顶点决定，分别对应于View的四个属性：top, left, right, bottom .其中top是左上角纵坐标，left是左上角横坐标，right是右下角横坐标，bottom是右下角纵坐标。这些都是相对于View的父容器来说的，它是一种相对坐标。

​         从Android3.0开始，View增加了额外的几个参数：x，y， translationX，translationY。其中x， y是View左上角的坐标，而 translationX和 translationY是View左上角相对于父容器的偏移量。这几个参数也是相对于父容器的坐标，并且translationX和translationY的默认值是0，换算关系：
$$
x =  left + translationX       <br/>
y = top + translationY
$$

View在平移的过程中，top和left表示的是原始左上角的位置信息，其值并不会发生改变，此时发生改变的是x，y，translationX和translationY这四个参数。

##### MotionEvent和TouchSlop

**1.  MotionEvent**

- ACTION_DOWN——手指刚接触屏幕

- ACTION_MOVE——手指在屏幕上移动

- ACTION_UP——手指从屏幕上松开的一瞬间
  正常情况下，一次手指触摸屏幕的行为会触发一系列的点事件，获取当前触摸点坐标的方法：

  $$getX()/getY()$$           返回相对于当前View左上角的x 和 y 坐标。

   $$getRawX()/getRawY()$$   返回的是相对于手机屏幕左上角的x 和 y 坐标。

**2.  TouchSlop**

  TouchSlop是系统所能识别出的被认为是滑动的最小距离，通过如下方法就可以获取到这个常量：

```java
ViewConfiguration.get(getContext()).getScaledTouchSlop()
```
##### VelocityTracker、GestureDetector和Scroller
**1.  VelocityTracker**

速度追踪，用于追踪手指在滑动过程中的速度，包括水平和竖直方向的速度。用法。首先，在View的onTouchEvent方法中追踪当前单击事件的速度：

```java
VelocityTracker velocityTracker = VelocityTracker.obtain();
velocityTracker.addMovement(event);
```

