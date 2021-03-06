
### 设置查看工作日志
在调用```[QAPM startWithAppKey:]```启动 QAPM SDK 前，设置日志输出函数。
可以根据不同发布版本情况进行输出日志控制，具体见如下参考 Demo。（[Demo下载](http://qapm-1253358381.cosgz.myqcloud.com/QAPM_SDK_Outer_v3.0.3.zip)）：

```
void loggerFunc(QAPMLoggerLevel level, const char* log) {

#ifdef RELEASE
    if (level <= QAPMLogLevel_Event) { ///外发版本log
        NSLog(@"%s", log);
    }
#endif
    
#ifdef GRAY
    if (level <= QAPMLogLevel_Info) { ///灰度和外发版本log
        NSLog(@"%s", log);
    }
#endif
    
#ifdef DEBUG
    if (level <= QAPMLogLevel_Debug) { ///内部版本、灰度和外发版本log
        NSLog(@"%s", log);
    }
#endif
}


- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    /// 设置QAPM 日志输出
    [QAPM registerLogCallback:loggerFunc];

    /// ... 
    /// 设置启动QAPM SDK
}
```
  
### 各功能工作状态查看
通过日志输出，开启的功能选项对照日志输出查看是否已经开启功能。

```
2018-12-20 14:56:39.024112+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [内存泄露检测功能]命中用户抽样率
2018-12-20 14:56:39.042624+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [内存泄露检测功能]开启
2018-12-20 14:56:39.042708+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [Blue(卡顿监控)功能]命中用户抽样率
2018-12-20 14:56:39.049071+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [Blue(卡顿监控)功能]开启
2018-12-20 14:56:39.049122+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [Yellow(VC泄露检测功能)]命中用户抽样率
2018-12-20 14:56:39.055291+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [Yellow(VC泄露检测功能)]开启
2018-12-20 14:56:39.055333+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [Sigkill功能]命中用户抽样率
2018-12-20 14:56:39.063032+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [Sigkill功能]开启
2018-12-20 14:56:39.063097+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [资源使用情况监控功能]命中用户抽样率
2018-12-20 14:56:39.078834+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [资源使用情况监控功能]开启
2018-12-20 14:56:39.078940+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [内存最大使用值监控(触顶率功能)]命中用户抽样率
2018-12-20 14:56:39.080742+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [内存最大使用值监控(触顶率功能)]开启
2018-12-20 14:56:39.080772+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [大块内存分配监控功能]命中用户抽样率
2018-12-20 14:56:39.082878+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [大块内存分配监控功能]开启
2018-12-20 14:56:39.082905+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [耗时打点统计功能]命中用户抽样率
2018-12-20 14:56:39.082930+0800 ApmDemo[86515:19364174] [QAPMLogEvent]: [耗时打点统计功能]可用
```
