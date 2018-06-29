版本号v1.0
通用规则：

所有编码方式均为UTF8
POST请求头中ContentType = application/json;
# 1.下单提交
#####Url：/api/outChannel/houseCommit?#####token=xxxxxxxxxxxxxx
#####请求方式：Post
####请求参数：


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
  
####返回参数：
字段名  |字段类型    |说明
:- | :-: | :-
code    |String     |状态
msg     |String     |返回信息
orderNo |String     |订单编号

#2.查看估价结果
#####Url：/api/outChannel/getPriceByOrderNo?#####token=xxxxxxxxxxxxxx
#####请求方式：get
####请求参数：
字段名 |字段类型    |说明  |是否必填    |样例  |完整样例
:- | :-: | :- | :-
orderNo |String  |订单编号    |是   |A20171215180558785  |{orderNo:”...”}

####返回参数：
字段名     |字段类型|说明
:- | :-: | :- | :-
estatesNo |String  |产证编号
message   |String  |退回信息
price     |String  |房屋估价
code      |String  |状态
msg       |String  |返回信息
orderState|String  |订单状态。取固定值：house_confirm

#####完整样例
{
"code": 0,
“msg”:”...”,
“data”:{
"resultModels": 
   {
“message”:””,
"price": 333,
"estatesNo": "沪123",
“orderState”: ”house_confirm”
       }

   }
}

#3.详细情况进件

#####url：/api/outChannel/intoPieces?token=xxxxxxxxxxxxxx
#####请求方式：post
####请求参数：
对象|字段名 |类型  |是否必填    |样例
    :- | :-: | :-
companyInfoModels 借款/权利企业信息    |businessNumber  |Sring    |是   |营业执照编号
companyInfoModels 借款/权利企业信息    |companyName     |Sring    |是   |企业名
companyInfoModels 借款/权利企业信息    |companyType     |Integer  |是   |企业类型类型 1 借款企业2权利企业（即房屋所有人）
custInfoModels 借款/权利人信息|custType    |Integer |是   |客户类型 1 借款人2 权利人（即房屋所有人）
custInfoModels 借款/权利人信息    |hunyinStatus    |Integer |是   |婚姻状态(1:未婚、2：已婚、3：离异、4：丧偶、5：两          次以上婚史)
custInfoModels 借款/权利人信息    |idType  |Integer |是   |证件类型
custInfoModels 借款/权利人信息    |job |Sring   |是   |职业
custInfoModels 借款/权利人信息    |laoren  |Integer |是   |有老人数（必须提供）
custInfoModels 借款/权利人信息    |name    |Sring   |是   |客户名称
custInfoModels 借款/权利人信息    |sid |Sring   |是   |证件号码
custInfoModels 借款/权利人信息    |telephone   |String   |是   |电话
custInfoModels 借款/权利人信息    |xiaohai |String   |是   |有未成人数（年龄小于18岁）（必须提供）