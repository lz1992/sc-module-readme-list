mapRightModule 模块 
===

mapRightSetting.jon说明
---

| 参数 | 类型 | 说明 |
|---|---|---|
|key|string|唯一标识 与mapLeftModule中的模块key对应|
|name|string|业务模块名称|
|icon|string|右侧面板tap页签的图标路径|
|iconType|string|Tap页签图标类型（目前仅img，暂不支持其他）|
|height|string|高度|
|sourcePath|string|右侧面板的数据源key 与config/urlHelper.js中的配置对应|
|[defalutPathParams](#defalutPathParams)|Object|绑定到接口上的参数配置|
|[panelSearchSetting](#panelSearchSetting)|Object|搜索栏配置|
|[panelBodySetting](#panelBodySetting)|Object|列表内容配置|

### <span id="defalutPathParams">defalutPathParams</span>

| 参数 | 类型 | 说明 |
|---|---|---|
|任意key|string或Array|当值为 **string**类型时：<br/>例1 "sttps":"PP"， 其key为sttps，值为PP。<br/> 例2 "depid":"@gldw"，其key为depid,值为在**搜索条件**中key为gldw的值。<br /> <br />当值为**Array**类型时表示获取的参数是时间类型的值：<br/>其获取时间参数的格式为<br/>`[{"value":"@btime","index":-1,"format":"YYYY-MM-DDTHH:mm:ss"},{"value":"@etime","index":-1,"format":"YYYY-MM-DDTHH:mm:ss"}]`<br/> 带 @ 值参数同 **string例2**中的一致  |

### 2、 <span id="panelSearchSetting">panelSearchSetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|title|string|标题|
|[setting[]](#panelSearchSetting-setting)|Array[Object] |搜索条件配置|

#### 代码片段：
```
"defalutPathParams":{
            "time":[
                {
                    "value":"@btime",
                    "index":-1,
                    "format":"YYYY-MM-DDTHH:mm:ss"
                },{
                    "value":"@etime",
                    "index":-1,
                    "format":"YYYY-MM-DDTHH:mm:ss"
                }
            ],
            "sttps":"PP",
            "depid":"@gldw",
            "search_stnm":"@search_stnm"
        }
```

#### 2.1、<span id="panelSearchSetting-setting">setting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|name|string|控件前缀的名称|
|type|string|控件类型：<br/> **date**（日期控件）：<br/>配套的**defatulValue**参数为对象<br/>`{"value":"now", "pfTime":0,"format":"YYYY-MM-DD HH:mm:ss"      } value为now表示当前时间，pfTime表示往前推几个小时，format为日期格式化`<br/>**select**（下拉框控件）：<br/> 配套的defatulValue参数为字符串<br/> defatulValue:"xx", xx为children中的value值<br/>**text**（文本输入控件）：无需默认值<br/>**checkbox**（多选框控件）：<br/> 配套的defatulValue参数为数组，其值为children中的value<br/>**radio**（单选框控件）：<br/>配套的defatulValue参数为字符串 <br/> defatulValue:"xx", xx为children中的value值|
|key|string|唯一标识|
|width|number|控件宽度|
|rule|string|雨情使用 针对时间控件的规则设置|
|defatulValue|string或Array或Object|默认参数|
|children[]|Array[Object]|数据集 <br/> 其数据结构为`[{"label":"全部","value":""}]`|
|serverData|Object|下拉框的数据源，结果会合并到children中  仅当**type**为**select**时有效， 数据结构为<br/>`{"path":"gldw_search_type","value":"depid","name":"dname"}` <br/>path的值为数据源地址的key<br/>value的值为数据接口**返回的数据**中的key，匹配**children**中的**value**。<br/>name的值为数据接口**返回的数据**中的key，匹配**children**中的**label**。|
|serverDataParams|Object|下拉框的数据源参数 仅当**type**为**select**时有效 对象结构`{"type":"yl"}` type为key，yl为值，不支持动态值|
#### 代码片段：
```
"panelSearchSetting":{
            "title":"条件选择",
            "setUpState":true,
            "setting":[
                {
                    "name":"&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;从",
                    "type":"date",
                    "key":"btime",
                    "rule":true,
                    "defatulValue":{
                        "value":"now",
                        "pfTime":0,
                        "format":"YYYY-MM-DD HH:mm:ss"                 
                    }
                },
                {
                    "name":"&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;到",
                    "type":"date",
                    "key":"etime",
                    "defatulValue":{
                        "value":"now",
                        "pfTime":0,
                        "format":"YYYY-MM-DD HH:mm:ss"                
                    }
                },
                {
                    "placeholder":"",
                    "children":[
                        {"label":"全部","value":""}
                    ],
                    "name":"管理单位",
                    "width":155,
                    "defatulValue":"",
                    "serverData":{
                        "path":"gldw_search_type",
                        "value":"depid",
                        "name":"dname"
                    },
                    "serverDataParams":{
                        "type":"yl"
                    },
                    "type":"select",
                    "key":"gldw"
                },
                {
                    "name":"站点名称",
                    "type":"text",
                    "width":155,
                    "key":"search_stnm"
                },			
                {
                    "name":"雨量范围",  //雨情特殊配置
                    "title":"雨量范围（单位:mm）",
                    "filter":{
                        "state":true,
                        "bindKey":"levelidx"
                        },
                    "children":[
                        { "label": "空", "value": "-1", "img":"./assets/MapRightSearch/圆点1.png","col":"6"},
                        { "label": "0", "value": "0", "img":"./assets/MapRightSearch/圆点2.png","col":"6" },
                        { "label": "10", "value": "1", "img":"./assets/MapRightSearch/圆点3.png","col":"6" },
                        { "label": "25", "value": "2", "img":"./assets/MapRightSearch/圆点4.png","col":"6" },
                        { "label": "50", "value": "3", "img":"./assets/MapRightSearch/圆点5.png","col":"6" },
                        { "label": "100", "value": "4", "img":"./assets/MapRightSearch/圆点6.png" ,"col":"6"},
                        { "label": "250", "value": "5", "img":"./assets/MapRightSearch/圆点7.png","col":"6" },
                        { "label": "250+", "value": "6", "img":"./assets/MapRightSearch/圆点8.png","col":"6" }
                    ],
                    "defatulValue":["-1","0","1","2","3","4","5","6"],
                    "type":"checkbox",
                    "key":"otype"
                },
                {
                    "name":"站点类型",                  
                    "children":[
                        { "label": "人工站", "value": "0", "col":"12"},
                        { "label": "自动站", "value": "1", "col":"12" }
                    ],
                    "defatulValue":["1"],
                    "width":200,
                    "type":"checkbox",
                    "key":"stnm_type"
                }
            ]
        }
```


### 3、 <span id="panelBodySetting">panelBodySetting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|title|string|标题|
|row_key|string|数据的唯一标识列，|
|width|string|表格宽度|
|[setting[]](#panelBodySetting-setting)|Array[Object] |列表配置|


#### 3.1、<span id="panelBodySetting-setting">setting</span>
| 参数 | 类型 | 说明 |
|---|---|---|
|title|string|标题|
|dataIndex|string|绑定数据的key|
|sorter_type|string|排序类型  若不设置则不排序，目前支持**number**和**string** 2种类型的排序|
|className|string|列样式类名|
|width|number|列宽|

#### 代码片段：
```
[
    {
        "key":"rain",      
        "name":"雨量监测",
        "icon":"./assets/MapLeftMenu/left_icon-5.png",
        "iconType":"img",
        "height":"500",
        "sourcePath":"rainData",
        "defalutPathParams":{
            "time":[
                {
                    "value":"@btime",
                    "index":-1,
                    "format":"YYYY-MM-DDTHH:mm:ss"
                },{
                    "value":"@etime",
                    "index":-1,
                    "format":"YYYY-MM-DDTHH:mm:ss"
                }
            ],
            "sttps":"PP",
            "depid":"@gldw",
            "search_stnm":"@search_stnm"
        },
        "panelSearchSetting":{
            "title":"条件选择",
            "setUpState":true,
            "setting":[
                {
                    "name":"&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;从",
                    "type":"date",
                    "key":"btime",
                    "rule":true,
                    "defatulValue":{
                        "value":"now",
                        "pfTime":0,
                        "format":"YYYY-MM-DD HH:mm:ss"                 
                    }
                },
                {
                    "name":"&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;到",
                    "type":"date",
                    "key":"etime",
                    "defatulValue":{
                        "value":"now",
                        "pfTime":0,
                        "format":"YYYY-MM-DD HH:mm:ss"                
                    }
                },
                {
                    "placeholder":"",
                    "children":[
                        {"label":"全部","value":""}
                    ],
                    "name":"管理单位",
                    "width":155,
                    "defatulValue":"",
                    "serverData":{
                        "path":"gldw_search_type",
                        "value":"depid",
                        "name":"dname"
                    },
                    "serverDataParams":{
                        "type":"yl"
                    },
                    "type":"select",
                    "key":"gldw"
                },
                {
                    "name":"站点名称",
                    "type":"text",
                    "width":155,
                    "key":"search_stnm"
                },			
                {
                    "name":"雨量范围",
                    "title":"雨量范围（单位:mm）",
                    "filter":{
                        "state":true,
                        "bindKey":"levelidx"
                        },
                    "children":[
                        { "label": "空", "value": "-1", "img":"./assets/MapRightSearch/圆点1.png","col":"6"},
                        { "label": "0", "value": "0", "img":"./assets/MapRightSearch/圆点2.png","col":"6" },
                        { "label": "10", "value": "1", "img":"./assets/MapRightSearch/圆点3.png","col":"6" },
                        { "label": "25", "value": "2", "img":"./assets/MapRightSearch/圆点4.png","col":"6" },
                        { "label": "50", "value": "3", "img":"./assets/MapRightSearch/圆点5.png","col":"6" },
                        { "label": "100", "value": "4", "img":"./assets/MapRightSearch/圆点6.png" ,"col":"6"},
                        { "label": "250", "value": "5", "img":"./assets/MapRightSearch/圆点7.png","col":"6" },
                        { "label": "250+", "value": "6", "img":"./assets/MapRightSearch/圆点8.png","col":"6" }
                    ],
                    "defatulValue":["-1","0","1","2","3","4","5","6"],
                    "type":"checkbox",
                    "key":"otype"
                },
                {
                    "name":"站点类型",                  
                    "children":[
                        { "label": "人工站", "value": "0", "col":"12"},
                        { "label": "自动站", "value": "1", "col":"12" }
                    ],
                    "defatulValue":["1"],
                    "width":200,
                    "type":"checkbox",
                    "key":"stnm_type"
                }
            ]
        },
        "panelBodySetting":{
            "title":"雨量信息（单位:mm）",
            "row_key":"t_number",
            "setting":[
                {
                    "title":"序号",
                    "dataIndex": "t_number",
                    "sorter_type":"number",
                    "className":"t_number",
                    "width":60
                },
                 {
                    "title": "站点名称",
                    "dataIndex": "stnm",
                    "sorter_type":"string",
                    "className":"center",
                    "width": 150
                },{
                    "title": "雨量",
                    "dataIndex": "precipitation",
                    "sorter_type":"number",
                    "className":"right"
                }

            ]
        }
    },
]
```
