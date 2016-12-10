测试标题
==========

## 乐视的移动端处理逻辑

其他视频媒体在触发监测代码时，一般会使用 SDK 触发或通过 API 方式传递移动端设备 ID，乐视既不使用 API， 也不用 SDK，所以在 response 中返回监测代码时，需要 AdMaster 自己处理移动参数，将 bidrequest 中的移动参数拼接到监测代码中。

目前获取代码接口返回一种新的形式的监测代码： 不跳转带宏参数的点击监测: `clickMacroWithoutRedirect`

形如：

    http://c.admaster.com.cn/c/a68844,b1125938,c2751,0n__adId__,i7442,m101,1d1,0a__OS__,z__IDFA__,0c__IMEI__,0d__AndroidID__,h

针对乐视，需要做如下的逻辑处理：

* 将 bidrequest 中的 IDFA、IMEI、AndroidId 进行宏替换
* 如果为 iOS, `__OS__` 替换为 1
* 如果是 Android，`__OS__` 替换为 0
* 如果  IDFA、IMEI、AndroidId  没有值，则不替换
