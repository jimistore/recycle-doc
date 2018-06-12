# 提供给第三方

标签 ： 提供给第三方蜜估接口

---
# 回收估价模型 - 接口文档
## 1对接时序图
![时序图](img/seq.png)

## 2说明与约定
### 2.1 - 签名算法
为确保 - 接口访问安全， - 接口的请求和响应应对所有参数使用对称加密算法做签名校验。请求和响应均在header中加入签名参数。
 - Header参数:

|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|appId|应用唯一标识|varchar(32)|Y|蜜估提供|
|timestamp|时间戳|number(11)|Y|时区GMT+8以秒为单位的时间戳|
|signature|签名|varchar(32)|Y| - |

 - 签名算法:
 2. 把所有参数（包括appId、secret、timestamp）的key和拼成字符串放入到数组，得到 array = ['key2=value2','key1=value1']
 3. 把数组按照ascii码进行升序排序，得到 array = ['key1=value1','key2=value2']
 3. 把数组的元素用&拼成一个字符串，得到 source = 'key1=value1&key2=value2'
 4. 根据step3得到的source生成MD5加密值，并转成大写，生成签名。sign=toUpperCase(Md5(source))

### 2.2请求约定
 - 接口协议:https
 - 请求方式:post
 - 消息格式:application/json
 - 消息编码:UTF-8
 
 - 请求参数样例
```
{
  "id":"",
  "age":""
}
```

### 2.3响应
 - 消息格式:application/json
 - 消息编发:UTF-8

 - 成功响应参数结构:
```
{
  "code":"200",
  "data":{
     "age":"12"
  }
}
```

## 3 - 接口列表
### 3.1获取品类 - 接口
 - 接口：${api_domain}/api/recycle/proxy/category/list/v1
 - 请求参数：无
 - 响应参数:

|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|id|品类Id|varchar(32)|Y| - |
|name|品类名称|varchar(20)|Y| - |

 - 响应示例
```
{
    "code": "200",
	"data": [{
        	"id": "yihuigou_1",
        	"name": "手机"
        }, {
        	"id": "yihuigou_2",
        	"name": "平板"
        }, {
        	"id": "yihuigou_3",
        	"name": "笔记本"
        }, {
        	"id": "yihuigou_5",
        	"name": "数码/手表"
        }]
}
``` 

### 3.2品牌机型 - 接口
 - 接口：https://migu.jimistore.com/api/model/{品类Id}
 - 请求方式：get
 - 响应参数:
 
|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|id|品牌Id|varchar(32)|Y| - |
|name|品牌名称|varchar(20)|Y| - |
|listproduct|该品牌下的所有机型| [{}] |Y| - |

####listproduct

|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|id|产品Id|varchar(32)|Y| - |
|name|产品名称|varchar(20)|Y| - |
|image|产品图片链接|varchar(100)|Y| - |

 - 响应示例:
```
{
    "code":"200",
    "data": [{
    "id": "1_21",
    "name": "诺基亚",
    "listproduct": [{
    	"id": "5190",
    	"name": "诺基亚 6（TA-1000/全网通/64G）",
    	"image": "http://www.ehuigou.com/Public/Uploads/pic/phone/nokia_6.jpg"
        }]
    }]
}
```

### 3.3产品属性与属性值 - 接口
 - 接口：https://migu.jimistore.com/api/model/product/{产品Id}
 - 请求方式:get
 - 响应参数: 
 
|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|id|属性Id|varchar(32)|Y| - |
|name|属性名称|varchar(40)|Y| - |
|multi|是否多选|bool|Y| - |
|rqd|是否必选|bool|N| - |
|parentId|父级|varchar(32)|N| - |
|listOptions|属性值| [{}] |Y| - |

####listOptions

|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|id|属性值Id|varchar(32)|Y| - |
|name|属性值名称|varchar(40)|Y| - |
|dft|是否默认选中|bool|Y| - |
|parentId|属性值父级|varchar(32)|Y| - |
|extend|扩展信息| {} |Y|目前在笔记本估价专用|

 - 响应示例
```
{   
    "code":"200",
    "data": [{
        "id": "1001069",
        "name": "购买渠道",
        "multi": false,
        "listOptions": [{
        	"id": "10493",
        	"name": "大陆国行",
        	"dft": false
        }, {
        	"id": "10494",
        	"name": "香港行货",
        	"dft": false
        }]
    }]
}
```

### 3.4估价
 - 接口：${api_domain}/api/recycle/proxy/valuing/v1?_=1528278727351
 - 请求方式：post
 - 请求参数:
 
|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|categoryId|品类Id|varchar(32)|Y| - |
|brandId|品牌Id|varchar(32)|Y| - |
|productId|产品Id|varchar(32)|Y| - |
|businessPropList|属性与属性值信息| [{}] |Y| - |

####businessPropList

|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|propId|属性Id|varchar(32)|Y| - |
|optionId|属性值Id|[]|Y| - |
|extend|扩展信息| {} |N|目前在笔记本估价专用|

 - 请求示例:
```
{
	"categoryId": "yihuigou_3",
	"brandId": "3_1",
	"productId": "5262",
	"businessPropList": [{
		"propId": "5262_ConfModel",
		"optionId": ["124"],
		"extend": {
			"confMemory": "16GB（16GB×1）",
			"confConfig": 1,
			"confModel": "苹果 2016年 新款Macbook Pro 15英寸（MLH32CH/A）",
			"confHarddisk": "256GB",
			"confColor": "镁铝合金，银色，深空灰色",
			"confCamera": "720p FaceTime HD摄像头",
			"confProce": "Intel 酷睿i7 6700HQ",
			"confScreen": "15.4英寸",
			"confCard": "双显卡（入门级独立显卡＋集成显卡）",
			"confDrive": "无内置光驱"
		}
	}, {
		"propId": "6055",
		"optionId": ["16928"]
	}, {
		"propId": "6056",
		"optionId": ["16930"]
	}, {
		"propId": "6057",
		"optionId": ["16931"]
	}, {
		"propId": "6058",
		"optionId": ["16932"]
	}, {
		"propId": "6059",
		"optionId": ["16925"]
	}]
}
```
 - 响应参数:
 
|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|price|估价价格|Long|Y| 单位:分 |
|categoryId|品类Id|varchar(32)|Y| - |
|categoryName|品类名称|varchar(20)|Y| - |
|brandId|品类Id|varchar(32)|Y| - |
|brandName|品类名称|varchar(20)|Y| - |
|productId|产品Id|varchar(32)|Y| - |
|productName|产品名称|varchar(20)|Y| - |
|productImg|产品图片链接|varchar(100)|Y| - |
|valuingPropList|估价的属性| [{}] |Y| - |

####valuingPropList

|参数名|中文含义|类型|是否必填|备注|
|:----|:----|:---| :--: |:-:|:---------|
|propId|属性Id|Long|Y|单位:分|
|prop|属性名称|varchar(40)|Y| - |
|multi|是否多选|bool|Y| - |
|optionId|属性值|[]|Y| - |
|option|属性值名称|[]|Y| - | 
|extend|扩展信息| {} |N|目前在笔记本估价专用| 

 - 响应示例:
```
{
	"code": "200",
	"data": {
		"price": "106500",
		"categoryId": "yihuigou_1",
		"brandId": "1_1",
		"brandName": "苹果",
		"productId": "1818",
		"productName": "苹果 iPhone 6s",
		"productImg": "http://www.ehuigou.com/Public/Uploads/pic/phone/apple_iphone6s.jpg"
		"valuingPropList": [{
			"propId": "1000404",
			"prop": "购买渠道",
			"optionId": ["7962"],
			"option": ["大陆国行"]
		}, {
			"propId": "1000405",
			"prop": "颜色",
			"optionId": ["7969"],
			"option": ["白色"]
		}, {
			"propId": "1000406",
			"prop": "存储容量",
			"optionId": ["7971"],
			"option": ["16G"]
		}, {
			"propId": "1000407",
			"prop": "版本/型号",
			"optionId": ["7975"],
			"option": ["A1700"]
		}, {
			"propId": "8535",
			"prop": "国内保修情况",
			"optionId": ["34355"],
			"option": ["保修一个月以上"]
		}, {
			"propId": "8536",
			"prop": "边框背板",
			"optionId": ["34390"],
			"option": ["全新原封机"]
		}, {
			"propId": "8537",
			"prop": "屏幕外观",
			"optionId": ["34392"],
			"option": ["屏幕完好"]
		}, {
			"propId": "8538",
			"prop": "屏幕性能",
			"optionId": ["34393"],
			"option": ["屏幕性能完好"]
		}, {
			"propId": "8539",
			"prop": "icloud是否注销",
			"optionId": ["34396"],
			"option": ["icloud已注销"]
		}, {
			"propId": "8540",
			"prop": "拆修情况",
			"optionId": ["34394"],
			"option": ["无拆修"]
		}, {
			"propId": "8541",
			"prop": "存在以下问题",
			"optionId": [],
			"option": []
		}]
	}
}
```