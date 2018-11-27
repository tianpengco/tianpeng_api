## 此文档说明开发者如何接入天鹏，请仔细阅读。
 

## 文档说明

此文档仅供开发者使用 API 方式对接时使用


## 接入说明

### 请求 URL

当需要请求广告时，发送一个 HTTP POST 请求到下面的地址

测试环境： https://ad.tianpengnet.cn/ad/tianpeng/test
生产环境： https://ad.tianpengnet.cn/ad/tianpeng/prod

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

| 字段类型  | 类型     | 必须 | 描述                                                                                                                                |
| --------- | -------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------- |
| id        | string   | 是   | app id，请提前将您的应用注册到玉米广告平台[https://www.yumimobi.com](https://www.yumimobi.com)，该 ID 为注册后玉米广告平台生成的 ID |
| name      | string   | 是   | app 名称                                                                                                                            |
| app_key   | string   | 否   | app key，该字段已经废弃，不再使用。如果填写，可以填写与 app id 相同的值                                                             |
| bundle    | string   | 是   | app bundle id，包名                                                                                                                 |
| ver       | string   | 否   | app 版本号                                                                                                                          |
| cat       | []string | 否   | app 类别                                                                                                                            |
| publisher | 对象     | 否   |                                                                                                                                     |

##### site 对象信息

| 字段名称   | 类型     | 必须 | 描述                                                                                                                                 |
| ---------- | -------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------ |
| id         | string   | 是   | 网站 ID，请提前将您的应用注册到玉米广告平台[https://www.yumimobi.com](https://www.yumimobi.com)，该 ID 为注册后玉米广告平台生成的 ID |
| name       | string   | 否   | 网站名称                                                                                                                             |
| domain     | string   | 否   | 网站域名                                                                                                                             |
| page       | string   | 是   | 当前页面网址                                                                                                                         |
| cat        | []string | 否   | 网站类别                                                                                                                             |
| sectioncat | []string | 否   | 网站当前频道类别                                                                                                                     |
| pagecat    | []string | 否   | 网站当前页面类别                                                                                                                     |
| ref        | string   | 否   | 当前页面 Referrer 网址                                                                                                               |
| search     | string   | 否   | 进入当前页面的搜索关键词                                                                                                             |
| mobile     | int      | 是   | 是否为移动网站，1 为移动网站                                                                                                         |
| keywords   | string   | 否   | 网页关键字，可多个，逗号分隔                                                                                                         |
| publisher  | 对象     | 否   | 流量提供方                                                                                                                           |

###### Publisher 对象信息

| 字段名称 | 类型   | 必须 | 描述               |
| -------- | ------ | ---- | ------------------ |
| name     | string | 是   | 流量提供方名称     |
| domain   | string | 否   | 流量提供方顶级域名 |
| cat      | string | 否   | 流量提供方类别     |

##### Device 对象信息

| 字段名称        | 类型    | 必须 | 描述                                                                  |
| --------------- | ------- | ---- | --------------------------------------------------------------------- |
| model           | string  | 是   | 设备型号                                                              |
| make            | string  | 否   | 生产厂商，例如：“Samsung”                                             |
| brand           | string  | 否   | 手机品牌，例如：“MI4”                                                 |
| plmn            | string  | 否   | 国家运营商编号                                                        |
| adt             | boolean | 否   | 是否允许通过追踪用户行为进行定向投放，0：不允许，1：允许，默认为 1    |
| connection_type | string  | 是   | 网络类型，空串表示未知，值为 wifi，2g，3g，4g，ethernet，cell_unknown |
| carrier         | int     | 是   | 运营商，0：移动，1：电信，3：联通，4：unknown                         |
| orientation     | int     | 是   | 设备方向，1：纵向，3：横向                                            |
| mac             | string  | 否   | MAC 地址，                                                            |
| imei            | string  | 否   | IMEI 码。iOS 没有 (cdma 手机请传 meid 码)                             |
| imsi            | string  | 否   | imsi                                                                  |
| android_id      | string  | 否   | Android ID 。Android 手机不传会影响填充                               |
| android_adid    | string  | 否   | Android AD ID                                                         |
| ios_adid        | string  | 是   | ios 系统的 idfa。                                                     |
| idfv            | string  | 否   | idfv                                                                  |
| openudid        | string  | 否   | openudid                                                              |
| local           | string  | 否   | 设备上的本地首选项设置                                                |
| os_type         | string  | 是   | 操作系统类型，值为"ios"， "android"， "wp"(windows phone)             |
| os_version      | string  | 是   | 操作系统版本                                                          |
| screen          | 对象    | 是   | 设备的屏幕信息                                                        |
| geo             | 对象    | 否   | 设备的位置信息                                                        |

###### Screen 对象信息

| 字段名称 | 类型  | 必须 | 描述                                                                    |
| -------- | ----- | ---- | ----------------------------------------------------------------------- |
| w        | int   | 是   | 水平分辨率，单位：像素                                                  |
| h        | int   | 是   | 纵向分辨率，单位：像素                                                  |
| dpi      | int   | 否   | 像素密度，单位：每英寸像素个数                                          |
| pxratio  | float | 否   | 屏幕物理像素密度，例：iPhone 3 为 1，iPhone 4 为 2，iPhone 6S plus 为 3 |

###### Geo 对象信息

| 字段名称 | 类型  | 必须 | 描述 |
| -------- | ----- | ---- | ---- |
| lat      | float | 是   | 纬度 |
| lon      | float | 是   | 经度 |
| accu     | int   | 否   | 精度 |

##### User 对象信息

| 字段名称 | 类别   | 必须 | 描述                                 |
| -------- | ------ | ---- | ------------------------------------ |
| id       | string | 否   | 用户 id                              |
| gender   | int    | 否   | 性别，0：女，1：男，2：其他，3：未知 |
| age      | int    | 否   | 年龄                                 |
| keywords | array  | 否   | 用户感兴趣的关键词                   |

##### Ad 对象信息

| 字段名称        | 类别   | 必须 | 描述                                                                                                                                                     |
| --------------- | ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type            | int    | 是   | 广告类型，0：横幅，1：插屏，2：开屏，3：原生，4：视频                                                                                                    |
| place_id        | string | 是   | 广告位 id，请提前将您的广告位注册到玉米广告平台[https://www.yumimobi.com](https://www.yumimobi.com)，该 ID 为注册后玉米广告平台生成的 Slot ID                 |
| floor_price     | float  | 否   | 底价，单位为分                                                                                                                                           |
| currency        | string | 否   | 货币单位，值为“CNY”，“USD”。当填写了 floor_price 后，该值为必填                                                                                          |
| w               | int    | 是   | 广告位宽度                                                                                                                                               |
| h               | int    | 是   | 广告位高度                                                                                                                                               |
| pos             | int    | 否   | 广告位位置，0：未知，4：头部，5：底部,6：侧边栏，7：全屏                                                                                                 |
| inventory_types | 数组   | 否   |<br> banner&插屏&开屏广告类型支持的广告资源类型，1：图片，2：图文，4：html5，5：文本，7：html5 url，即一个指向 html5 素材页面的 url；               <br>视频广告类型支持的广告资源类型，3：视频；<br>原生广告类型支持的广告资源类型，6：原生；<br>如果为空，则默认只支持 1：图片 <br><font color="#dd0000">注：不同type支持inventory_types不同；</font><br /> |
| native          | 对象   | 否   | 原生广告信息                                                                                                                                             |

###### Native 对象信息

| 字段名称 | 类型       | 必须 | 描述                                                                                                                     |
| -------- | ---------- | ---- | ------------------------------------------------------------------------------------------------------------------------ |
| layout   | int        | 是   | 原生广告类型，1： 内容墙， 2： 应用墙，3：新闻流， 4：聊天列表，5：走马灯广告，6：内容流，7：矩阵                        |
| assets   | Asset 数组 | 是   | 原生广告元素列表，当前有 5 种元素，分别为标题 (title)， Icon(img)， Large image (img)，Description (data)， Rating(data) |

**Asset 对象信息**

| 字段名称 | 类型 | 必须 | 描述                                         |
| -------- | ---- | ---- | -------------------------------------------- |
| id       | int  | 是   | 广告元素 id                                  |
| required | int  | 否   | 广告元素是否必须，1：必须，0：可选，默认为 0 |
| title    | 对象 | 否   | 文字元素                                     |
| img      | 对象 | 否   | 图像元素                                     |
| data     | 对象 | 否   | 其他数据元素                                 |

> img，title，data 这三个元素，一个 asset 只能存在一个

**Image 对象信息**

| 字段名称 | 类型 | 必须 | 描述                                                           |
| -------- | ---- | ---- | -------------------------------------------------------------- |
| type     | int  | 是   | image 元素的类型，1：图标，2：品牌 Logo，3：大图               |
| w        | int  | 否   | image 元素的宽度，单位为像素，当广告形式为 native 时，该值必填 |
| h        | int  | 否   | image 元素的高度，单位为像素，当广告形式为 native 时，该值必填 |

**Title 对象信息**

| 字段名称 | 类型 | 必须 | 描述                   |
| -------- | ---- | ---- | ---------------------- |
| len      | int  | 是   | title 元素最大文字长度 |

**Data 对象信息**

| 字段名称 | 类型 | 必须 | 描述                                                                                                                                                                                                                                        |
| -------- | ---- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type     | int  | 是   | 数据类型 1：Sponsor 名称，应该包含品牌名称，2：描述，3：打分，4：点赞个数，5：下载个数，6： 产品价格，7：销售价格，往往和前者结合，表示折扣价，8：电话，9：地址，10：描述 2，11：显示的链接，12：行动按钮名称，1001：视频 url，1002：评论数 |
| len      | int  | 是   | 元素最大文字长度                                                                                                                                                                                                                            |

##### Zplay 对象信息

| 字段名称           | 类型   | 必须 | 描述                                      |
| ------------------ | ------ | ---- | ----------------------------------------- |
| app_channel        | string | 否   | 应用渠道 ID                               |
| uuid               | string | 否   | uuid                                      |
| request_id         | string | 否   | request_id                                |
| preload            | int    | 否   | 插屏是否预加载 0 不预加载 插屏，1，预加载 |
| banner_interval    | int    | 否   | Banner 轮播时间，单位秒                   |
| intersect_interval | int    | 否   | 插屏轮播时间，单位秒                      |
| splash_interval    | int    | 否   | 开屏轮播时间，单位秒                      |
| is_close           | int    | 否   | 是否可关闭， 0：不可关闭， 1：可关闭      |
| ad_loc_id          | string | 否   | 广告位 id                                 |
| ios_idfv           | string | 否   | ios idfv                                  |
| open_uuid          | string | 否   | open_uuid， 设备号                        |

### ADX 返回信息

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

##### Zplay 对象信息

| 字段名称      | 类型   | 必须 | 描述                              |
| ------------- | ------ | ---- | --------------------------------- |
| app_id        | string | 否   | zplay ssp api 返回的 app id       |
| position_sid  | string | 否   | zplay ssp api 返回的 position sid |  |
| app_secret    | string | 否   | zplay ssp api 返回的 app secret   |
| trans_data    | string | 否   | zplay ssp api 透传数据            |
| deep_link_url | string | 否   | deeplink 链接访问地址             |

###### Native 对象信息

| 字段名称   | 类型           | 必须 | 描述                                                                                                           |
| ---------- | -------------- | ---- | -------------------------------------------------------------------------------------------------------------- |
| assets     | Asset 对象数组 | 是   | 原生广告元素列表，当前主要支持 5 种元素，分别为标题 (title)， 图标(img)， 大图(img)， 描述 (data)，得分 (data) |
| imptracker | 数组           | 否   | 展示跟踪地址数组，需要返回一个 1 像素图片                                                                      |
| link       | 对象           | 否   | 目标链接，默认链接对象，当 assets 中不包括 link 对象时，使用此对象                                             |

**Asset 对象信息**

| 字段名称 | 类型 | 必须 | 描述                                              |
| -------- | ---- | ---- | ------------------------------------------------- |
| id       | int  | 是   | 广告元素 ID                                       |
| required | int  | 否   | 广告元素是否必须显示，1：必须，0：可选， 默认为 0 |
| title    | 对象 | 否   | 文字元素                                          |
| img      | 对象 | 否   | 图像元素                                          |
| data     | 对象 | 否   | 其他数据元素                                      |
| link     | 对象 | 否   | 点击目标链接                                      |

**Image 对象信息**

| 字段名称 | 类型   | 必须 | 描述                         |
| -------- | ------ | ---- | ---------------------------- |
| url      | string | 是   | image url 地址               |
| w        | int    | 否   | image 元素的宽度，单位为像素 |
| h        | int    | 否   | image 元素的宽度，单位为像素 |

**Title 对象信息**

| 字段名称 | 类型   | 必须 | 描述     |
| -------- | ------ | ---- | -------- |
| text     | string | 是   | 标题文字 |

**Data 对象信息**

| 字段名称 | 类型   | 必须 | 描述     |
| -------- | ------ | ---- | -------- |
| label    | string | 否   | 数据名称 |
| value    | string | 是   | 数据正文 |

**Link 对象信息**

| 字段名称     | 类型   | 必须 | 描述                                                                                                                             |
| ------------ | ------ | ---- | -------------------------------------------------------------------------------------------------------------------------------- |
| url          | string | 是   | 目标链接                                                                                                                         |
| clicktracker | 数组   | 否   | 点击追踪链接                                                                                                                     |
| type         | int    | 否   | 点击动作类型，1：在 app 内 webview 打开目标链接，2：在系统浏览器打开目标链接，3：打开地图，4：拨打电话，5：播放视频，6：App 下载，7：应用唤醒  |
| fallback_url       | string   | 否   | 应用唤醒失败后的打开地址，允许使用[宏](supported_macros.md)，例http://www.zplay.cn/ad/{AUCTION_BID_ID}                                                                          |
| fallback_action    | int      | 否   | fallback_url的动作类型，1：在app内webview打开目标链接，2：在系统浏览器打开目标链接，3：打开地图，4：拨打电话，5：播放视频，6：App下载，7：应用唤醒                                                                          |
 
