
### 人脸识别结果通知
#### 调用场景
当摄像头捕获并识别完了人脸后，将数据通知系统。接口采用https协议，只支持POST调用方式。  

### 接口地址
https://api.juniuo.com/face/notify.do  

### 请求参数
> 参数通过post请求的body传递，格式为json  

参数名        | 参数类型    | 必传  | 说明
------------ | -----------|-------| --------
partner_id   | 字符串     |  是   | 提供人脸识别支持的合作方， 桔牛提供
terminal_id  | 字符串     |  是   | 人脸识别的终端机器id， 桔牛与合作方协商生成
camera_id    | 字符串     |  是   | 人脸识别终端摄像头id， 桔牛与合作方协商成成
camera_type  | 字符串     |  是   | 人脸识别终端摄像头类型 pos/gate（分别表示收银台/店门口）
random       | 整数       |  是   | 10位随机数字
sign         | 字符串     |  是   | 签名，（请参照下面“接口sign的计算方式“部分）
face_data    | 数组       |  是   | 人脸数据，由face_id和face_img对象组成的数组（可能同时识别到多个人），参照下面face_data参数说明
  
face_data参数组成 :
 
参数名        | 参数类型    | 必传  | 说明
------------ | -----------|-------| --------
face_id      | 字符串      |  是   | 人脸唯一id
face_img     | 字符串      |  是   | 人脸图片的base64编码

参数示例：  
```
{
    "partner_id": "abc123",
    "terminal_id": "a001",
    "camera_id": "a001002",
    "camera_type": "pos",
    "random": 1234567890,
    "sign": "",
    "face_data": [
        {
            "face_id": "b0010020001",
            "face_img": "data:image/jpg;base64,/9j/4QMZR..."
        }
    ]
}
```

#### 接口sign的计算方式  
1、将参数partner_id,partner_token,terminal_id,terminal_pwd,camera_id,random通过"key1=value&key2=value"等方式拼接；  
2、将拼接的字符串进行md5，得到32位小写的值即位sign。  

例如在上例中，sign=MD5("partner_id=abc123&partner_token=2d2e22sdk&terminal_id=a001&terminal_pwd=wdlksdw223&camera_id=a001002&camera_type=pos&random=1234567890")  

> 加密拼接串中的partner_token为桔牛提供。terminal_pwd为桔牛和合作方协商生成。  

#### 返回结果
接口返回一个json格式的内容  
当发生错误时：
```
{
    "errorCode":"camera_not_exists",
    "errorInfo":"摄像头不存在",
    "data":""
}
```
仅当errorCode为0时表示成功：
```
{
    "errorCode":"0",
    "errorInfo":"",
    "data":""
}
```