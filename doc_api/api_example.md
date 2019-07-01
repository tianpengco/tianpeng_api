## 请求URL:

https://ad.tianpengnet.cn/ad/tianpeng/api

## 请求参数:
``` json
  {
    "ver": "2.0",
    "pid": "abc",
    "need_https": 0,
    "app": {
        "name": "DrivingTest",
        "bundle": "com.test"
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
    "adslot ": {
        "w": 640,
        "h": 100
    }
}
```
## 返回数据:
``` json
{
    "ads": [
        {
            "action": 7,
            "adh": 960,
            "adw": 640,
            "click_report": [
                "http://texxx",
                "xxx"
            ],
            "deeplink_url": "suning://m.suning.com/index?adTypeCodexxx",
            "images_url": [
                "http://sc.ghssad.com/sources/s/2019052511/22/5ce8bba71a427.jpg"
            ],
            "landings_url": [
                "https://cuxiaxxx"
            ],
            "show_report": [
                "http://texxx",
                "httpssss"
            ]
        }
    ],
    "code": 0
}
```
