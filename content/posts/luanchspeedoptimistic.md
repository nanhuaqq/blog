---
title: "Luanchspeedoptimistic"
date: 2018-09-03T07:47:54+08:00
draft: true
---

## 启动速度的测量

要优化启动速度，前提条件是要知道启动耗时多少，最简单直接也是最笨的方式就是在application的oncreate最开始和末尾都获取一下系统时间

```java
System.currentTimeMillis()
```

然后相减得到时间差。

上面的方式得不到每一个操作的耗时，在优化起来没有目标。

另一种方式是利用```Debug```这个类，同样的在application的onCreate方式的开始和末尾处加入如下代码

```java
if (BuildConfig.DEBUG) {
            Debug.startMethodTracing("filename");
}
```

```java
if (BuildConfig.DEBUG) {
            Debug.stopMethodTracing();
}
```

然后运行程序，启动程序。然后在程序目录下的file文件夹下会自动生成一个filename.trace的文件。在androidstudio下打开该文件，就可以清楚的查看每个方法的耗时。

## 优化策略	

优化策略比较简单，

- 能后台线程初始化的动作就放到后台线程
- 必需要在ui线程初始化的动作，能延迟初始化就延迟初始化

```java
new Thread(){
            @Override
            public void run() {
                super.run();
                Process.setThreadPriority(Process.THREAD_PRIORITY_BACKGROUND);
                //do some inition
            }
 }
```

```java
this.getWindow().getDecorView().post(() -> {
    MyApplication.UIHandler.post(() -> {
        FinbtcInitUtil.initX5();
        FinbtcInitUtil.initAliPush();
        mPresenter.subscribe();
        FinbtcInitUtil.initOpenInstall();
        AnalyticsUtils.track(MyApplication.getAppContext(), AnalyticsCons.AppStart);

    });
});
```

然后大功告成。