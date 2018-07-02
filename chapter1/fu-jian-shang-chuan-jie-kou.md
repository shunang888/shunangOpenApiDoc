#附件上传、下载接口 V1.0

###一、上传文件

#####请求
地址：http://api.fyamc.cn:31101/file/upload.ashx?UploadUser=xxxxxxxxxxx&VDir=xxxxxxxxxxx&UserName=xxxxxxxxxxxxxxxxxxxxxxx&RefID=xxxxxxxxxxxxxxxxxxx

UploadUser参数传入调用者的用户名，该用户名由我方分配，调用方应当妥善保管该用户名，防止泄露
VDir（可选）参数用于指定上传文件所处的目录，例如\客户资料\产证照片，如不传则默认为根路径\
UserName（可选）参数用于指定上传文件的归属用户，由调用者自行管理，与UploadUser无关
RefID(可选)用户自定义传入的字符串，返回结果中将包含这个字符串（常用于前端标记）

请求方式：POST
Content-Type:multipart/form-data
请求体：文件流

#####返回值

类型：JSON数组
数组元素的结构及说明如下：
ClassRtnMsg
{
    PublicstringRefID;  //参考ID回传
    Publicstring status;  //状态，0=正常，500=错误
    PublicstringerrMsg; //错误消息，当status=err时，表示对错误的文字描述
    PublicstringfileName;//文件名（将调用方传过来的文件名称回传）
    PublicstringfileGUID;//文件GUID，以后下载的时候使用该GUID来请求文件
}

备注：（上传文件时系统会为每个文件分配一个唯一的GUID，上传方必须保存该GUID，用于下载等操作）


###二、下载文件

#####请求
地址：http://api.fyamc.cn:31101/file/download.ashx?GUID=XXXXXXXXXXXXXXXXXXXXXXXXX
请求方式：GET
请求参数：文件的GUID值

#####返回
如果文件存在就返回文件，response头中含有以下信息
Content-Type:application/octet-stream
content-disposition:attachment;filename=原上传时候的文件名

如果不存在则返回HTTP 404

注意：为了获得更好的体验，如果文件是jgp/png格式，则Content-Type:image/jpeg或Content-Type:image/png，浏览器会直接加载显示该图片，而不是弹出下载附件框

###三、预览图片（获取缩略图）

#####请求
地址：http://api.fyamc.cn:31101/file/preview.ashx?GUID=XXXXXXXXXXXXXXXXXXXXXXXXX&h=111&w=222
请求方式：GET
请求参数：
GUID=文件的GUID值
w=可选值，缩略图的宽度（像素）
h=可选值，缩略图的高度（像素）
默认w=85,h=60

#####返回
如果文件是jgp/png格式，则Content-Type:image/jpeg或Content-Type:image/png

如果不存在或非图片格式则返回HTTP 404

###四、删除文件

#####请求
地址：http://api.fyamc.cn:31101/file/delete.ashx?GUID=XXXXXXXXXXXXXXXXXXXXXXXXX
请求方式：POST
请求参数：
GUID=文件的GUID值

#####返回
样例：
{"code"="200","msg"="OK"}

成功删除则返回code=200，失败则返回code=500

注意：文件并不会被物理删除，只是逻辑上标记为删除状态，但是调用download方法或info方法都将返回错误。

以上http://api.fyamc.cn:31101为正式环境，测试环境将uri改为http://testfile.91zhaiquan.net:31102/*****/***开头，其它值不变

