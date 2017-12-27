mapDialogModule模块
===

配置文件readme_chartInfo.json说明
---
| 参数 | 类型 | 说明 |
|---|---|---|
|dataSourcePath|string|数据源地址的key|
|pathParams|string|数据源地址的key|
|width|string|数据源地址的key|
|height|string|数据源地址的key|
|setting|string|数据源地址的key|


####配置示例
```
{
    "dataSourcePath": "rainDialogData",
    "pathParams": {
        "stcd": "@stcd",
        "time":"@time"
    },
    "width": 660,
    "height": 400,
    "setting": [{
        "infos": [
            {
                
                "type":"title",
                "fontSize":12,
                "titleConfig":{
                    "name":"@stnm",
                    "time":{
                        "btime":{
                            "key":"@time",
                            "index":0,
                            "format":"YYYY年MM月DD日HH时"
                        },
                        "etime":{
                            "key":"@time",
                            "index":1,
                            "format":"- YYYY年MM月DD日HH时"
                        }
                    }
                },
                "content":"{name}雨量柱状图 <br /> {time}"
            },
            {
                "name": "",
                "key": "list",
                "textColor":"#fff",
                "type": "chart"
            },
            {
                "name": "累计雨量（mm）",
                "key": "sum_precipitation",
                "ofcol":1,
                "col":23,
                "type": "text"
            },
            {
                "name": "测站地址",
                "key": "stlc",
                "ofcol":1,
                "col":23,
                "type": "text"
            }
        ],
        "width": 660,
        "height": 350,
        "legend":"hide",
        "fixed": "2",
        "xFormat": "DD日\nHH时",
        "toolTipFormat": "YYYY年MM月DD日HH时mm分",
        "ySetting": [
        {
            "name": "雨情（mm）",
            "key": "precipitation",
            "color": "#70F3FF",
            "valueType": "monotone",
            "chartType": "column"
            }
        ],
        "xSetting": {
            "name": "tm",
            "key": "tm"

        }
    }]
    
}


```