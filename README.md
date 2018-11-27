## 此文档说明开发者如何接入天鹏，请仔细阅读。
 

## 文档说明

此文档仅供开发者使用 API 方式对接时使用


## 接入说明

### 请求 URL

当需要请求广告时，发送一个 HTTP POST 请求到下面的地址
测试环境   https://ad.tianpengnet.cn/ad/tianpeng/test
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
| ads        | ad 对象数组 | 是   | 广告信息数组                                                                                                                       |
| zplay      | 对象        | 否   | 该对象仅供 zplay 广告内部使用，开发者（SSP）可忽略                                                                                 |

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
| result   | int         | 是   | 返回结果，0：成功，小于 0 表示失败                                       |
| msg      | string      | 否   | 失败的话，会填写失败原因，例："网络错误"                                 |
| ad       | 对象        | 否   | 如果失败，或者无对应广告则无此数据，此字段为协议版本 1.0（包括）以下有效 |
| ads      | ad 对象数组 | 否   | 如果失败，或者无对应广告则无此数据                                       |
| cur      | string      | 否   | 广告价格货币类型，默认为"CNY"                                            |

##### Ad 对象信息

| 字段名称           | 类型     | 必须 | 描述                                                                                                                                           |
| ------------------ | -------- | ---- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| id                 | string   | 是   | 广告 id                                                                                                                                        |
| place_id           | string   | 是   | 广告位 id，与 request 中的 place_id 对应                                                                                                       |
| action             | int      | 是   | 广告动作类型，1：在 app 内 webview 打开目标链接，2：在系统浏览器打开目标链接，3：打开地图，4：拨打电话，5：播放视频，6：App 下载， 7：应用唤醒 |
| html_snippet       | string   | 否   | html 广告代码                                                                                                                                  |
| image_url          | string   | 否   | 图片地址                                                                                                                                       |
| w                  | int      | 是   | 广告宽度                                                                                                                                       |
| h                  | int      | 是   | 广告高度                                                                                                                                       |
| app_bundle         | string   | 否   | 对于 Android，是应用的 packageName；对于 iOS，是 Bundle identifier                                                                             |
| app_ver            | string   | 否   | 应用版本号                                                                                                                                     |
| target_url         | string   | 否   | 目标地址                                                                                                                                       |
| click_trackers     | array    | 否   | 当点击广告时被上报的监控 URL 列表，应在后台访问                                                                                                      |
| imp_trackers       | array    | 否   | 当广告被展示时被上报的监控 URL 列表，应在后台访问                                                                                                    |
| refresh_interv     | int      | 是   | 广告应该在这个间隔后刷新，若为 0 则不刷 新                                                                                                     |
| inventory_type     | int      | 是   | 广告资源类型，1：图片，2：图文，3：视频，4：html5，5：文本，6：原生，7：html5 url，即一个指向 html5 素材页面的 url                             |
| title              | string   | 否   | 广告标题，图文广告时需要                                                                                                                       |
| desc               | string   | 否   | 广告描述，图文广告时需要                                                                                                                       |
| ssp_id             | string   | 是   | ssp id，该字段为玉米交易平台（ADX）保留字段，开发者（SSP）可忽略                                                                               |
| download_file_name | string   | 否   | 下载文件名，动作类型为下载类型时需要                                                                                                           |
| file_size          | int      | 否   | 当广告为下载广告时，这是下载文件大小                                                                                                           |
| price              | float    | 否   | 广告价格                                                                                                        |
| ex_param           | []string | 否   | 扩展参数                                                                                                                                       |
| ssp_ad_id          | string   | 否   | 自主 api 返回的 sspAdId，该字段为玉米交易平台（ADX）保留字段，开发者（SSP）可忽略                                                              |
| video              | 对象     | 否   | 视频对象                                                                                                                                       |
| native             | 对象     | 否   | 原生广告对象                                                                                                                                   |
| logo_url           | string   | 否   | 角标资源地址                                                                                                                                   |
| fallback_url       | string   | 否   | 应用唤醒失败后的打开地址，允许使用[宏](supported_macros.md)，例http://www.zplay.cn/ad/{AUCTION_BID_ID}                                                                          |
| fallback_action    | int      | 否   | fallback_url的动作类型，1：在app内webview打开目标链接，2：在系统浏览器打开目标链接，3：打开地图，4：拨打电话，5：播放视频，6：App下载，7：应用唤醒                                                                          |

###### Video 对象信息

| 字段名称                   | 类型   | 必须 | 描述                                           |
| -------------------------- | ------ | ---- | ---------------------------------------------- |
| url                        | string | 是   | 视频播放 url                                   |
| play_duration              | int    | 否   | 视频播放时长， 单位为秒                        |
| player_start_trackers      | array  | 否   | 播放时上报 url                                 |
| player_end_trackers        | array  | 否   | 播放完成时上报 url                             |
| target_page_show_trackers  | array  | 否   | 落地页展示上报 url，当落地页被展示时上报的监控 URL 列表，应在后台访问   |
| target_page_click_trackers | array  | 否   | 落地页点击上报 url，当落地页被点击时上报的监控 URL 列表，应在后台访问，点击时的跳转地址为ad.target_url。注意：当填写此数组时，请勿再次填写ad.click_trackers数组。 |

     
