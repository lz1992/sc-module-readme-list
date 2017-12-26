mapLeftModule 模块 
===

配置文件mapLeftMenuSetting.jon说明
---

| 参数 | 类型 | 说明 |
|---|---|---|
|key|string|唯一标识|
|name|string|菜单名称|
|icon|string|菜单小图片的路径|
|iconType|string|小图片类型|
|iconStyle|Object|小图片的样式 遵循jsx的style对象|
|open|bool|是否展开菜单|
|[children[]](#children)|Array Object|子菜单集合|


### <span id="children">children</span> 

| 参数 | 类型 | 说明 |
|---|---|---|
|key|string|唯一标识|
|name|string|菜单名称|
|icon|string|菜单小图片的路径|
|iconType|string|小图片类型|
|iconStyle|Object|小图片的样式 遵循jsx的style对象|
|checked|bool|菜单是否选中|


#### 代码片段：
```
[
    {
        "key": "basic_information",
        "name": "在线监测",
        "icon": "./assets/MapLeftMenu/left_icon-1.png",
        "iconType":"img",
        "iconStyle":{
            "width":24,
            "height":24,
            "top":4
        },
        "open":true,
        "children": [{
                "key": "szjc",
                "name": "水质监测",
                "checked": true,
                "iconStyle":{
                    "width":22,
                    "height":22,
                    "top":6
                },
                "icon": "./assets/MapLeftMenu/left_icon-2.png",
                "iconType":"img"
            },
            {
                "key": "wrljc",
                "name": "污染源监测",
                "iconStyle":{
                    "width":22,
                    "height":22,
                    "top":6
                },
                "liType":"not_add",
                "icon": "./assets/MapLeftMenu/left_icon-3.png",
                "iconType":"img"
            },
            {
                "key": "water",
                "name": "水位监测",
                "checked": false,
                "iconStyle":{
                    "width":22,
                    "height":22,
                    "top":6
                },
                "liType":"dialog",
                "icon": "./assets/MapLeftMenu/left_icon-4.png",
                "iconType":"img"
            }
        ]
    }  
]
```