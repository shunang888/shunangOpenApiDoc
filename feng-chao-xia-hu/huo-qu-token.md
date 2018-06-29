# 获取token

> 1 客户获取token 之后可以调用下户系统提供的开放api。

> 2 参数说明:
   - appId: 为用户申请的appId
   - timestamp: 当前UTC时间戳，从1970年1月1日0点0 分0 秒开始到现在的毫秒数(String)
   - checkStr: 请求签名
      - 签名规则:
      - sha1(secritKey,appId,timestamp) , 其中secritKey为用户申请app时候附带 请用户妥善保存
      
```java
 // 计算并获取CheckStr示例
    public static String getCheckStr(String publicKey, String appId, String timestamp) {
        return encode("sha1", publicKey + appId + timestamp);
    }

    private static String encode(String algorithm, String value) {
        if (value == null) {
            return null;
        }
        try {
            MessageDigest messageDigest = MessageDigest.getInstance(algorithm);
            messageDigest.update(value.getBytes());

            /* format */
            byte[] bytes =messageDigest.digest();
            int len = bytes.length;
            StringBuilder buf = new StringBuilder(len * 2);
            for (int j = 0; j < len; j++) {
                buf.append(HEX_DIGITS[(bytes[j] >> 4) & 0x0f]);
                buf.append(HEX_DIGITS[bytes[j] & 0x0f]);
            }
            return buf.toString();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
    
    private static final char[] HEX_DIGITS = { '0', '1', '2', '3', '4', '5','6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f' };
```      
      

- 示例-获取token：

 - 1.1. HTTP示例

 - 1.2. curl示例

 - 1.3. 消息体中的JSON字段说明

##### HTTP示例
```
POST /receiveMsg.action HTTP/1.1
Host: sso.ixiahu.com
Content-Type: application/json

{"appId":"0462cbdc-7658-44c6-a96d-e6fc4fa53034", "timestamp":"1440570500855", "checkStr":"2d3d2086cb7ec273ac0c2f961c353b2fc4ddb0e3"}
```

##### curl示例
```html
curl -X POST -H "Content-Type: application/json"
-d '{"appId":"0462cbdc-7658-44c6-a96d-e6fc4fa53034", "timestamp":"1440570500855", "checkStr":"2d3d2086cb7ec273ac0c2f961c353b2fc4ddb0e3"}' 'http://sso.ixiahu.com
/sso/api/oauth2.0/getAccessToken'
```

##### 消息体中的JSON字段说明
名称 | 类型 | 说明
:- | :-: | :-
msg| String | 结果说明
code|int| 0 代表成功 401登陆失败 403其他异常
data|jsonObject|"expire":43200 > 过期时间,<br/> "token":"ba641a7a356b05e5047916be2da0fc7a" > token对象


###### 结束







# 获取token

> 1 客户获取token 之后可以调用下户系统提供的开放api。

> 2 参数说明:
   - appId: 为用户申请的appId
   - timestamp: 当前UTC时间戳，从1970年1月1日0点0 分0 秒开始到现在的毫秒数(String)
   - checkStr: 请求签名
      - 签名规则:
      - sha1(secritKey,appId,timestamp) , 其中secritKey为用户申请app时候附带 请用户妥善保存
      
```java
 // 计算并获取CheckStr示例
    public static String getCheckStr(String publicKey, String appId, String timestamp) {
        return encode("sha1", publicKey + appId + timestamp);
    }

    private static String encode(String algorithm, String value) {
        if (value == null) {
            return null;
        }
        try {
            MessageDigest messageDigest = MessageDigest.getInstance(algorithm);
            messageDigest.update(value.getBytes());

            /* format */
            byte[] bytes =messageDigest.digest();
            int len = bytes.length;
            StringBuilder buf = new StringBuilder(len * 2);
            for (int j = 0; j < len; j++) {
                buf.append(HEX_DIGITS[(bytes[j] >> 4) & 0x0f]);
                buf.append(HEX_DIGITS[bytes[j] & 0x0f]);
            }
            return buf.toString();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }
    
    private static final char[] HEX_DIGITS = { '0', '1', '2', '3', '4', '5','6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f' };
```      
      

- 示例-获取token：

 - 1.1. HTTP示例

 - 1.2. curl示例

 - 1.3. 消息体中的JSON字段说明

##### HTTP示例
```
POST /receiveMsg.action HTTP/1.1
Host: sso.ixiahu.com
Content-Type: application/json

{"appId":"0462cbdc-7658-44c6-a96d-e6fc4fa53034", "timestamp":"1440570500855", "checkStr":"2d3d2086cb7ec273ac0c2f961c353b2fc4ddb0e3"}
```

##### curl示例
```html
curl -X POST -H "Content-Type: application/json"
-d '{"appId":"0462cbdc-7658-44c6-a96d-e6fc4fa53034", "timestamp":"1440570500855", "checkStr":"2d3d2086cb7ec273ac0c2f961c353b2fc4ddb0e3"}' 'http://sso.ixiahu.com
/sso/api/oauth2.0/getAccessToken'
```

##### 消息体中的JSON字段说明
名称 | 类型 | 说明
:- | :-: | :-
msg| String | 结果说明
code|int| 0 代表成功 401登陆失败 403其他异常
data|jsonObject|"expire":43200 > 过期时间,<br/> "token":"ba641a7a356b05e5047916be2da0fc7a" > token对象


###### 结束







