## 第三章  Android控件架构与自定义控件详解

### Android控件架构

​         Android中的每个控件都会在界面中占得一块矩形区域， 

​        Android中控件被分为两类：**1. ViewGroup ** **2. View**

​         通过**ViewGroup**, 整个界面上的控件形成了一个树形结构，这也就是控件树，上层控件负责下层控件的测量与绘制，并传递交互事件。在Activity中使用`findViewById()`方法，就是在控件树中以树的深度优先遍历来查找树的对应元素。在每棵控件树的顶部，都有一个ViewParent对象，这就是每棵控件树的控制核心，所有的交互管理事件都由它来统一调度和分配，从而可以对整个视图进行整体控制。



​               ![View结构](C:\Users\Administrator\Desktop\view.png)                ![View结构](C:\Users\Administrator\Desktop\activity_view.png)

**ContentView** ： 是一个ID为content的Framelayout，activity_main.xml就是设置在这样一个FrameLayout里。