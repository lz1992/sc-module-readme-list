mapDialogModule模块
===

配置文件readme_chartInfo.json说明
---
| 参数 | 类型 | 说明 |
|---|---|---|
|dataSourcePath|string|数据源|
|[pathParams](#pathParams)|Object|数据源参数|
|width|number|弹框宽度|
|height|number|弹框高度|
|type|string|报图类型存在5种,每种对应一个模版的配置文件，当前示例模版为type="chartInfo"|
|[titleSetting](#titleSetting)|Object|报图标题配置|
|[chartSetting](#chartSetting)|Object|报图配置|
|[infoSetting](#infoSetting)|Array[]|底部文字配置|

### <span id="pathParams">pathParams</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|任意字符串|string|键值对，key为数据源配置的参数key，<br/>value：<br/> 1、值不存在@符号，表示固定值会直接赋值给参数key（key=value）。<br/>2、值存在@符号，<br/>表示从openOptions.pointData对象中寻找@后面字符串对应的key的值,赋值给参数key(key=openOptions.pointData[value]|


### <span id="titleSetting">titleSetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|template|string|模版字符串，通过使用@{xx}实现字符串占位符的替换，支持数据格式化`@{xxx|date(YYYY年MM月DD日HH时)}`，目前支持2种格式化分别是日期和小数保留，<br/>1、`@{xxx|date(YYYY年MM月DD日HH时)}`<br/>date就是日期格式化<br/>2、`@{xxx|toFixed(2)}`<br/>toFixed表示小数保留，(2)为保留两位小数|
|dataSource|string|数据源,其值有2个分支，<br/>1、openOptions:<br/>表示初始化弹框的参数，template中的模版字符串key会从数据源配置中获取，<br/>例：@{stnm}的值为openOptions.pointData[stnm]<br/>serverData:<br/>表示dataSourcePath接口返回的数据集，返回结果直接挂在serverData下（）。|

####titleSetting部分配置示例
```
"titleSetting":{
        "template":"@{stnm}水位过程线 <br /> @{btime|date(YYYY年MM月DD日HH时)} - @{etime|date(YYYY年MM月DD日HH时)}",
        "dataSource":"openOptions.pointData"
    }
```


### <span id="chartSetting">chartSetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|dataSource|string|数据源,其值有2个分支，<br/>1、openOptions:<br/>表示初始化弹框的参数，template中的模版字符串key会从数据源配置中获取，<br/>例：@{stnm}的值为openOptions.pointData[stnm]<br/>serverData:<br/>表示dataSourcePath接口返回的数据集，返回结果直接挂在serverData下（）。|
|width|string|报图宽度|
|height|string|报图高度|
|legend|string|图例是否隐藏，值为hide时隐藏图例|
|textColor|string|弹出内文本颜色|
|fixed|string|数值保留位数|
|xFormat|string|x轴日期的格式化|
|toolTipFormat|string|悬浮宽的格式化|
|[ySetting](#ySetting)|Array[Object]|y轴值的配置，支持多个|
|[xSetting](#xSetting)|Object|x轴值的配置|

#### <span id="ySetting">ySetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|name|string|y轴的中文显示名|
|key|string|表示y轴值的数据来源，即数据来源来至dataSource，<br/>例：dataSource为serverData.data.list时，y轴值serverData.data.list[x][key],list必须为数组，[x]自增序号表示无需理会，|
|color|string|报图颜色|
|valueType|string|固定值，为valueType，目前仅有该值|
|chartType|string|报图类型，目前有3种，line（折线图）、column（柱状图）、arealine（面过程线）|

#### <span id="xSetting">xSetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|name|string|x轴的绑定字段值，和key保持一致即可|
|key|string|表示x轴值的数据来源，即数据来源来至dataSource，<br/>例：dataSource为serverData.data.list时，x轴值serverData.data.list[x][key],list必须为数组，[x]自增序号表示无需理会，|

#### chartSetting部分配置示例
```
 "chartSetting":{
        "dataSource":"serverData.data.list",
        "width": 660,
        "height": 350,
        "legend":"hide",
        "textColor":"#fff",
        "fixed": "2",
        "xFormat": "DD日 \n HH时",
        "toolTipFormat": "YYYY年MM月DD日HH时mm分",
        "ySetting": [{
                "name": "水情(m)",
                "key": "z",
                "color": "#70F3FF",
                "valueType": "monotone",
                "chartType": "arealine"
            }
        ],
        "xSetting": {
            "name": "tm",
            "key": "tm"
        }
    }
```

### <span id="infoSetting">infoSetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|name|string|左侧数据源的中文字符|
|key|string|数据源，取到数据之后赋值|
|ofcol|string|24等分的前置空格占比|
|col|string|24等分的内容占比|
|type|string|类型，有3种,<br/> 1、text<br/>无任何转换，字节取值后赋值<br/> 2、date<br/>日期类型<br/> 3、fixed<br/>数值保留类型|
|fmt|string|当type为date：其值为格式化类型(YYYY年MM月DD天等)<br/>当type为fixed时：其值为保留位数|

#### infoSetting部分配置示例
```
"infoSetting": [
        {
            "name": "最新水位(m)",
            "key": "serverData.data.curz",
            "ofcol":1,
            "col":23,
            "type": "text"
        },
        {
            "name": "站址",
            "key": "serverData.data.stlc",
            "ofcol":1,
            "col":23,
            "type": "text"
        }
    ]
```

#### 完整配置示例
```
{
    "dataSourcePath": "waterDialogData",
    "pathParams": {
        "stcd": "@stcd",
        "time":"@time",
        "sttp":"@datasttp"
    },
    "width": 660,
    "height": 400,
    "type":"chartInfo",
    "titleSetting":{
        "template":"@{stnm}水位过程线 <br /> @{btime|date(YYYY年MM月DD日HH时)} - @{etime|date(YYYY年MM月DD日HH时)}",
        "dataSource":"openOptions.pointData"
    },
    "chartSetting":{
        "dataSource":"serverData.data.list",
        "width": 660,
        "height": 350,
        "legend":"hide",
        "textColor":"#fff",
        "fixed": "2",
        "xFormat": "DD日 \n HH时",
        "toolTipFormat": "YYYY年MM月DD日HH时mm分",
        "ySetting": [{
                "name": "水情(m)",
                "key": "z",
                "color": "#70F3FF",
                "valueType": "monotone",
                "chartType": "arealine"
            }
        ],
        "xSetting": {
            "name": "tm",
            "key": "tm"
        }
    },
    "infoSetting": [
        {
            "name": "最新水位(m)",
            "key": "serverData.data.curz",
            "ofcol":1,
            "col":23,
            "type": "text"
        },
        {
            "name": "站址",
            "key": "serverData.data.stlc",
            "ofcol":1,
            "col":23,
            "type": "text"
        }
    ]
}
```


### 完整接口数据结构
```
{
    "data": {
        "stcd": "20160008",
        "stnm": "万花溪水位站                                ",
        "rvnm": null,
        "hnnm": null,
        "stlc": null,
        "curz": "0.32",
        "curtm": "2018-01-09T16:40:00",
        "warning": " ",
        "warning1": " ",
        "warning2": " ",
        "warning3": " ",
        "warning4": " ",
        "capacity": " ",
        "fsltd_capacity": " ",
        "list": [{
            "tm": "2018-01-09T16:40:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:35:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:30:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:25:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:20:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:15:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:10:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:05:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T16:00:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:55:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:50:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T15:45:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T15:40:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:35:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:30:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:25:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:20:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:15:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T15:10:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T15:05:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T15:00:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:55:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:50:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:45:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:40:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T14:35:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:30:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:25:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:20:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:15:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:10:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T14:05:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T14:00:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T13:55:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T13:50:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:45:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:40:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:35:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:30:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:25:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T13:20:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:15:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:10:00",
            "z": "0.31"
        }, {
            "tm": "2018-01-09T13:05:00",
            "z": "0.32"
        }, {
            "tm": "2018-01-09T13:00:00",
            "z": "0.32"
        }]
    }
}
```