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

**[401x标识和session相关错误]**
>
*   4010: UNAUTHORIZED
    即“未认证”，即用户没有必要的凭据。该状态码表示当前请求需要用户验证。
*   4011: NO_SESSION
    无SESSION，即服务器端对应SESSION已经失效或删除，客户端无法连接，必须重新登录。

>   [402x标识和必须数据有关错误]
*   4020: DATA_EXIST
    数据已存在，即要添加数据已经存在，不能重复添加，比如此手机号已注册，再次注册产生这个错误。
*   4021：DATA_NOEXIST
    数据不存在，无法继续执行操作，比如坐标上传时，根据客户端发送的项目
    id，数据库查询不到项目；再比如web端登陆时，根据code查询不到用户，
    返回这个错误。
*   4022: DATA_REFUSE
    请求的数据不属于自己，拒绝操作，比如删除不是自己的项目,请求不时自己的订单,不是自己的测站等操作。

**[403x千寻错误]**
>
*   4030: QXWE_EXPIRED
    千寻过期，千寻服务时间过期，请求时返回。

**[404x标识验证码相关错误]**
>
*   4040 CODE_NEED
    需要验证码，比如web端第一次登录，或登录过，但是15天内没有登陆过，再次登录时产生这个错误。
*   4041: CODE_INVALID
    验证码过期，需要重新获取，验证码一般只有5-10分钟的有效期，超过这个时间，验证码需要重新获取。
*   4042: CODE_ERROR
    验证码输入错误，请重新提交。

**[405x标识套餐错误]**
>
*   4050: PACKAGE_EXPIRED
    套餐已过期，无法提供服务，比如无法上传文件、无法修改要素等操作，套餐必须要续费。
*   4051: PACKAGE_LIMIT
    套餐限制，不允许执行，比如空间已满或流量用尽，不允许上传文件；新建
    项目数达到上限，不允许建立项目。
*   4052: PACKAGE_NOALLOW_BUY
    套餐不满足购买条件，比如空间大小,子账户数已超过套餐限制,无法购买。

**[406x表示认证错误]**
>
*   4060: CERTIFY_NO_PERSONAL
    未进行实名认证，无法购买套餐等操作,或未进行实名认证,直接进行企业认
    证也返回这个错误。
*   4061: CERTIFY_NO_COMPANY
    未进行企业认证，无法购买高级套餐，购买数据服务。

**[407x坐标相关错误]**
>
*   4070: COOR_PROJECT_NO_CENTER
    项目中心未设置，上传坐标时，返回这个错误。
*   4071: COOR_BUILD_CENTER_ERROR  
    上传的坐标excel中建筑物中心点或定位点格式错误，无法添加建筑物。
*   4072: COOR_FORMAT_ERROR
    上传的坐标excel文件格式错误，文件损坏，excel文件格式不是预期的，excel数据不是预期的。

。