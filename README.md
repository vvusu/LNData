# LNData 数据收集上报SDK

## 无埋点上报
SDK 实现可视化埋点方案，支持动态修改打点配置文件，动态化更新买点需求。

## 事件列表

| 事件类型 |事件子类型| 描述|
|---|---|---|
|App||应用事件|
||Register|App注册|
||Launch|APP启动|
||Terminated|App后台|
|Click||点击事件|
||Button|按钮点击事件|
||Gesture|手势点击事件（点击，长按）|
||Cell|列表点击事件|
||Switch|开关按钮点击事件|
|Page||页面事件|
||Show|页面展示|
||Hide|页面消失|
||Create|页面创建（支持不上报）|
||Dealloc|页面销毁（支持不上报）|
|Edit||输入事件|
||End|结束文字输入|
||Change|输入文字改变|
|Scroll||滑动事件|
||ToTop|点击滑动到顶部|
||EndDecelerate|滚动结束|
||DidEndDrag|结束手势拖拽|
||WillEndDrag|将要结束手势拖拽|
|WebView||Web事件|
||StartLoad|开始加载web页|
||FinishLoad|完成加载web页|
||FailLoad|加载失败web页|
|Event||手动打点事件|
||自定义|自定义事件类型|
|Error||APP错误事件-网路错误，数据错误等|
||自定义|错误统计类型|
|Crash||APP崩溃事件|

## LNDataSDK接入

#### 导入SDK
`LNData.framework`和 `libsqlite3.tbd`添加到工程中 
`LNData.framework`导入到 `Embeddid Binaries`

#### 添加头文件
```
#import <LNData/LNData.h>
```
#### 在启动时候注册 key为应用ID
```
[LNDataManager startWithAppKey:@""];
```

#### 开启本地Sqlite Web服务器
```
[LNDataManager startDBWebServer];
```

#### 开启圈选, 用于产品标记打点
```
[LNDataMark show];
```
基本打点方法请在 LNDataEvent.h 中查看



## LNData 圈选说明文档
工程中要开启圈选功能，页面上会有工具条展示。

### 圈选
点击工具条上的圈选按钮，应用会进入圈选状态，在屏幕上点击你需要圈选的控件，APP会进入圈选详细设置页面

#### 主要功能：
头部有控件截图展示

| 名称 |说明|
|---|---|
|事件ID |ID生成规则为 当事件有路径（根据事件路径+事件标签 哈希256），当事件没有路径（appID:event_type:subtype 哈希256）|
|事件路径|事件路径会显示当前圈选的控件的页面层级，以及头部会显示控件类型。（可点击切换到父级控件）|
|事件名称|为事件添加一个名称，方便管理|
|事件类型|事件的主类型（可点击更新事件）|
|事件子类型|事件所包含的所有子类型|
|事件标签|事件标签，准确标示控件，生成事件ID用到，（添加`*`符号，会去掉控件路径层级下标，匹配相同路径下的多个控件事件）|
|事件参数|事件参数是SDK 所能获取到控件的基本参数，用于更多维度的数据分析|
|业务参数|业务参数是业务所需要手动设置的业务参数，比如文章ID，商品ID等|
|页面参数|会显示当前控件所在的页面名称（可点击直接进行页面圈选与编辑）|

### 检测
点击工具条上的检测按钮，应用会展示当前页面圈选的所有控件事件

### API
测试服接口
#### 圈选配置接口
app_id,version 参数
[API 示例](./resources/config.json)

#### 打点上报接口
[API 示例](./resources/event.json)

