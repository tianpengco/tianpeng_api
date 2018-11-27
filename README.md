## 此文档说明开发者如何接入天鹏广告 API，请仔细阅读。
 

此文档仅供开发者使用 API 方式对接时使用


## 接入说明

### 请求 URL

测试环境   https://ad.tianpengnet.cn/ad/tianpeng/test \
生产环境  https://ad.tianpengnet.cn/ad/tianpeng/prod 

### 通信方式及编码

HTTPS 协议、POST 方法，数据使用 JSON 格式，编码采用 UTF-8 编码。


#### Request 字段信息

| 字段名称   | 类型        | 必须 | 描述                                                                                                                               |
| ---------- | ----------- | ---- | ---------------------------------------------------------------------------------------------------------------------------------- |
| ver        | string      | 是   | 当前版本号 2.0                                                                                                         
| appkey  | string      | 是   |  应用程序唯一标识（我方提供）                                                                                       |
| pid    | string         | 是   | 广告位 （我方提供）                                                                                                                                                                                                   
| app        | 对象        | 是   | app 对象信息                                                                                                                       |                                                                                                         
| device     | 对象        | 是   | 设备信息                                                                                                                                                                                                                                          
| ads        | ad 对象数组 | 是   | 广告信息数组        |                                                                                                             

##### app 对象信息

| 字段名称        | 类型    | 必须 | 描述                                                                  |
| --------------- | ------- | ---- | --------------------------------------------------------------------- |
| name      | string   | 是   | app 名称      |                                                         
| bundle    | string   | 是   | app bundle id，包名  |         
                                                                                 

  

##### Device 对象信息

| 字段名称        | 类型    | 必须 | 描述                                                                  |
| --------------- | ------- | ---- | --------------------------------------------------------------------- |
| ip              | string  | 是   | 设备当前 ip                                                              |
| idfa           | string  | 是   |  IOS IDFA                                                             |
| idfv            | string  | 是   | IOS idfv                                        |
| anid           | string  | 是   | Android ID                                             |
| imei            | string  | 是   | imei                                                        |
| imsi            | string  | 是   | imsi                                                        |
| mac            | string  | 是   | mac 地址，如 00:02:00:00:00:00                                                        |
| ua            | string  | 是   | 浏览器 userAgent                                                        |
| type            | string  | 是   | 设备类型(0 – phone，1 – pad，2 – 其他)                                                        |
| os            | string  | 是   | 操作系统类型(0 – IOS，1 – ANDROID)                                                        |
| osv            | string  | 是   | 操作系统版本，如：10.2.1                                                        |
| brand            | string  | 是   | 设备品牌，如：HUAWEI                                                        |
| model            | string  | 是   | 设备型号，如：MATE9                                                        |
| sw            | string  | 是   | 设备屏幕宽度，像素，如 1080                                                        |
| sh            | string  | 是   | 设备屏幕高度，像素，如 1920                                                   |
| lat            | string  | 是   | 纬度                                                        |
| lon            | string  | 是   | 经度                                                        |
| orientation    | string  | 是 |横竖屏，0–竖屏，1–横屏                                                 |
| mcc            | string  | 是   | 移动国家码，中国：460                                                       |
| mnc            | string  | 是   | 移动网络码，移动 00/02/07，联通 01/06，电信 03/05/11           |
| connection     | string  | 是   | 网络类型：0-未知，1-wifi，2-2G，3-3G，4-4G                                      |
| density        | string  | 否   | 屏幕像素密度，如，1/2/3/1.5                                                     |
| lang            | string  | 否   |当前使用的语言，如 zh-cn                                                        |


##### Ad 对象信息

| 字段名称        | 类别   | 必须 | 描述                                                                                                                                                     |
| --------------- | ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type            | int    | 是   | 广告类型，0：横幅，1：插屏，2：开屏，3：原生，4：视频 |
| w               | int    | 是   | 广告位宽度        |                                                                                                                                       
| h               | int    | 是   | 广告位高度       |                                                                                                                                        
| pos             | int    | 否   | 广告位位置，0：未知，4：头部，5：底部,6：侧边栏，7：全屏                                                                                                 |
| inventory_types | 数组   | 否   |<br> banner&插屏&开屏广告类型支持的广告资源类型，1：图片，2：图文，4：html5，5：文本，7：html5 url，即一个指向 html5 素材页面的 url；               <br>视频广告类型支持的广告资源类型，3：视频；<br>原生广告类型支持的广告资源类型，6：原生；<br>如果为空，则默认只支持 1：图片 <br><font color="#dd0000">注：不同type支持inventory_types不同；</font><br /> |

 

#### Response 字段信息

| 字段名称 | 类型        | 必须 | 描述                                                                     |
| -------- | ----------- | ---- | ------------------------------------------------------------------------ |
| code     | int         | 是   | 返回结果，0：成功，小于 0 表示失败                                       |
| msg      | string      | 否   | 失败的话，会填写失败原因，例："网络错误"                                 |
| ads      | ad 对象数组 | 否   | 如果失败，或者无对应广告则无此数据                                       |


##### Ad 对象信息

| 字段名称           | 类型     | 必须 | 描述                                                                                                                                           |
| ------------------ | -------- | ---- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| source                 | string   | 否   | 广告来源   |
| action_type             | int   | 否   | 交互类型：0-跳转落地页，1-下载   |
| inventory_type             | int   | 否   | 广告资源类型，1：图片，2：图文，3：视频，4：html5，5：文本，6：原生，7：html5 url，即一个指向 html5 素材页面的 url   |
| action             | int   | 否   | 广告动作类型，1：在 app 内 webview 打开目标链接，2：在系统浏览器打开目标链接，3：打开地图，4：拨打电话，5：播放视频，6：App 下载， 7：应用唤醒   |
| adw             | int   | 否   | 广告宽   |
| adh             | int   | 否   | 广告高   |
| html             | string   | 否   |  html 广告代码，需要用 webview 展示   |
| image_url             | array   | 否   | 广告图片地址数组，一般为 1 个，原生信息流广告可能为多个   |
| landing_url             | string   | 否   | 落地页(广告点击跳转地址) / 下载地址   |
| req_download_url             | string   | 否   | 特殊下载类广告   |
| deeplink_url             | string   | 否   | 搜索终端是否安装对应 app，有则跳转至 app对应地址，无则跳转到 landing_url   |
| video             | string   | 否   | 视频广告封面素材对象，详见下方   |
| show_report             | array   | 否   | 展示监控数组，广告展示后触发上报   |
| click_report             | array   | 否  | 点击监控数组，用户点击后触发上报   |
| deeplink_report             | array   | 否   | deeplink 类广告成功调用后，触发上报   |
| load_report             | array   | 否   | 加载监控数组，加载广告的同时触发上报   |
| app_downstart_report             | array   | 否   | 下载开始上报监控   |
| app_downend_report             | array   | 否   | 下载成功上报监控   |
| app_installstart_report             | array   | 否   | 安装开始上报监控   |
| app_installend_report             | array   | 否   | 安装成功上报监控   |
| app_open_report             | array   | 否   | 安装成功后打开应用上报监控   |
| package_name             | string   | 否   | 下载包名称   |
| icon             | string   | 否   | 信息流广告图标   |
| title             | string   |否   | 广告标题   |
| desc             | string   | 否   | 广告描述   |
| download_file_name             | string   | 是   | 下载文件名，动作类型为下载类型时需要   |
| adlogo             | string   |否   | 广告标识图标   |
| file_size             | int   | 否   | 当广告为下载广告时，这是下载文件大小   |

###### Video 对象信息

| 字段名称                   | 类型   | 必须 | 描述                                           |
| -------------------------- | ------ | ---- | ---------------------------------------------- |
| start                        | string | 是   | 视频加载之前初始封面                                 |
| end                        | string | 是   | 视频播放结束封面                                  |
| url                        | string | 是   | 视频播放 url                                   |
| play_duration              | int    | 否   | 视频播放时长， 单位为秒                        |
| player_start_trackers      | array  | 否   | 播放时上报 url                                 |
| player_end_trackers        | array  | 否   | 播放完成时上报 url                             |
| target_page_show_trackers  | array  | 否   | 落地页展示上报 url，当落地页被展示时上报的监控 URL 列表，应在后台访问   |
| target_page_click_trackers | array  | 否   | 落地页点击上报 url，当落地页被点击时上报的监控 URL 列表，应在后台访问，点击时的跳转地址为ad.target_url。注意：当填写此数组时，请勿再次填写ad.click_trackers数组。 |

### 测试例子

## 请求参数:
``` json
{
    "ver": "2.0",
    "appkey": "bg76gil7",
    "pid": "an6o1ngv",
    "need_https": 0,
    "app": {
        "name": "DrivingTest",
        "bundle": "org.linable.candy.snow2018"
    },
    "device": {
        "type": 0,
        "osv": "6.0",
        "brand": "Xiaomi",
        "model": "Redmi Note 4",
        "mac": "b0:e2:35:fd:76:ba",
        "ua": "Mozilla",
        "sw": 1080,
        "sh": 1920,
        "orientation": "1",
        "density": 3,
        "mcc": "460",
        "mnc": "01",
        "connection": 1,
        "lang": "zh",
        "os": 1,
        "imei": "863100038994079",
        "imsi": "460011062102506",
        "anid": "ac4f7e622e5275a5"
    },
    "ads": [
        {
            "type": 0,
            "place_id": "an6o1ngv",
            "floor_price": 0,
            "w": 640,
            "h": 100,
            "inventory_types": [  1,  2,  4,  5  ]
        }
    ]
}
```
## 返回数据:
``` json
{
    "ads": [
        {
            "action": 2,
            "adh": 100,
            "adlogo": "http://stxxxo/zhxxyun.png",
            "adw": 640,
            "click_report": [
                "http://xxx"
            ],
            "image_url": [
                "http://xxx2745.jpg"
            ],
            "inventory_type": 1,
            "landing_url": "http://tssss_=",
            "show_report": [
                "http:sssEdQEB&cb=1",
                "http://sss"
            ]
        }
    ],
    "code": 0    
}
```
     
