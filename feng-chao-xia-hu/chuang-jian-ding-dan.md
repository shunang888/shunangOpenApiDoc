# 创建订单

> 1 获取token [获取token](/feng-chao-xia-hu-api/huo-qu-token.md)

> 2 参数数说明:

名称 | 类型 |为空| 说明
:- | :-: | :-:| :-
reserveDate|date|false | 下户预约时间
community|String|false|小区名称
province|String|false|省份
city|String|false|城市
county|String|false|区县
address|String|false|地址
modelType|Long|false|模板类型 为客户提供的动态模板表示 下户系统配置后给予（否则为标准模板）
longitude|String|false|经度 为百度地图地址坐标解析 为了实地人员的准确性下单尽量使用地图选点
latitude|String|false|纬度 同上



- 示例-创建订单：

 - 1.1. HTTP示例

 - 1.2. curl示例

 - 1.3. 消息体中的JSON字段说明

##### HTTP示例
```
POST /receiveMsg.action HTTP/1.1
Host: ixiahu.com
Content-Type: application/json

{"reserveDate":"2018-06-19 00:00:00","community":"爱下户测试","province":"上海市","city":"上海市","county":"黄浦区","address":"上海市黄浦区卢湾都市型工业楼宇(瞿溪路)","longitude":121.477811,"latitude":31.20378,"modelType":2}
```

##### curl示例
```html
curl -X POST -H "Content-Type: application/json"
-d '{"reserveDate":"2018-06-19 00:00:00","community":"爱下户测试","province":"上海市","city":"上海市","county":"黄浦区","address":"上海市黄浦区卢湾都市型工业楼宇(瞿溪路)","longitude":121.477811,"latitude":31.20378,"modelType":2}
' 'http://aixiahu.com/receiveMsg.action'
```

##### 消息体中的JSON字段说明
名称 | 类型 | 说明
:- | :-: | :-
msg| String | 接口返回信息
code| String| 0 代表成功 403代表异常
data| jsonobject| orderNo: "1806111142400001" 订单号


###### 结束


