# RxJava

RxJava：**异步**。

RxJava在GitHub上的自我介绍是  

>  "a library for composing asynchronous and event-based programs using observable sequences for the Java VM"（一个在 Java VM 上使用可观测的序列来组成异步的、基于事件的程序的库）。
>

特点：**简洁**。    **随着程序逻辑变得越来越复杂，它依然能够保持简洁。**

## API介绍和原理解析

### 1. 概念：扩展的观察者模式

RxJava的异步实现，是通过一种扩展的观察者模式来实现的。

 观察者模式：A对象(观察者) 对B对象(被观察者) 的某种变化高度敏感，需要在B变化的一瞬间做出反应。采用**注册**(register)或者称为**订阅**(Subscribe)的方式， 告诉被观察者：我需要你的某种状态，你要在它变化的时候通知我。

Android中典型的就是监听器`OnClickListener`. `View`是被观察者，`OnClickListener`是观察者，二者通过`SetOnClickListener`方法达成订阅关系。

​                       ![](http://ww4.sinaimg.cn/mw1024/52eb2279jw1f2rx42h1wgj20fz03rglt.jpg)



（`Button` -> 被观察者、`OnClickListener` -> 观察者、`setOnClickListener()` -> 订阅，`onClick()` -> 事件）

​                       ![](http://ww3.sinaimg.cn/mw1024/52eb2279jw1f2rx4446ldj20ga03p74h.jpg)

### 2. RxJava的观察者模式

RxJava有四个基本概念：`Observable`(可观察者，即被观察者)、`Observer`(观察者)、`Subscribe`(订阅)、事件。

`Observable` 和`Observer` 通过 `subscribe()` 方法实现订阅关系，从而 `Observable` 可以在需要的时候发出事件来通知 `Observer`。

与传统的观察者模式不同，RxJava的事件回调方法除了普通事件`onNext()`(相当于`onClick()`/`onEvent()`)之外，还定义了两个特殊的事件：`onCompleted()`和`onError()`.

- `onCompleted()`:事件队列完成。RxJava     

