# 消息抄送

消息抄送功能概述

>1、下户通信服务器可以通过消息抄送功能，将消息数据实时同步给第三方开发者的服务器。`在接收数据之前，需要在下户通信管理后台注册消息抄送数据的接收地址`；

>2、抄送消息时，若开发者服务器处于离线状态或者由于其他原因导致连接不上消息接收地址，下户通信会根据一定策略再尝试抄送一定次数，若开发者服务器仍然无法连接，默认情况下，下户通信`将会丢弃抄送失败的消息`。若有特殊需求不能丢弃消息，请联系下户通信商务经理；

>3、考虑到网络环境的不稳定，为了确保开发者的消息接口能收到抄送的消息，下户通信可能会重复发送同一条消息，建议开发者对所收到的消息进行一定的`去重操作`；

>4、下户通信消息抄送服务对于一条消息是否抄送成功具有`超时判定机制（超时时间为5s）`，若超时，将会尝试重新抄送一定次数。如果第三方消息接收接口在接收到消息之后，会做比较耗时的操作（例如DB入库等操作）的话，建议将该接口做成`异步机制`（例如可以将消息先存到MQ中），以免被下户通信判定为超时；

>5、在消息抄送服务中，checkStr= sha1(secritKey,appId,timestamp)， 其中`secritKey、appId、timestamp`均为String类型。在验证数据是否在传输过程中被篡改时，需要`计算验证checkStr`。secritKey值为开发者的secritKey， appId为分sso分配的  。

>6、下户通信抄送服务需要开发者服务器在超时时间（5s）内返回HTTP 200状态码，以验证本次消息抄送是否成功。


### 抄送消息类型
> 消息抄送包含两种：

>>"eventType"="1" 抄送报告连接 

>>"eventType"="2" 抄送订单状态完成


---

- 示例-抄送报告连接：

 - 1.1. 消息体中的JSON字段说明
 

##### 抄送字段列表
名称 | 类型 |示例| 说明  
:- | :-: | :- | :- 
eventType | String | "1" | 抄送报告连接 
appId| String | "0462cbdc-7658-44c6-a96d-e6fc4fa53034" | 抄送报告连接appId
timestamp| String | "1440570500855" | String 时间戳
checkStr| String | "2d3d2086cb7ec273ac0c2f961c353b2fc4ddb0e3" | 校验字段
orderNo| String | "1806111023210001" | 订单编号
reportUrl| String | "http://testfile.91zhaiquan.net:31102/file/download.ashx?GUID=fb9bafb3-eda9-4ddf-847e-05b92907cedc" | 报告地址


- 1.2. 消息体中的JSON字段说明

##### 抄送字段列表
名称 | 类型 |示例| 说明
:- | :-: | :- | :-
eventType | String | "2" | 抄送订单状态完成
appId| String | "0462cbdc-7658-44c6-a96d-e6fc4fa53034" | 抄送报告连接appId
timestamp| String | "1440570500855" | String 时间戳
checkStr| String | "2d3d2086cb7ec273ac0c2f961c353b2fc4ddb0e3" | 校验字段
orderNo| String | "1806111023210001" | 订单编号
finish| String | "true" | 订单已经完成



###### 结束

