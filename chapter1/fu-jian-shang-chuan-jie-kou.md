#附件上传、下载接口 V1.0

一、上传文件

请求
地址：http://api.fyamc.cn:31101/file/upload.ashx?UploadUser=xxxxxxxxxxx&VDir=xxxxxxxxxxx&UserName=xxxxxxxxxxxxxxxxxxxxxxx&RefID=xxxxxxxxxxxxxxxxxxx
UploadUser参数传入调用者的用户名，该用户名由我方分配，调用方应当妥善保管该用户名，防止泄露
VDir（可选）参数用于指定上传文件所处的目录，例如\客户资料\产证照片，如不传则默认为根路径\
UserName（可选）参数用于指定上传文件的归属用户，由调用者自行管理，与UploadUser无关
RefID(可选)用户自定义传入的字符串，返回结果中将包含这个字符串（常用于前端标记）
请求方式：POST
Content-Type:multipart/form-data
请求体：文件流



返回值
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