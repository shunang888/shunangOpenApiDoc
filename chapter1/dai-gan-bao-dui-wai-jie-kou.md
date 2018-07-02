版本号v1.0
通用规则：
所有编码方式均为UTF8
POST请求头中ContentType = application/json;

# 1.下单提交

Url：/api/outChannel/houseCommit?#####token=xxxxxxxxxxxxxx
请求方式：Post

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

######完整样例
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

Url：/api/outChannel/getPriceByOrderNo?#####token=xxxxxxxxxxxxxx
请求方式：get

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

######完整样例
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

url：/api/outChannel/intoPieces?token=xxxxxxxxxxxxxx
请求方式：post

####请求参数：
对象|字段名 |类型  |是否必填    |样例
    :- | :-: | :-
companyInfoModels 借款/权利企业信息    |businessNumber  |String    |是   |营业执照编号
companyInfoModels 借款/权利企业信息    |companyName     |String    |是   |企业名
companyInfoModels 借款/权利企业信息    |companyType     |Integer   |是   |企业类型类型 1 借款企业2权利企业（即房屋所有人）
custInfoModels 借款/权利人信息(C)    |custType        |Integer |是   |客户类型 1 借款人2 权利人（即房屋所有人）
C    |hunyinStatus    |Integer |是   |婚姻状态(1:未婚、2：已婚、3：离异、4：丧偶、5：两次以上婚史)
C    |idType    |Integer  |是   |证件类型
C    |job       |String   |是   |职业
C    |laoren    |Integer  |是   |有老人数（必须提供）
C    |name      |String   |是   |客户名称
C    |sid       |tSring   |是   |证件号码
C    |telephone |String   |是   |电话
C    |xiaohai   |String   |是   |有未成人数（年龄小于18岁）（必须提供）
houseModels房屋信息(H)|address       |String   |见图  |房产地址
H|areaRemark    |String   |见图  |面积备注（可传空）
H|city          |String   |见图  |房产所在城市
H|diYa          |String   |见图  |是否有民间抵押
H|district      |String   |见图  |房产地区
H|doneTime      |String   |见图  |竣工年限
H|estatesNo     |String   |见图  |产证编号
H|floorNo       |Integer  |见图  |所在楼层（缺省0）
H|floorSum      |Integer  |见图  |总楼层（缺省0）
H|houseArea     |Double   |见图  |房产面积
H|houseNature   |String   |见图  |房产性质(多层公寓、高层公寓、花园住宅、其它、工业厂房、商铺、办公楼)
H|isFuGai       |Integer  |见图  |民间是否为最高额抵押(0：否、1：是)
H|isSeeHouse    |Integer  |见图  |能否看房(0：否、1：是，2：未知)
H|isZuiGaoEDiYa |Integer  |见图  |银行是否为最高额抵押(0：否、1：是)
H|juZhu         |String   |见图  |居住情况(自住、租赁有备案、租赁无备案、空置、拆迁安置)
H|laoRen        |Integer  |见图  |有无老年人和未成年 (0：否、1：是)
H|minJian       |String   |见图  |民间抵押余额（缺省0）
H|minJianDaoQiRi|String   |见图  |民间到期日
H|minJianZiFang |String   |见图  |民间出资方
H|owner1        |String   |见图  |房产权利人
H|personNo      |Integer  |见图  |户口人数（必须提供）
H|province      |String   |见图  |房产所在省
H|qiTa          |String   |见图  |此前借款用途
H|regionName    |String   |见图  |小区名称(必须提供)
H|remark        |String   |见图  |备注
||shuXing       |Integer  |是    |房屋属性(1抵押房、2备用房)
||urlId         |String   |见图  |附件的GUID，逗号分隔
||useTime       |String   |见图  |使用年限（缺省0）
||yinHang       |String   |见图  |抵押银行名称
||yinHangBalance|String   |见图  |银行抵押余额
||yinHangDaiKuan|String   |见图  |银行贷款性质(按揭、持证抵押)
||yinHangDiYa   |String   |见图  |是否有银行抵押
||yinHangRiQi   |String   |见图  |银行到期日
||DqbHouseDiya  |houseDiyaList | |抵押信息(houseDiya对象)
||yinHangXingZhi|String   |见图  |银行性质(中资、外资)
deptModel资方信息|deptId          |Long     |是    ||
deptModel资方信息|userId          |Long     |是    ||
loanInfoModel 借款信息|borrowingBalance  |Integer |是   |借款金额（万元）
||borrowingLife       |Integer |是   |借款期限（月）
||borrowingUsage      |Integer |是   |借款用途
||capitalName         |String  |是   |资金方名称
||monthRate           |String  |是   |月利率
||borrowingLaoren     |String  |是   |老人数
||borrowingXiaohai    |String  |是   |小孩数
||payment             |String  |是   |还款来源
||orderNo             |String  |是   |订单编号
||orderState          |String  |是   |订单状态
houseDiya抵押信息      |fk_house_id       |Integer |是   |关联订单dqb_house表主键
同上||dycs              |String   |是   |抵押次数
同上||dyqr              |String   |是   |抵押权人
同上||dyje              |double   |是   |抵押全额
同上||dyye              |double   |是   |抵押余额
同上||zgedy             |String   |是   |最高额抵押
同上||dyxz              |String   |是   |抵押性质
同上||dkxz              |String   |是   |贷款性质
同上||kssj              |Time    |是   |开始时间
同上||jssj              |Time    |是   |结束时间
||ziLiaoGuid        |String  |是   |资包id

#####特别说明：
(1)
houseModels中，如果是抵押房（shuXing=1），则以下字段的值将被忽略：
houseNature(房屋性质)、estatesNo(产证编号)、houseArea(面积)、
regionName(小区名)、floorNo(所在楼层)、floorSum(总楼层)
province(省)、city(市)、district(区)、address(地址)
抵押房各个字段如下图所示：
![](/assets/图片1.png)
若“是否抵押”=“否”，则抵押信息不必填写，否则必须填写

(2)
备用房字段可以简化（*必填，其他选填），如下图所示：
![](/assets/图片2.png)

(3)
deptModel资方信息是一对枚举值，调用双方必须实时更新值库。

(4)
orderState有以下两种可能的取值：
house_confirm:房屋评估待确认==需要确认后才能详细进件
house_confirmed:房屋评估已确认
riskmanage_return_modify:风控退回（修改）	
一般情况下默认为house_confirmed，如果这个单子收到过“风控退回（修改）”的消息通知（后文有详细说明），则应该传入riskmanage_return_modify。
riskmanage_evaluation 风控中 可以补充材料

####返回参数：
字段名 |字段类型    |说明     |样例
    :- | :-: | :-
code  |String      |状态  ||
msg   |String      |返回信息 ||   

######完整样例
{
"msg": "token不能为空",
"code": 500
}

#4.估价复议

Url：/api/outChannel/priceReconsider?token=xxxxxxxxxxxxxx
请求方式：post

####请求参数：
|字段名       |字段类型      |是否必填    |说明  |样例
:- | :-: | :-
|orderNo      |String   |是   |订单编号    |A20171215175337324
|estatesNo    |String   |是   |房产编号    |沪房地2字2001第0123123号
|caseBack     |String   |是   |理由       |价格偏高，价格偏低，其他
|message      |String   |是   |具体原因    
|attachmentId |String   |是   |附件的GUID，逗号分隔（单独文档说明）    |5fd614fc-141a-4003-927a-205de047246e,b2873343-9278-4228-91c6-4485c273c4d4
|orderState   |String   |是   |订单状态    |house_fuyi

######完整样例
{
“orderState”:house_fuyi,
"fuYiModels": [{
"caseBack": "价格偏高",
"estatesNo": “...”,
"message": "文本框中的内容",
"urlId": "5fd614fc-141a-4003-927a-205de047246e,b2873343-9278-4228-91c6-4485c273c4d4"
},{},...
],
"orderNo": 90
}

####返回参数：
|字段名	|字段类型  |说明	   |样例
:- | :-: | :-
|code	|String	  |状态	   ||
|msg	|String	  |返回信息 ||	

######完整样例
{ 
 "msg": "",
"code": 200
}

#5.认可评估价格

Url： /api/outChannel/queRenJiaGe?token=xxxxxxxxxxxxxx
请求方式：post

####请求参数：
|字段名	   |字段类型	|是否必填	|说明	        |样例
:- | :-: | :-
|orderNo   |String	|是	        |订单编号	|A20171215180558785

######完整样例
{
orderModel:{
orderNo:”A20171215180”
  }
}

####返回参数：
字段名  |字段类型   |说明  |样例
:- | :-: | :-
code    |String   |状态  ||
msg     |String   |返回信息   || 

######完整样例
{  "msg": "",
"code": 200
}

#6.弃单

Url：/api/outChannel/orderGiveUp?token=xxxxxxxxxxxxxx
请求方式：post

####请求参数：
字段名   |字段类型     |是否必填    |说明        |样例
:- | :-: | :-
orderNo |String      |是          |订单编号    |A20171215180558785

######完整样例
{
orderModel:{
orderNo:”A20171215180”
}
}

####返回参数：
字段名	|字段类型	|说明	   |样例
:- | :-: | :-
code	|String	        |状态	   ||
msg	|String	        |返回信息  ||	

######完整样例
{ 
 "msg": "",
"code": 200
}

#7.获取保理结果

Url： /api/outChannel/getGuaranteeResult?token=xxxxxxxxxxxxxx
请求方式：get

####请求参数：
字段名	|字段类型   |是否必填	|说明	 |样例	               |完整样例
:- | :-: | :-
orderNo	|String	   |是	       |订单编号 |A20171215180558785	||

####返回参数：

字段名       |字段类型   |说明
:- | :-: | :-
code        |String    |状态
msg         |String    |返回信息
riskResule  |String    |风控结果
riskBalance |String    |出保金额（万元）
yearRate    |String    |年利率
riskMessage |String    |最终风控意见

######完整样例
{ 
"msg": "",
"code": 500
“guaranteeModel”:
  {
“riskResule”:
“riskBalance”:
“yearRate”:
“riskMessage”：
}
}

#8.补充资料

Url：/api/outChannel/buChong?token=xxxxxxxxxxxxxx
请求方式：post

####请求参数：
字段名   |字段类型 |是否必填 |说明        |样例
:- | :-: | :-
orderNo |String  |是       |订单编号    |A20171215180558785
beizhu  |String  |是       |备注  
urlId   |String  |是       |附件的GUID，逗号分隔（单独文档说明）    |5fd614fc-141a-4003-927a-205de047246e,b2873343-9278-4228-91c6-4485c273c4d4

####返回参数：
字段名	|字段类型   |说明       |样例
:- | :-: | :-
code	|String	    |状态       ||
msg	|String	    |返回信息   ||

######完整样例	
{ 
 "msg": "",
"code": 200
}

#9.系统登录

URL:/api/interfaceLogin
请求方式:post

####请求参数：
字段名	|字段类型    |是否必填	 |说明	    |完整样例
:- | :-: | :-
username|String	     |是	 |用户名称   ||
password|String	     |是	 |密码	    ||

####返回参数：
字段名  |字段类型   |说明
:- | :-: | :-
code   |String    |状态：（0:成功、500：失败）
token  |String    |返回token信息(用作调用其它接口的关键值)
msg    |String    |返回结果描述(失败时才有)

######完整样例
{ 
"msg": "",
"code": 0,
“token”: “abcdef”
}

特别说明：成功登录后，调用方必须保存返回的token，并将该token作为参数，在其他所有接口中表现。Token有效期为12小时，同一用户重复登录将使之前的token失效。

#11. 渠道确认风控结果

url:/api/risk/riskResultConfirm?token=xxxxxxxxxxxxxx
请求方式：get

####请求参数：
字段名   |字段类型    |是否必填    |说明       |完整样例

orderNo  |String     |是         |订单编号   | { "orderNo": "11111",}

####返回参数：
字段名   |字段类型   |说明
:- | :-: | :-
code    |String    |状态：（0:成功、500：失败）
msg     |String    |返回结果描述(失败时才有)

######完整样例
{ 
"msg": "",
"code": 0,
}

#12.字典表字段

####证件类型：
身份证 :1 
护照 :2 
港澳通行证  :3
台胞证  :4 
其它 :5

####婚姻状态：
未婚  :1 
已婚 :2 
离异 :3 
丧偶 :4 
两次以上婚史 :5

####房产性质：
多层公寓          :1 
高层公寓         :2 
花园住宅         :3 
工业厂房         :4 
商铺              :5 
办公楼            :6 
已购公房、房改房  :7
商住两用         :8
经济适用房        :9
其它             :10

####居住情况：
自住   : 1 
租赁有备案: 2 
租赁无备案: 3
空置  : 4 
拆迁安置: 5  

####银行性质(权人类型)：
中资银行: 1
外资银行:  2
小贷公司:  3
典当行  :4 
民间个人:  5
其他公司:  6
未知 :7

####房屋属性：
抵押房 :1
备用房  :2
其它 :3

####银行贷款性质(抵押种类)：
按揭  :1
普通抵押:  2
最高额抵押  :3
公积金贷款抵押  :4
其他 :5