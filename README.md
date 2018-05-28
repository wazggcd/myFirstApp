# 拓扑图配置
## 配置总图
- 例子
``` js
{
    "nodes":[
        { "data": { "id": "y1", "name": "应用1", "type": "a", "icon": "app" } },
        { "data": { "id": "y2", "name": "应用2", "type": "a", "icon": "app" } },
        { "data": { "id": "s1", "name": "服务1", "type": "s", "icon": "tomcat" } },
        { "data": { "id": "s2", "name": "服务2", "type": "s", "icon": "mysql" } },
        { "data": { "id": "s3", "name": "服务3", "type": "s", "icon": "redis" } },
        { "data": { "id": "s4", "name": "服务4", "type": "s", "icon": "java" } },
        { "data": { "id": "c1", "name": "容器1", "type": "c", "icon": "zookeeper" } },
        { "data": { "id": "c2", "name": "容器2", "type": "c", "icon": "nginx" } },
        { "data": { "id": "c3", "name": "容器3", "type": "c", "icon": "tensorflow" } },
        { "data": { "id": "c4", "name": "容器4", "type": "c", "icon": "tensorflow" } },
        { "data": { "id": "c5", "name": "容器5", "type": "c", "icon": "redis" } },
        { "data": { "id": "c6", "name": "容器6", "type": "c", "icon": "java" } }
    ],
    "edges":[
        { "data": { "source": "y1", "target": "s1", "lineColor": "#f00"} },
        { "data": { "source": "y1", "target": "s3", "lineColor": "#00a200" } },
        { "data": { "source": "y2", "target": "s2", "lineColor": "#00a200" } },
        { "data": { "source": "y2", "target": "s1", "lineColor": "#f00"} },
        { "data": { "source": "s1", "target": "c1", "lineColor": "#00a200" } },
        { "data": { "source": "s1", "target": "c2", "lineColor": "#00a200" } },
        { "data": { "source": "s2", "target": "c3", "lineColor": "#f00"} },
        { "data": { "source": "s3", "target": "c4", "lineColor": "#00a200" } },
        { "data": { "source": "s4", "target": "c5", "lineColor": "#00a200" } },
        { "data": { "source": "s4", "target": "c6", "lineColor": "#00a200" } }
    ]
}
```

- 字段解释
    - 每个json对象由 nodes(节点) 和edges(连线)两个字段组成
    - nodes表示节点 值为数组, 每个数组元素为一个对象:
    ``` js
    {
      "data":{
        "id":"y1", //节点id, 保证唯一性, 不能重复
        "name":"应用1", // 节点名称, 可以为任意字符串, 显示在节点图标的下方
        "type":"a", // 节点类型, 可取值有: 应用'a', 服务's', 容器'c'
        "icon":"app" // 图标类型, 可取值有: 'tomcat', 'java', 'tensorflow', 'mysql', 'redis', 'zookeeper', 'nginx', 'app'
      }
    },
    ```
    - edges表示连线, 值为数组, 每个数组元素为一个对象:
    ``` js
    {
      "data":{
        "source":"s1", // 连线起始节点的id
        "target":"c1", // 连接目标节点的id
        "lineColor":"#00a200" // 连线颜色, 可取值:绿色'#00a200', 红色'#f00', 白色'#fff'
    }
    ```
- 注意事项
    - 为保证'应用节点'(节点type为'a')处于第一行, 其他类型的节点*不能*指向应用节点
    - 为保证'容器节点'(节点type为'c')处于第三行, 容器节点*不能*指向其他节点, 必须有一个'服务节点'(节点type为's')指向容器节点


## 配置子图
- 例子
``` js
{
    "nodes":[
        { "data": { "id": "y1", "name": "应用1", "type": "a", "icon": "app" } },
        { "data": { "id": "s1", "name": "服务1", "type": "s", "icon": "tomcat" } },
        { "data": { "id": "s2", "name": "服务2", "type": "s", "icon": "mysql" } },
        { "data": { "id": "s3", "name": "服务3", "type": "s", "icon": "redis" } },
        { "data": { "id": "s4", "name": "服务4", "type": "s", "icon": "java" } },
        { "data": { "id": "c1", "name": "容器1", "type": "c", "icon": "zookeeper" } },
        { "data": { "id": "c2", "name": "容器2", "type": "c", "icon": "nginx" } },
        { "data": { "id": "c3", "name": "容器3", "type": "c", "icon": "tensorflow" } },
        { "data": { "id": "c4", "name": "容器4", "type": "c", "icon": "tensorflow" } },
        { "data": { "id": "c5", "name": "容器5", "type": "c", "icon": "redis" } },
        { "data": { "id": "c6", "name": "容器6", "type": "c", "icon": "java" } }
    ],
    "edges":[
        { "data": { "source": "y1", "target": "s1", "lineColor": "#fff"} },
        { "data": { "source": "y1", "target": "s1", "lineColor": "#fff"} },
        { "data": { "source": "y1", "target": "s3", "lineColor": "#fff"} },
        { "data": { "source": "y1", "target": "s4", "lineColor": "#fff"} },
        { "data": { "source": "s4", "target": "s3", "lineColor": "#00a200"} },
        { "data": { "source": "s1", "target": "s2", "lineColor": "#00a200" } },
        { "data": { "source": "s2", "target": "s3", "lineColor": "#f00" } },
        { "data": { "source": "s3", "target": "s4", "lineColor": "#f00"} },
        { "data": { "source": "s1", "target": "c1", "lineColor": "#00a200" } },
        { "data": { "source": "s1", "target": "c2", "lineColor": "#f00" } },
        { "data": { "source": "s2", "target": "c3", "lineColor": "#f00"} },
        { "data": { "source": "s3", "target": "c4", "lineColor": "#00a200" } },
        { "data": { "source": "s4", "target": "c5", "lineColor": "#00a200" } },
        { "data": { "source": "s4", "target": "c6", "lineColor": "#00a200" } }
    ]
}
```

- 字段解释
    - 总体跟总图字段差不多, 请参与总图的说明

- 注意事项
    - '应用节点'(节点type为'a')*有且只能*有一个
    - '应用节点'需要指向*每一个*'服务节点', 且设置线的颜色为白色'#fff'
    - 为保证'应用节点'(节点type为'a')处于第一行, 其他类型的节点*不能*指向应用节点
    - 为保证'容器节点'(节点type为'c')处于第三行, 容器节点*不能*指向其他节点, 必须有一个'服务节点'(节点type为's')指向容器节点
