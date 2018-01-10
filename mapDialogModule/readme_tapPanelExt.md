mapDialogModule模块
===

配置文件readme_tapPanelExt.json说明
---
| 参数 | 类型 | 说明 |
|---|---|---|
|dataSourcePath|string|数据源|
|<a href="#pathParams">pathParams</a>|Object|数据源参数|
|width|number|弹框宽度|
|height|number|弹框高度|
|dataAdapter|number|数据适配器，目前仅有objectToArrs_SXJC，后续会扩展添加其他适配器，用于根据规则进行要素匹配|
|type|string|报图类型存在5种,每种对应一个模版的配置文件，当前示例模版为type="tapPanelExt"|
|<a href="#tapExtSetting">tapExtSetting</a>|Array[Object]|面板配置|

### <a name="pathParams">pathParams</a>
| 参数 | 类型 | 说明 |
|---|---|---|
|任意字符串|string|键值对，key为数据源配置的参数key，<br/>value：<br/> 1、值不存在@符号，表示固定值会直接赋值给参数key（key=value）。<br/>2、值存在@符号，<br/>表示从openOptions.pointData对象中寻找@后面字符串对应的key的值,赋值给参数key(key=openOptions.pointData[value]|


### <a name="tapExtSetting">tapExtSetting</a>
| 参数 | 类型 | 说明 |
|---|---|---|
|<a name="dataSource">dataSource</a>|string|数据源,其值有2个分支，<br/>1、openOptions:<br/>表示初始化弹框的参数，template中的模版字符串key会从数据源配置中获取，<br/>例：@{stnm}的值为openOptions.pointData[stnm]<br/>serverData:<br/>表示dataSourcePath接口返回的数据集，返回结果直接挂在serverData下（）。|
|<a href="#typeTapSetting">typeTapSetting</a>|Object|要素配置|
|<a href="#chartTapSetting">chartTapSetting</a>|Object|报图配置|


#### <a name="typeTapSetting">typeTapSetting</a>

| 参数 | 类型 | 说明 |
|---|---|---|
|<a href="base">base</a>|Object|配置|
|<a href="labels">labels</a>|Array[Object]|要素数据源key配置|

##### <a name="base">base</a>

| 参数 | 类型 | 说明 |
|---|---|---|
|lbWidth|string|百分之值， 右上角label页签的宽度占比|
|extendBtn|Object|右上角label页签的内容|
|modal|Object|右上角label点击的弹框样式|
|showLabelCount|number|tap页签数量|

##### <a name="labels">labels</a>

| 参数 | 类型 | 说明 |
|---|---|---|
|key|string|序号|
|label|Object|模块页签名称|
|bindKey|Object|主key字段，需要提取的数据key|
|fchart_bindKey|number|副key字段，需要提取的数据key，支持多个key以“,”隔开|

#### <a name="chartTapSetting">chartTapSetting</a>

| 参数 | 类型 | 说明 |
|---|---|---|
|<a href="#labels">labels</a>当中<a href="#zkey">主key</a>的值|Object|对应主key的报图配置(参照readme_chartInfo.md的配置)|

##### <a name="zkey">主key的值</a>

| 参数 | 类型 | 说明 |
|---|---|---|
|titleSetting|Object|标题配置(参照**readme_chartInfo.md**的**titleSetting**配置)|
|chartSetting|Object|报图配置(参照**readme_chartInfo.md**的**chartSetting**配置)|
|infoSetting|Array[Object]|底部文字配置(参照**readme_chartInfo.md**的**infoSetting**配置)，允许为空|

### 完整配置示例代码
```
{
    "dataSourcePath": "qxjcDialogData",
    "pathParams": {
        "stcd": "@stcd",
		"frequency":"@frequency",
        "time":"@time"
    },
    "width": 660,
    "height": 400,
    "dataAdapter":"objectToArrs_SXJC",
	"type":"tapPanelExt",
    "setting": {
		"dataSource":"serverData.data.list",
		"typeTapSetting":{
			"base":{
				"lbWidth":"20%",
				"extendBtn":{
					"label":"5类要素"
				},
				"modal":{
					"width":320
				},
				"showLabelCount":2
			},
			"labels":[
				{
					"key":"1",
					"label":"气温",
					"bindKey":"temp",
					"fchart_bindKey":"temp_max,temp_min"
				},
				{
					"key":"2",
					"label":"降水",
					"bindKey":"rainfall"
				},
				{
					"key":"3",
					"label":"风向风速",
					"bindKey":"windspeed",
					"fchart_bindKey":"winddir,windspeed_max,winddir_max,windspeed_exmax,winddir_exmax"
				},
				{
					"key":"4",
					"label":"相对湿度",
					"bindKey":"humidity"
				},
				{
					"key":"5",
					"label":"气压",
					"bindKey":"airpressure",
					"fchart_bindKey":"airpressure_max,airpressure_min"
				}
			]
		},
		"chartTapSetting":{
			"temp":{
				"titleSetting":{
                    "template":"@{stnm} 气温 折线图  <br /> @{btime|date(YYYY年MM月DD日HH时)} - @{etime|date(YYYY年MM月DD日HH时)}",
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
                            "name": "气温",
                            "key": "temp",
                            "color": "#4e9f27",
                            "valueType": "monotone",
                            "chartType": "line"
                        },
                        {
                            "name": "最高气温",
                            "key": "temp_max",
                            "color": "#fff000",
                            "valueType": "monotone",
                            "chartType": "line"
                        },
                        {
                            "name": "最低气温",
                            "key": "temp_min",
                            "color": "#00fff0",
                            "valueType": "monotone",
                            "chartType": "line"
                        }
                    ],
                    "xSetting": {
                        "name": "tm",
                        "key": "tm"
                    }
                },
                "infoSetting": []
			},
			"rainfall":{
				"titleSetting":{
                    "template":"@{stnm} 降水 柱状图 <br /> @{btime|date(YYYY年MM月DD日HH时)} - @{etime|date(YYYY年MM月DD日HH时)}",
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
                        "name": "降水",
                        "key": "rainfall",
                        "color": "#70F3FF",
                        "valueType": "monotone",
                        "chartType": "column"
                    }],
                    "xSetting": {
                        "name": "tm",
                        "key": "tm"
                    }
                },
                "infoSetting": []
			},
			"windspeed":{
				"titleSetting":{
                    "template":"@{stnm} 风速风向 折线图  <br /> @{btime|date(YYYY年MM月DD日HH时)} - @{etime|date(YYYY年MM月DD日HH时)}",
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
                            "name": "风向风速",
                            "key": "windspeed",
                            "color": "#4e9f27",
                            "img":{
                                "translatekey":"winddir",
                                "color":"#65a8dd",
                                "path":"M12.5 100 L50 0 L87.5 100 L50 75 Z"
                            },
                            "valueType": "monotone",
                            "chartType": "line"
                        },
                        {
                            "name": "最大风向风速",
                            "key": "windspeed_max",
                            "color": "#fff000",
                            "img":{
                                "translatekey":"winddir_max",
                                "color":"#fff000",
                                "path":"M12.5 100 L50 0 L87.5 100 L50 75 Z"
                            },
                            "valueType": "monotone",
                            "chartType": "line"
                        },
                        {
                            "name": "极大风向风速",
                            "key": "windspeed_exmax",
                            "color": "#00fff0",
                            "img":{
                                "translatekey":"winddir_exmax",
                                "color":"#00fff0",
                                "path":"M12.5 100 L50 0 L87.5 100 L50 75 Z"
                            },
                            "valueType": "monotone",
                            "chartType": "line"
                        }
                    ],
                    "xSetting": {
                        "name": "tm",
                        "key": "tm"
                    }
                },
                "infoSetting": []
			},
			"humidity":{
				"titleSetting":{
                    "template":"@{stnm} 相对湿度 折线图  <br /> @{btime|date(YYYY年MM月DD日HH时)} - @{etime|date(YYYY年MM月DD日HH时)}",
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
                            "name": "相对湿度",
                            "key": "humidity",
                            "color": "#4e9f27",
                            "valueType": "monotone",
                            "chartType": "line"
                        }
                    ],
                    "xSetting": {
                        "name": "tm",
                        "key": "tm"
                    }
                },
                "infoSetting": []
			},
			"airpressure":{
				"titleSetting":{
                    "template":"@{stnm} 气压 折线图  <br /> @{btime|date(YYYY年MM月DD日HH时)} - @{etime|date(YYYY年MM月DD日HH时)}",
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
                    "ySetting": [
                        {
                            "name": "气压",
                            "key": "airpressure",
                            "color": "#4e9f27",
                            "valueType": "monotone",
                            "chartType": "line"
                        },
                        {
                            "name": "最高气压",
                            "key": "airpressure_max",
                            "color": "#fff000",
                            "valueType": "monotone",
                            "chartType": "line"
                        },
                        {
                            "name": "最低气压",
                            "key": "airpressure_min",
                            "color": "#00fff0",
                            "valueType": "monotone",
                            "chartType": "line"
                        }
                    ],
                    "xSetting": {
                        "name": "tm",
                        "key": "tm"
                    }
                },
                "infoSetting": []
			}
		}
	}
}
```

### 接口数据示例
```
{
    "data": {
        "stcd": "56751",
        "stnm": "大理气象站",
        "mnag": "国家地面气象站点",
        "mnfrq": null,
        "stlc": "大理镇",
        "nt": null,
        "list": [{
            "tm": "2018-01-10T10:00:00",
            "temp": 7.7,
            "temp_max": 7.9,
            "temp_min": 0.8,
            "airpressure": 805.3,
            "airpressure_max": 805.3,
            "airpressure_min": 804.6,
            "seapressure": 1019.2,
            "vap": 4.9,
            "windspeed": 0.6,
            "winddir": 337.0,
            "winddir_max": 187.0,
            "winddir_exmax": 294.0,
            "windspeed_max": 0.9,
            "windspeed_exmax": 1.8,
            "rainfall": 0.0,
            "humidity": 47.0,
            "humidity_min": 46.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T09:00:00",
            "temp": 0.8,
            "temp_max": 0.8,
            "temp_min": -1.7,
            "airpressure": 804.6,
            "airpressure_max": 804.6,
            "airpressure_min": 803.6,
            "seapressure": 1020.9,
            "vap": 4.9,
            "windspeed": 0.8,
            "winddir": 185.0,
            "winddir_max": 129.0,
            "winddir_exmax": 124.0,
            "windspeed_max": 1.4,
            "windspeed_exmax": 2.0,
            "rainfall": 0.0,
            "humidity": 76.0,
            "humidity_min": 74.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T08:00:00",
            "temp": -1.5,
            "temp_max": -0.4,
            "temp_min": -1.5,
            "airpressure": 803.6,
            "airpressure_max": 803.6,
            "airpressure_min": 803.0,
            "seapressure": 1020.2,
            "vap": 4.5,
            "windspeed": 1.1,
            "winddir": 263.0,
            "winddir_max": 283.0,
            "winddir_exmax": 276.0,
            "windspeed_max": 1.4,
            "windspeed_exmax": 2.8,
            "rainfall": 0.0,
            "humidity": 83.0,
            "humidity_min": 78.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T07:00:00",
            "temp": -0.5,
            "temp_max": 2.1,
            "temp_min": -0.5,
            "airpressure": 803.0,
            "airpressure_max": 803.0,
            "airpressure_min": 802.3,
            "seapressure": 1019.0,
            "vap": 4.6,
            "windspeed": 0.4,
            "winddir": 155.0,
            "winddir_max": 320.0,
            "winddir_exmax": 145.0,
            "windspeed_max": 1.3,
            "windspeed_exmax": 2.1,
            "rainfall": 0.0,
            "humidity": 78.0,
            "humidity_min": 65.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T06:00:00",
            "temp": 2.2,
            "temp_max": 2.7,
            "temp_min": 1.3,
            "airpressure": 802.3,
            "airpressure_max": 802.3,
            "airpressure_min": 801.8,
            "seapressure": 1016.4,
            "vap": 4.6,
            "windspeed": 1.3,
            "winddir": 320.0,
            "winddir_max": 318.0,
            "winddir_exmax": 321.0,
            "windspeed_max": 2.8,
            "windspeed_exmax": 3.5,
            "rainfall": 0.0,
            "humidity": 64.0,
            "humidity_min": 57.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T05:00:00",
            "temp": 1.6,
            "temp_max": 4.0,
            "temp_min": 1.6,
            "airpressure": 801.8,
            "airpressure_max": 801.9,
            "airpressure_min": 801.6,
            "seapressure": 1015.2,
            "vap": 4.5,
            "windspeed": 1.3,
            "winddir": 263.0,
            "winddir_max": 234.0,
            "winddir_exmax": 238.0,
            "windspeed_max": 1.9,
            "windspeed_exmax": 3.2,
            "rainfall": 0.0,
            "humidity": 65.0,
            "humidity_min": 50.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T04:00:00",
            "temp": 3.6,
            "temp_max": 4.3,
            "temp_min": 3.0,
            "airpressure": 801.7,
            "airpressure_max": 801.8,
            "airpressure_min": 801.5,
            "seapressure": 1013.6,
            "vap": 4.4,
            "windspeed": 1.5,
            "winddir": 205.0,
            "winddir_max": 286.0,
            "winddir_exmax": 296.0,
            "windspeed_max": 2.1,
            "windspeed_exmax": 3.5,
            "rainfall": 0.0,
            "humidity": 56.0,
            "humidity_min": 51.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T03:00:00",
            "temp": 4.0,
            "temp_max": 5.4,
            "temp_min": 3.5,
            "airpressure": 801.6,
            "airpressure_max": 801.6,
            "airpressure_min": 801.1,
            "seapressure": 1013.7,
            "vap": 4.2,
            "windspeed": 1.9,
            "winddir": 288.0,
            "winddir_max": 323.0,
            "winddir_exmax": 318.0,
            "windspeed_max": 2.2,
            "windspeed_exmax": 4.3,
            "rainfall": 0.0,
            "humidity": 52.0,
            "humidity_min": 45.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T02:00:00",
            "temp": 4.6,
            "temp_max": 6.8,
            "temp_min": 4.2,
            "airpressure": 801.2,
            "airpressure_max": 801.2,
            "airpressure_min": 800.9,
            "seapressure": 1013.7,
            "vap": 4.5,
            "windspeed": 2.2,
            "winddir": 233.0,
            "winddir_max": 233.0,
            "winddir_exmax": 257.0,
            "windspeed_max": 2.2,
            "windspeed_exmax": 4.6,
            "rainfall": 0.0,
            "humidity": 53.0,
            "humidity_min": 42.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T01:00:00",
            "temp": 7.0,
            "temp_max": 10.0,
            "temp_min": 7.0,
            "airpressure": 801.1,
            "airpressure_max": 801.3,
            "airpressure_min": 800.6,
            "seapressure": 1013.1,
            "vap": 4.1,
            "windspeed": 1.0,
            "winddir": 216.0,
            "winddir_max": 157.0,
            "winddir_exmax": 171.0,
            "windspeed_max": 6.0,
            "windspeed_exmax": 9.6,
            "rainfall": 0.0,
            "humidity": 41.0,
            "humidity_min": 31.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-10T00:00:00",
            "temp": 10.0,
            "temp_max": 10.3,
            "temp_min": 9.8,
            "airpressure": 800.6,
            "airpressure_max": 801.0,
            "airpressure_min": 800.6,
            "seapressure": 1011.5,
            "vap": 3.7,
            "windspeed": 5.8,
            "winddir": 167.0,
            "winddir_max": 160.0,
            "winddir_exmax": 164.0,
            "windspeed_max": 7.0,
            "windspeed_exmax": 14.1,
            "rainfall": 0.0,
            "humidity": 30.0,
            "humidity_min": 30.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T23:00:00",
            "temp": 10.1,
            "temp_max": 10.4,
            "temp_min": 9.9,
            "airpressure": 800.8,
            "airpressure_max": 801.0,
            "airpressure_min": 800.6,
            "seapressure": 1012.1,
            "vap": 3.8,
            "windspeed": 5.8,
            "winddir": 159.0,
            "winddir_max": 158.0,
            "winddir_exmax": 161.0,
            "windspeed_max": 6.6,
            "windspeed_exmax": 13.4,
            "rainfall": 0.0,
            "humidity": 31.0,
            "humidity_min": 31.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T22:00:00",
            "temp": 10.3,
            "temp_max": 11.1,
            "temp_min": 10.3,
            "airpressure": 800.7,
            "airpressure_max": 801.1,
            "airpressure_min": 800.3,
            "seapressure": 1012.6,
            "vap": 4.0,
            "windspeed": 3.2,
            "winddir": 161.0,
            "winddir_max": 160.0,
            "winddir_exmax": 161.0,
            "windspeed_max": 5.3,
            "windspeed_exmax": 10.5,
            "rainfall": 0.0,
            "humidity": 32.0,
            "humidity_min": 29.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T21:00:00",
            "temp": 11.1,
            "temp_max": 12.2,
            "temp_min": 11.1,
            "airpressure": 800.3,
            "airpressure_max": 800.3,
            "airpressure_min": 799.3,
            "seapressure": 1013.7,
            "vap": 3.8,
            "windspeed": 5.2,
            "winddir": 155.0,
            "winddir_max": 157.0,
            "winddir_exmax": 166.0,
            "windspeed_max": 7.6,
            "windspeed_exmax": 11.8,
            "rainfall": 0.0,
            "humidity": 29.0,
            "humidity_min": 26.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T20:00:00",
            "temp": 12.1,
            "temp_max": 12.6,
            "temp_min": 12.1,
            "airpressure": 799.2,
            "airpressure_max": 799.4,
            "airpressure_min": 798.8,
            "seapressure": 1011.6,
            "vap": 3.8,
            "windspeed": 6.9,
            "winddir": 151.0,
            "winddir_max": 149.0,
            "winddir_exmax": 135.0,
            "windspeed_max": 9.4,
            "windspeed_exmax": 14.8,
            "rainfall": 0.0,
            "humidity": 27.0,
            "humidity_min": 25.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T19:00:00",
            "temp": 12.3,
            "temp_max": 13.5,
            "temp_min": 12.3,
            "airpressure": 799.2,
            "airpressure_max": 799.3,
            "airpressure_min": 797.8,
            "seapressure": 1011.2,
            "vap": 4.4,
            "windspeed": 7.7,
            "winddir": 140.0,
            "winddir_max": 137.0,
            "winddir_exmax": 137.0,
            "windspeed_max": 9.6,
            "windspeed_exmax": 17.0,
            "rainfall": 0.0,
            "humidity": 31.0,
            "humidity_min": 27.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T18:00:00",
            "temp": 13.5,
            "temp_max": 16.1,
            "temp_min": 13.5,
            "airpressure": 798.8,
            "airpressure_max": 799.1,
            "airpressure_min": 798.0,
            "seapressure": 1009.9,
            "vap": 4.6,
            "windspeed": 7.0,
            "winddir": 147.0,
            "winddir_max": 151.0,
            "winddir_exmax": 170.0,
            "windspeed_max": 8.7,
            "windspeed_exmax": 17.4,
            "rainfall": 0.0,
            "humidity": 30.0,
            "humidity_min": 17.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T17:00:00",
            "temp": 15.6,
            "temp_max": 17.6,
            "temp_min": 15.4,
            "airpressure": 799.1,
            "airpressure_max": 799.1,
            "airpressure_min": 797.9,
            "seapressure": 1009.1,
            "vap": 4.6,
            "windspeed": 6.2,
            "winddir": 142.0,
            "winddir_max": 132.0,
            "winddir_exmax": 112.0,
            "windspeed_max": 8.5,
            "windspeed_exmax": 16.0,
            "rainfall": 0.0,
            "humidity": 26.0,
            "humidity_min": 14.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T16:00:00",
            "temp": 17.0,
            "temp_max": 17.0,
            "temp_min": 15.8,
            "airpressure": 798.3,
            "airpressure_max": 799.5,
            "airpressure_min": 798.3,
            "seapressure": 1007.3,
            "vap": 3.7,
            "windspeed": 2.8,
            "winddir": 294.0,
            "winddir_max": 152.0,
            "winddir_exmax": 140.0,
            "windspeed_max": 6.9,
            "windspeed_exmax": 13.7,
            "rainfall": 0.0,
            "humidity": 19.0,
            "humidity_min": 14.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T15:00:00",
            "temp": 16.2,
            "temp_max": 16.2,
            "temp_min": 14.2,
            "airpressure": 799.6,
            "airpressure_max": 800.7,
            "airpressure_min": 799.5,
            "seapressure": 1009.2,
            "vap": 3.9,
            "windspeed": 3.2,
            "winddir": 116.0,
            "winddir_max": 130.0,
            "winddir_exmax": 112.0,
            "windspeed_max": 4.2,
            "windspeed_exmax": 8.5,
            "rainfall": 0.0,
            "humidity": 21.0,
            "humidity_min": 18.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T14:00:00",
            "temp": 14.2,
            "temp_max": 14.2,
            "temp_min": 13.0,
            "airpressure": 800.7,
            "airpressure_max": 801.8,
            "airpressure_min": 800.7,
            "seapressure": 1011.0,
            "vap": 5.2,
            "windspeed": 1.4,
            "winddir": 62.0,
            "winddir_max": 91.0,
            "winddir_exmax": 104.0,
            "windspeed_max": 2.8,
            "windspeed_exmax": 4.6,
            "rainfall": 0.0,
            "humidity": 32.0,
            "humidity_min": 31.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T13:00:00",
            "temp": 13.1,
            "temp_max": 13.3,
            "temp_min": 12.3,
            "airpressure": 801.8,
            "airpressure_max": 803.0,
            "airpressure_min": 801.8,
            "seapressure": 1013.0,
            "vap": 5.3,
            "windspeed": 2.6,
            "winddir": 86.0,
            "winddir_max": 106.0,
            "winddir_exmax": 81.0,
            "windspeed_max": 2.7,
            "windspeed_exmax": 5.0,
            "rainfall": 0.0,
            "humidity": 35.0,
            "humidity_min": 33.0,
            "totalradiation": null
        }, {
            "tm": "2018-01-09T12:00:00",
            "temp": 12.3,
            "temp_max": 12.4,
            "temp_min": 11.3,
            "airpressure": 802.9,
            "airpressure_max": 803.6,
            "airpressure_min": 802.9,
            "seapressure": 1014.5,
            "vap": 4.9,
            "windspeed": 2.2,
            "winddir": 91.0,
            "winddir_max": 78.0,
            "winddir_exmax": 66.0,
            "windspeed_max": 2.5,
            "windspeed_exmax": 4.4,
            "rainfall": 0.0,
            "humidity": 34.0,
            "humidity_min": 33.0,
            "totalradiation": null
        }]
    }
}
```
