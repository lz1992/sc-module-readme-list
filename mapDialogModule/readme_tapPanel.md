mapDialogModule模块
===

配置文件readme_tapPanel.json说明
---
| 参数 | 类型 | 说明 |
|---|---|---|
|dataSourcePath|string|数据源|
|[pathParams](#pathparams)|Object|数据源参数|
|width|number|弹框宽度|
|type|string|报图类型存在5种,每种对应一个模版的配置文件，当前示例模版为type="tapPanel"|
|[tapSetting](#tapsetting)|Array[Object]|面板配置|

### <span id="pathParams">pathParams</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|任意字符串|string|键值对，key为数据源配置的参数key，<br/>value：<br/> 1、值不存在@符号，表示固定值会直接赋值给参数key（key=value）。<br/>2、值存在@符号，<br/>表示从openOptions.pointData对象中寻找@后面字符串对应的key的值,赋值给参数key(key=openOptions.pointData[value]|

### <span id="tapSetting">tapSetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|<span id="dataSource">dataSource</span>|string|数据源,其值有2个分支，<br/>1、openOptions:<br/>表示初始化弹框的参数，template中的模版字符串key会从数据源配置中获取，<br/>例：@{stnm}的值为openOptions.pointData[stnm]<br/>serverData:<br/>表示dataSourcePath接口返回的数据集，返回结果直接挂在serverData下（）。|
|title|string|标题|
|type|string|类型，目前仅支持表格类型布局，后续扩展报图效果|
|fontsize|string|字体大小|
|[trs](#trs)|Array[Object]|表格的行对象|
|width|string|面板宽度|
|height|string|面板高度|

#### <span id="trs">trs</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|[tds](#tds)|Array[Object]|表格列对象|

##### <span id="tds">tds</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|rowSpan|string|表格tr的属性|
|colSpan|string|表格td属性|
|name|string|中文名值，固定值|
|key|string|[dataSource](#datasource)中的key所对应的值，动态变量|
|template|string|模版字符串`${name}${val}`，`${name}`对应取前面name的值，`${val}`为key转换后的值，可以添加其他任意字符串，|
|style|Object|jsx的样式|

### 完整配置代码
```
{
    "dataSourcePath": "kzDialogData",
    "pathParams": {
        "stcd":"@stcd"
    },
    "width": 650,
    "tapTitlHide":false,
    "type": "tapPanel",
    "tapSetting": [
        {
            "title": "基本信息",
            "dataSource": "serverData.data",
            "type": "table",
            "fontsize":"13px",
            "trs": [ {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "客栈名称",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                            "paddingLeft":8,   
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "name"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "经营者",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                              "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "operators"
                    }
                    
                    
                ]
            }, {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "经营者身份证号",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                            "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "idcard"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "电话",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,   
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "template":"${name}${val}",
                        "name": "",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "phone"
                    }
                ]
            },  {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "开业时间",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                              "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "opentime"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "经营地址",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "address"
                    }
                ]
            }, {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "房东姓名",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "landlord"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "房东联系电话",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "landlordphone"
                    }
                ]
            },  {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "经营建筑面积(㎡)",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                            "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "jyjzmz"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "月应交纳相关税收(元)",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "yyjnxgss"
                    }
                ]
            },  {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "经度",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                            "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "lng"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "纬度",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "lat"
                    }
                ]
            }],
            "width": 660,
            "height": 350
        },
        {
            "title": "证件信息",
            "dataSource": "serverData.data",
            "type": "table",
            "fontsize":"13px",
            "trs": [ {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "土地权属证明",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                            "paddingLeft":8,   
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "tdqszm"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "国土证明",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                              "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "gtzm"
                    }
                    
                    
                ]
            }, {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "规划建设许可证",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                            "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "ghjsxkz"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "营业执照",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,   
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "template":"${name}${val}",
                        "name": "",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "yyzz"
                    }
                ]
            },  {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "食品经营许可证",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                              "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                             "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "spjyxkz"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "卫生许可证",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "wsxkz"
                    }
                ]
            }, {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "文化经营许可证",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "whjyxkz"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "税务执照",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "swzz"
                    }
                ]
            },  {
                "tds":[
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "消防安全检查合格证",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                            "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "xfaqjchgz"
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "金硅系统",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":14,
                            "padding":"5px 5px",
                             "paddingLeft":8,  
                            "textAlign":"right",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": ""
                    },
                    {
                        "rowSpan":"",
                        "colSpan":0,
                        "name": "",
                        "template":"${name}${val}",
                        "style":{
                            "fontSize":12,
                            "padding":"5px 15px",
                            "color":"#fff",
                            "textAlign":"center",
                            "backgroundColor":"rgba(96, 114, 136, .7)",
                            "border": "1px solid rgba(96, 114, 136, .8)",                             "paddingRight": "10px"
                        },
                        "key": "jgxt"
                    }
                ]
            }],
            "width": 660,
            "height": 350
        }
    ]
}
```


### 完整接口数据结构
```
{
    "data": {
        "id": 11247.0,
        "name": "利丰饭店",
        "village": "满江村委会",
        "operators": "杨玉芬",
        "idcard": "532901197603081421",
        "phone": "15125240804",
        "opentime": null,
        "address": "满江五社",
        "landlord": null,
        "landlordphone": null,
        "tdqszm": null,
        "jyjzmz": "100",
        "yyjnxgss": null,
        "gtzm": null,
        "ghjsxkz": null,
        "pwxkz": null,
        "yyzz": null,
        "spjyxkz": null,
        "jgxt": null,
        "wsxkz": null,
        "whjyxkz": null,
        "swzz": null,
        "xfaqjchgz": null,
        "czs": 0.0,
        "lng": 100.271111,
        "lat": 25.613889,
        "addvcd": "532901002                     ",
        "idno": "532901002",
        "areaname": "大理创新工业园区满江办事处"
    }
}
```