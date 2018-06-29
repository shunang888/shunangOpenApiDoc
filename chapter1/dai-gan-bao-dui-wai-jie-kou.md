版本号v1.0
通用规则：

所有编码方式均为UTF8
POST请求头中ContentType = application/json;
# 1.下单提交
####Url：/api/outChannel/houseCommit?####token=xxxxxxxxxxxxxx
####请求方式：Post
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