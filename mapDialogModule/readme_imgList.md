mapDialogModule模块
===

配置文件readme_imgList.json说明
---
| 参数 | 类型 | 说明 |
|---|---|---|
|dataSourcePath|string|数据源|
|[pathParams](#pathParams)|Object|数据源参数|
|width|number|弹框宽度|
|height|number|弹框高度|
|type|string|报图类型存在5种,每种对应一个模版的配置文件，当前示例模版为type="imgList"|
|[imgListSetting](#imgListSetting)|Object|面板配置|

### <span id="pathParams">pathParams</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|任意字符串|string|键值对，key为数据源配置的参数key，<br/>value：<br/> 1、值不存在@符号，表示固定值会直接赋值给参数key（key=value）。<br/>2、值存在@符号，<br/>表示从openOptions.pointData对象中寻找@后面字符串对应的key的值,赋值给参数key(key=openOptions.pointData[value]|


### <span id="imgListSetting">imgListSetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|<span id="dataSource">dataSource</span>|string|数据源,其值有2个分支，<br/>1、openOptions:<br/>表示初始化弹框的参数，template中的模版字符串key会从数据源配置中获取，<br/>例：@{stnm}的值为openOptions.pointData[stnm]<br/>serverData:<br/>表示dataSourcePath接口返回的数据集，返回结果直接挂在serverData下（）。**数据源结果必须为数组**|
|timeStatus|boolean|是否显隐日期搜索框，无该参数表示隐藏日期搜索框|
|[time](#time)|object|时间轴配置|
|[img](#img)|object|图片容器配置|
|[info](#info)|object|详情信息配置|

#### <span id="img">img</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|title|string|标题，可不填|
|key|string|数据源，来自于[dataSource](#dataSource)|
|style|object|jsx的样式对象|

#### <span id="time">time</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|title|string|标题，可不填|
|key|string|数据源，来自于[dataSource](#dataSource)，结构构成必须为xxx.xx,xxx为数组，xx为数组中对象的key值|
|style|object|jsx的样式对象|


#### <span id="info">info</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|[list_setting](#list_setting)|Array[Object]|行配置|
|style|object|jsx的样式对象|

#### <span id="list_setting">list_setting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|name|string|中文名称|
|key|string|数据源，来自于[dataSource](#dataSource)|
|format|string|日期的格式化，若值存在表示key对应的值为日期字符串，否则为空或无该参数即可|

### 完整配置示例代码
```
{
    "dataSourcePath": "lzjcDialogData",
    "dataType":"array",
    "pathParams": {
        "stcd": "@stcd",
        "time":"@time",
        "sttp":"@datasttp"
    },
    "width": 860,
    "height": 400,
    "type":"imgList",
    "imgListSetting": {
        "dataSource":"serverData.data",
        "time":{
            "key":"datetime",
            "style":{}
        },
        "img":{
            "key":"list.relative_path",
            "style":{"width": "calc(100% - 150px - 350px)"} 
        },
        "info":{
            "style":{"width": 350} ,
            "list_setting": [
                {
                    "name":"观测位置 :",
                    "key":"position"
                },
                {
                    "name":"观测日期 :",
                    "format":"YYYY-MM-DD HH:mm:ss",
                    "key":"datetime"
                },
                {
                    "name":"填报单位 :",
                    "key":"tbdw"
                },
                {
                    "name":"填报人 :",
                    "key":"uname"
                },
                {
                    "name":"发生程度 :",
                    "key":"occurrence"
                },
                {
                    "name":"处理情况 :",
                    "key":"situation"
                }
            ]
        }
        
    }

}
```

### 完整接口数据结构
```
{
    "data": [{
            "stcd": "SC-2",
            "stnm": "下关镇",
            "department": "下关城区北面",
            "position": "洱海二水厂",
            "description": "水厂",
            "datetime": "2017-11-06T14:45:47",
            "situation": "测试",
            "aid": "114",
            "uname": "strong",
            "occurrence": "无蓝藻，水体清澈，无颗粒状蓝藻",
            "count": 1,
            "list": [{
                "id": 114,
                "file_name": "image",
                "relative_path": "/Doc/UploadFile/Attachement/201711/20171106144531938.jpg",
                "tm": "2017-11-06T14:45:46"
            }]
        },
        {
            "stcd": "SC-2",
            "stnm": "下关镇",
            "department": "下关城区北面",
            "position": "洱海二水厂",
            "description": "水厂",
            "datetime": "2017-11-06T16:32:55",
            "situation": "林章",
            "aid": "126,127",
            "uname": "strong",
            "occurrence": null,
            "count": 2,
            "list": [{
                    "id": 126,
                    "file_name": "image",
                    "relative_path": "/Doc/UploadFile/Attachement/201711/20171106163243137.jpg",
                    "tm": "2017-11-06T16:32:55"
                },
                {
                    "id": 127,
                    "file_name": "image",
                    "relative_path": "/Doc/UploadFile/Attachement/201711/20171106163245028.jpg",
                    "tm": "2017-11-06T16:32:55"
                }
            ]
        },
        {
            "stcd": "SC-2",
            "stnm": "下关镇",
            "department": "下关城区北面",
            "position": "洱海二水厂",
            "description": "水厂",
            "datetime": "2017-11-07T19:31:18",
            "situation": "测试",
            "aid": "172",
            "uname": "strong",
            "occurrence": null,
            "count": 1,
            "list": [{
                "id": 172,
                "file_name": "IMG_3079",
                "relative_path": "/Doc/UploadFile/Attachement/201711/20171107193104261.PNG",
                "tm": "2017-11-07T19:31:18"
            }]
        },
        {
            "stcd": "SC-2",
            "stnm": "下关镇",
            "department": "下关城区北面",
            "position": "洱海二水厂",
            "description": "水厂",
            "datetime": "2017-11-23T15:41:59",
            "situation": "测试",
            "aid": "5388",
            "uname": "strong",
            "occurrence": "目及范围内二分之一水面均有蓝藻分布",
            "count": 1,
            "list": [{
                "id": 5388,
                "file_name": "IMG_3132",
                "relative_path": "/Doc/UploadFile/Attachement/201711/20171123154159383.JPG",
                "tm": "2017-11-23T15:41:58"
            }]
        }
    ]
}
```