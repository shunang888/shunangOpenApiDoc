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
houseModels房屋信息|address       |String   |见图  |房产地址
houseModels房屋信息|areaRemark    |String   |见图  |面积备注（可传空）
houseModels房屋信息|city          |String   |见图  |房产所在城市
houseModels房屋信息|diYa          |String   |见图  |是否有民间抵押
houseModels房屋信息|district      |String   |见图  |房产地区
houseModels房屋信息|doneTime      |Sring   |见图  |竣工年限
houseModels房屋信息|estatesNo     |String   |见图  |产证编号
houseModels房屋信息|floorNo       |Integer |见图  |所在楼层（缺省0）
houseModels房屋信息|floorSum      |Integer |见图  |总楼层（缺省0）
houseModels房屋信息|houseArea     |Double  |见图  |房产面积
houseModels房屋信息|houseNature   |String   |见图  |房产性质(多层公寓、高层公寓、花园住宅、其它、工业厂房、商铺、办公楼)
houseModels房屋信息|isFuGai       |Integer |见图  |民间是否为最高额抵押(0：否、1：是)
houseModels房屋信息|isSeeHouse    |Integer |见图  |能否看房(0：否、1：是，2：未知)
houseModels房屋信息|isZuiGaoEDiYa |Integer |见图  |银行是否为最高额抵押(0：否、1：是)
houseModels房屋信息|juZhu         |String   |见图  |居住情况(自住、租赁有备案、租赁无备案、空置、拆迁安置)
houseModels房屋信息|laoRen        |Integer |见图  |有无老年人和未成年 (0：否、1：是)
houseModels房屋信息|minJian       |String   |见图  |民间抵押余额（缺省0）
houseModels房屋信息|minJianDaoQiRi|String   |见图  |民间到期日
houseModels房屋信息|minJianZiFang |String   |见图  |民间出资方
houseModels房屋信息|owner1        |String   |见图  |房产权利人
houseModels房屋信息|personNo      |Integer |见图  |户口人数（必须提供）
houseModels房屋信息|province      |String   |见图  |房产所在省
houseModels房屋信息|qiTa          |String   |见图  |此前借款用途
houseModels房屋信息|regionName    |String   |见图  |小区名称(必须提供)
houseModels房屋信息|remark        |String   |见图  |备注
houseModels房屋信息|shuXing       |Integer |是    |房屋属性(1抵押房、2备用房)
houseModels房屋信息|urlId         |String   |见图  |附件的GUID，逗号分隔
houseModels房屋信息|useTime       |String   |见图  |使用年限（缺省0）
houseModels房屋信息|yinHang       |String   |见图  |抵押银行名称
houseModels房屋信息|yinHangBalance|String   |见图  |银行抵押余额
houseModels房屋信息|yinHangDaiKuan|String   |见图  |银行贷款性质(按揭、持证抵押)
houseModels房屋信息|yinHangDiYa   |String   |见图  |是否有银行抵押
houseModels房屋信息|yinHangRiQi   |String   |见图  |银行到期日
houseModels房屋信息|DqbHouseDiya  |houseDiyaList  |  |抵押信息(houseDiya对象)
houseModels房屋信息|yinHangXingZhi|String   |见图  |银行性质(中资、外资)
deptModel资方信息|deptId  |Long    |是  ||
deptModel资方信息|userId  |Long    |是  ||
|borrowingBalance  |Integer |是   |借款金额（万元）
|borrowingLife     |Integer |是   |借款期限（月）
|borrowingUsage    |Integer |是   |借款用途
|capitalName       |String   |是   |资金方名称
|monthRate         |String   |是   |月利率
|borrowingLaoren   |String  |是   |老人数
|borrowingXiaohai  |String  |是   |小孩数
|payment           |String   |是   |还款来源
|orderNo     |String   |是   |订单编号
|orderState  |String   |是   |订单状态

