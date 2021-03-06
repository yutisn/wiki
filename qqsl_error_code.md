<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [青清水利错误码定义](#%E9%9D%92%E6%B8%85%E6%B0%B4%E5%88%A9%E9%94%99%E8%AF%AF%E7%A0%81%E5%AE%9A%E4%B9%89)
    - [一. 2xxx：成功返回](#%E4%B8%80-2xxx%E6%88%90%E5%8A%9F%E8%BF%94%E5%9B%9E)
    - [二. 4xxx：客户端错误,这类的状态码代表了客户端看起来可能发生了错误，妨碍了服务器的处理。服务器就应该返回一个解释当前错误码。除了4000在GET和POST请求可能返回，其他的客户端错误码都是针对POST请求的。前两个xx代表错误分类，最后一个x代表具体错误类型。](#%E4%BA%8C-4xxx%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%94%99%E8%AF%AF%E8%BF%99%E7%B1%BB%E7%9A%84%E7%8A%B6%E6%80%81%E7%A0%81%E4%BB%A3%E8%A1%A8%E4%BA%86%E5%AE%A2%E6%88%B7%E7%AB%AF%E7%9C%8B%E8%B5%B7%E6%9D%A5%E5%8F%AF%E8%83%BD%E5%8F%91%E7%94%9F%E4%BA%86%E9%94%99%E8%AF%AF%E5%A6%A8%E7%A2%8D%E4%BA%86%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E5%A4%84%E7%90%86%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%B0%B1%E5%BA%94%E8%AF%A5%E8%BF%94%E5%9B%9E%E4%B8%80%E4%B8%AA%E8%A7%A3%E9%87%8A%E5%BD%93%E5%89%8D%E9%94%99%E8%AF%AF%E7%A0%81%E9%99%A4%E4%BA%864000%E5%9C%A8get%E5%92%8Cpost%E8%AF%B7%E6%B1%82%E5%8F%AF%E8%83%BD%E8%BF%94%E5%9B%9E%E5%85%B6%E4%BB%96%E7%9A%84%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%94%99%E8%AF%AF%E7%A0%81%E9%83%BD%E6%98%AF%E9%92%88%E5%AF%B9post%E8%AF%B7%E6%B1%82%E7%9A%84%E5%89%8D%E4%B8%A4%E4%B8%AAxx%E4%BB%A3%E8%A1%A8%E9%94%99%E8%AF%AF%E5%88%86%E7%B1%BB%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AAx%E4%BB%A3%E8%A1%A8%E5%85%B7%E4%BD%93%E9%94%99%E8%AF%AF%E7%B1%BB%E5%9E%8B)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 青清水利错误码定义
### 一. 2xxx：成功返回

>
2000：OK
    请求已成功。实际的响应将取决于所使用的请求方法。在GET请求中，响应将包含所希望数据；POST请求中，响应将包含描述操作结果的数据。

### 二. 4xxx：客户端错误,这类的状态码代表了客户端看起来可能发生了错误，妨碍了服务器的处理。服务器就应该返回一个解释当前错误码。除了4000在GET和POST请求可能返回，其他的客户端错误码都是针对POST请求的。前两个xx代表错误分类，最后一个x代表具体错误类型。

**[400x表示通用错误]**
>
*   4000: PARAMETER_ERROR
    参数错误，表示服务器收到的参数不合法，比如预期是整型，客户端传递的
    是字符串；预期是手机号，客户端传递的不合法；请求被拒绝。
*   4001：FAIL
    操作失败，标识服务器执行过程中出现异常，无法继续执行，服务器要保证
    失败后恢复到执行前的转台，比如失败后保证不修改数据库和缓存。
*   4002: PASSWORD_ERROR
    密码错误，比如修改密码时，原密码输入错误。
*   4003: FILE_TOO_MAX
    上传文件过大，服务器拒绝。
*  4004: FILE_TYPE_ERROR
    文件类型出错,比如前台发送office文件给后台，后台记录这个文件信息，用于检测子系统进行文件转换，如果文件类型不是office文件，报出这个错误。    

**[401x标识和session相关错误]**
>
*   4010: UNAUTHORIZED
    无访问权限，即用户没有必要的凭据,shiro认证异常或拦截出错时返回这个错误。
*   4011: NO_SESSION
    无SESSION，即服务器端对应SESSION已经失效或删除，客户端无法连接，必须重新登录。

**[402x标识和必须数据有关错误]**
>
*   4020: DATA_EXIST
    数据已存在，即要添加数据已经存在，不能重复添加，比如此手机号已注册，再次注册产生这个错误。
*   4021：DATA_NOEXIST
    数据不存在，无法继续执行操作，比如坐标上传时，根据客户端发送的项目
    id，数据库查询不到项目；再比如web端登陆时，根据code查询不到用户，
    返回这个错误。
*   4022: DATA_REFUSE
    请求的数据不属于自己，拒绝操作，比如删除不是自己的项目,请求不时自己的订单,不是自己的测站等操作。
* 4023: DATA_LOCK
    数据已被锁定，比如用户登录时，如果用户被锁定，返回这个错误。 

**[403x千寻错误]**
>
*   4030: QXWZ_FULL
    千寻连接池已满，无法提供服务，请稍候尝试连接。   

**[404x标识验证码相关错误]**
>
*   4040 CODE_NEED
    需要验证码，比如web端第一次登录，或登录过，但是15天内没有登陆过，再次登录时产生这个错误。
*   4041: CODE_INVALID
    验证码过期，需要重新获取，验证码一般只有5-10分钟的有效期，超过这个时间，验证码需要重新获取。
*   4042: CODE_ERROR
    验证码输入错误，请重新提交。
*   4043: CODE_NOEXIST
    未获取验证码，请点击获取。

**[405x标识套餐错误]**
>
*   4050: PACKAGE_EXPIRED
    套餐已过期，无法提供服务，比如无法上传文件、无法修改要素等操作，套餐必须要续费。
*   4051: PACKAGE_LIMIT
    套餐限制，不允许执行，比如空间已满或流量用尽，不允许上传文件；新建
    项目数达到上限，不允许建立项目。
*   4052: PACKAGE_NOALLOW_BUY
    套餐不满足购买条件，比如空间大小,子账户数已超过套餐限制,无法购买。
*   4053: PACKAGE_NOALLOW_RENEW
    套餐不满足续费条件,比如测试套餐不允许续费。
*   4054: PACKAGE_NOALLOW_UPDATE
    套餐不满足升级条件，比如升级后套餐小于等于目前套餐。   

**[406x表示认证错误]**
>
*   4060: CERTIFY_NO_PERSONAL
    未进行实名认证，无法购买套餐等操作,或未进行实名认证,直接进行企业认
    证也返回这个错误。
*   4061: CERTIFY_NO_COMPANY
    未进行企业认证，无法购买高级套餐，购买数据服务。
*   4062: CERTIFY_REPEAT
    重复认证错误，账号已认证不能再次认证了，如果再次发起认证，将返回这个错误。

**[407x坐标相关错误]**
>
*   4070: COOR_PROJECT_NO_CENTER
    项目中心未设置，上传坐标时，返回这个错误。
*   4071: COOR_BUILD_CENTER_ERROR  
    上传的坐标excel中建筑物中心点或定位点格式错误，无法添加建筑物。
*   4072: COOR_FORMAT_ERROR
    上传的坐标excel文件格式错误，文件损坏，excel文件格式不是预期的，excel数据不是预期的。
*   4073: COOR_TYPE_ERROR
    上传时选择的坐标类型和excel数据不一致，比如选择的是WGS84的度类型，上传的是WGS84的度分秒格    式，返回这个错误。
*   4074 COOR_UNKONW_SHEET_TYPE
    sheet类型不能对应到枚举		
*   4075 COOR_RETURN_PROMPT
    上传时返回相应提示信息
    
**[408x订单相关错误]**
>
*   4080: TRADE_EXPIRED
    订单过期，比如对过期订单进行支付，返回这个错误。
*   4081: TRADE_PAYED
    订单已支付，比如关闭一个已完成支付的订单，返回这个错误。
*   4082: TRADE_HAS_NOPAY
    有未支付的订单，比如已有未支付的订单，再次生成订单，返回这个错误。     
*   4083: TRADE_NOPAY
    订单未支付，比如删除一个未支付的订单，返回这个错误。    
    
**[409x子账号错误]**    
>
* 4090 ACCOUNT_NO_CONFIRMED，子账号未确认  
    子账号未通过确认，不能登录，一般是新建后，子账号未确认或拒绝
* 4091 ACCOUNT_INVITED
    子账号已被邀请，不能重复邀请，用于由企业邀请子账号，子账号还未回复，但是由于短信只能定位到手机号，所以别的企业暂时不能重复邀请，必须等24小时候等邀请失效后，才能再次邀请
    
**[410x全景错误]**
>
*   4101: PANORAMA_NO_SCENE
    全景下没有场景，无法显示或编辑  
*   4102: PANORAMA_IMAGE_NOT_EXIST
    新建全景时，图片下载失败
*   4103: PANORAMA_SLICE_ERROE
    新建全景时，切图失败

**[411x事件错误]
>
* 4111: MATTER_TYPE_ERROR 事件状态错误
* 4112: MATTER_TIMEOUT 交办超时，不能责任退回
* 4113: RIVER_REGION_ERROR 河流最高行政区设置错误

