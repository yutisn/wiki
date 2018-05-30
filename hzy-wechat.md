# 微信公众号涉及的接口设计
## 一 ArticleControler 新闻动态和政策方案 
>
1. 取得新闻动态列表,/article/newses,GET
    * 参数：regionId，行政区id
    * 返回：
        * OK，所属行政区的新闻动态列表
        * FAIL，行政区不存在
2. 取得政策法规列表，/article/laws, GET
    * 参数：regionId，行政区id
    * 返回：
        * OK，全国范围的政策法规+市级的政策法规列表  
        * FAIL，行政区id不存在
3. 取得新闻动态和政策法规详情,/article/article/{id},GET
    * 参数：id: 新闻动态id
    * 返回：
        * OK，新闻动态所有属性
        * FAIL，id不存在

## 二 StationController 测站
>
1. 取得测站列表：121.40.82.11:8080/stations，GET
    * 参数：regionId，行政区id
    * 返回：
        * OK,行政区下的所有测站，包含createDate(建立时间),instanceId(唯一编码),type(测站类型),address(安装位置),value(最新数据)
2. 取得仪表当日数据：121.40.82.11:8080/sensor/{code}, GET    
    * 参数：code，仪表编码
    * 返回：
        * OK，仪表当日数据
        * FAIL,仪表编码不存在

## 三 PanoramaController，全景
>
1. 取得全景列表，/panorama/lists,GET
    * 参数：regionId，行政区id
    * 返回：
        * OK，行政区下的全景列表,包含name，createDate(建立时间),instanceId(唯一编码),thumbUrl(缩略图)，coor(坐标)，address(位置)

## 四 ComplaintControler，投诉
>
1. 提交投诉,/complaint/submit,POST
    用户必须登录
    * 参数：
        * title：标题，必需
        * describe：描述，由几组关注信息自动组成的，必需
        * content：投诉内容，必需
        * images: 图片路径，最多五张图片，{image1:xx,image2:xxx,image3:xxx...}，图片必需
        * coor:由网页定位识别的经纬度，必需
        * address:由网页定位识别的位置，必需
        * riverSegmentId:选择的河段id，必需
        * riverSegmentName:选择的河段名，必需
        * name:投诉人姓名，可以使匿名
        * phone:投诉人电话，可以为空
    * 返回：
        * OK，建立成功，与登录的user关联
2. 取得投诉列表，/complaint/lists,GET
    用户必须登录
    * 参数：无
    * 返回：
        * OK，返回投诉列表，只需返回id，createDate, title，images，riverSegmentName, handleName, handleDate
3. 取得投诉详情，/complaint/{id},GET
    用户必须登录
    * 参数：id:投诉id
    * 返回：
        * OK，投诉所有属性
        * FAIL，id不存在
        * 4022，DATA_REFUSE，请求的投诉id不属于自己

## 五 HzUsrController 河长
>
1. 取得总河长，各级河长人数，/hzUser/master,GET
    * 参数：regionId，行政区id
    * 返回：
        * OK，{master:[xx,xx,xx],slave:[xx,xx,xx],cityNum:xx,countyNum:xx,townNum:xx,villageNum:xx}
2. 取得市级河长名录，/hzUser/cityLevel,GET
        * 参数：regionId，行政区id
        * OK，[{name:xx,riverSegments(管辖河段):[xx,xx,xx],type:xx}]
3. 取得县级级河长名录，/hzUser/countyLevel,GET
    * 参数：regionId，行政区id
    * 返回：
        * OK，[{name:xx,riverSegments(管辖河段):[xx,xx,xx],type:xx}]
4. 取得村级河长名录，/hzUser/townLevel,GET
    * 参数：regionId，行政区id
    * 返回：
        * OK，[{name:xx,riverSegments(管辖河段):[xx,xx,xx],type:xx}]   
5. 取得村级河长名录，/hzUser/villageLevel,GET
    * 参数：regionId，行政区id
    * 返回：
        * OK，[{name:xx,riverSegments(管辖河段):[xx,xx,xx],type:xx}] 



```
河长云相关图片路径：
    qqslimage/hzy/{regionId}/article，新闻
    qqslimage/hzy/{regionId}/river，河流
    qqslimage/hzy/{regionId}/Complaint/{userId}/，投诉
```
