版本号v1.0
通用规则：

所有编码方式均为UTF8
POST请求头中ContentType = application/json;
# 1.下单提交
#####Url：/api/outChannel/houseCommit?#####token=xxxxxxxxxxxxxx
#####请求方式：Post
#####请求参数：


字段名 |字段类型   | 说明 | 是否必填
:- | :-: | :- | :-
regionName |String | 小区名(必须提供)     |是
address    |String | 地址                |是
houseNature|String | 房屋性质            |是
estatesNo  |String | 产证编号            |是
houseArea  |Double | 面积               |是
areaRemark |String | 面积备注（可传空）   |否
province   |String | 省                 |是
city       |String | 市                 |是
district   |String | 区                 |是
floorNo    |Integer| 所在楼层（缺省0）   |是
floorSum   |Integer| 总楼层（缺省0）     |是
remark     |String | 备注（可传空）      |否
urlId      |String | 附件的GUID，逗号分隔（单独文档说明）                                  |是
assessPrice|Double | 自估价             |是

#####完整样例
    {"assessHouseModels": [{
"address": "瞿溪路1234号",
"areaRemark": "面积备注",
"assessPrice": 993.99,
"city": "上海市",
"district": "黄浦区",
"estatesNo": "产证编号001",
"floorNo": 4,
"floorSum": 5,
"houseArea": 99.99,
"houseNature": "房产性质",
"id": 1,
"orderId": 1,
"province": "上海市",
"regionName": "互融小区",
"remark": "备注21434",
"urlId": "5fd614fc-141a-4003-927a-205de047246e,b2873343-9278-4228-91c6-4485c273c4d4"
},{
//第二套
},
...
  ]}
  
字段名  |字段类型    |说明
:- | :-: | :-
code    |String     |状态
msg     |String     |返回信息
orderNo |String     |订单编号

