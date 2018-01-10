mapDialogModule模块
===

配置文件readme_chartInfo.json说明
---
| 参数 | 类型 | 说明 |
|---|---|---|
|dataSourcePath|string|数据源|
|<a href="#pathParams">pathparams</a>|Object|数据源参数|
|width|number|弹框宽度|
|height|number|弹框高度|
|type|string|报图类型存在5种,每种对应一个模版的配置文件，当前示例模版为type="iframe"|
|<a href="#iframeSetting">iframeSetting</a>|Object|报图标题配置|


### <a name="pathParams">pathParams</a>
| 参数 | 类型 | 说明 |
|---|---|---|
|任意字符串|string|键值对，key为数据源配置的参数key，<br/>value：<br/> 1、值不存在@符号，表示固定值会直接赋值给参数key（key=value）。<br/>2、值存在@符号，<br/>表示从openOptions.pointData对象中寻找@后面字符串对应的key的值,赋值给参数key(key=openOptions.pointData[value]|


### <a name="iframeSetting">iframeSetting</a>
| 参数 | 类型 | 说明 |
|---|---|---|
|iframePath|string|模版字符串,@{xxx}占位符，xxx为dataSource数据源中的key|
|dataSource|string|数据源,其值有2个分支，<br/>1、openOptions:<br/>表示初始化弹框的参数，template中的模版字符串key会从数据源配置中获取，<br/>例：@{stnm}的值为openOptions.pointData[stnm]<br/>serverData:<br/>表示dataSourcePath接口返回的数据集，返回结果直接挂在serverData下（）。|
