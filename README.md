# �ṩ��������

��ǩ �� �ṩ���������۹��ӿ�

---
#1.�۹���ع��۽ӿ�

###1.1ǩ���㷨
Ϊȷ���ӿڷ��ʰ�ȫ���ӿڵ��������ӦӦ�����в���ʹ�öԳƼ����㷨��ǩ��У�顣�������Ӧ����header�м���ǩ��������
Header����:
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|appId|Ӧ��Ψһ��ʶ|String|Y|�۹��ṩ| |
|timestamp|ʱ���|String|Y|ʱ��GMT+8����Ϊ��λ��ʱ���| |
|signature|ǩ��|String|Y|| |
ǩ���㷨:
 1. �����в���������appId��secret��timestamp����key��ƴ���ַ������뵽���飬�õ� array = ['key2=value2','key1=value1']
 2. �����鰴��ascii������������򣬵õ� array = ['key1=value1','key2=value2']
 3. �������Ԫ����&ƴ��һ���ַ������õ� source = 'key1=value1&key2=value2'
 4. ����step3�õ���source����MD5����ֵ����ת�ɴ�д������ǩ����sign=toUpperCase(Md5(source))

###1.2����Լ��
 - ${api_domain} = recycle-api.jimistore.com
 - �ӿ�Э��:https
 - ����ʽ:post
 - ��Ϣ��ʽ:application/json
 - ��Ϣ����:UTF-8

�����������

    {
      "id":"",
      "age":""
    }

###1.3��Ӧ
 - ��Ϣ��ʽ:application/json
 - ��Ϣ�෢:UTF-8

�ɹ���Ӧ�����ṹ:

    {
      "code":"200",
      "data":{
         "age":"12"
      }
    }

###1.4��ȡƷ��ӿ�
�ӿڣ�${api_domain}/api/recycle/proxy/category/list/v1
�����������
��Ӧ����:
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|id|Ʒ��Id|String|Y|| |
|name|Ʒ������|String|Y|| |
��Ӧʾ��

    {
	    "code": "200",
    	"data": [{
    		"id": "yihuigou_1",
    		"name": "�ֻ�"
    	}, {
    		"id": "yihuigou_2",
    		"name": "ƽ��"
    	}, {
    		"id": "yihuigou_3",
    		"name": "�ʼǱ�"
    	}, {
    		"id": "yihuigou_5",
    		"name": "����/�ֱ�"
    	}]
    }

###1.5Ʒ�ƻ��ͽӿ�
�ӿڣ�https://migu.jimistore.com/api/model/{Ʒ��Id}
����ʽ��get
��Ӧ����:
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|id|Ʒ��Id|String|Y|| |
|name|Ʒ������|String|Y|| |
|listproduct|��Ʒ���µ����л���|List|Y|| |

####listproduct
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|id|��ƷId|String|Y|| |
|name|��Ʒ����|String|Y|| |
|image|��ƷͼƬ����|String|Y|| |
��Ӧʾ��:

    [{
        "id": "1_21",
        "name": "ŵ����",
        "listproduct": [{
        	"id": "5190",
        	"name": "ŵ���� 6��TA-1000/ȫ��ͨ/64G��",
        	"image": "http://www.ehuigou.com/Public/Uploads/pic/phone/nokia_6.jpg"
        }]
	}]


###1.6��Ʒ����������ֵ�ӿ�
�ӿڣ�https://migu.jimistore.com/api/model/product/{��ƷId}
����ʽ:get
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|id|����Id|String|Y|| |
|name|��������|String|Y|| |
|multi|�Ƿ��ѡ|Boolean|Y|| |
|rqd|�Ƿ��ѡ|Boolean|N|| |
|parentId|����|String|N|| |
|listOptions|����ֵ|List|Y|| |
####listOptions
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|id|����ֵId|String|Y|| |
|name|����ֵ����|String|Y|| |
|dft|�Ƿ�Ĭ��ѡ��|Boolean|Y|| |
|parentId|����ֵ����|String|Y|| |
|extend|��չ��Ϣ|Map|Y|Ŀǰ�ڱʼǱ�����ר��||
��Ӧʾ��

    [{
	"id": "1001069",
	"name": "��������",
	"multi": false,
	"listOptions": [{
		"id": "10493",
		"name": "��½����",
		"dft": false
	}, {
		"id": "10494",
		"name": "����л�",
		"dft": false
	}]
}]
###1.7����
�ӿڣ�${api_domain}/api/recycle/proxy/valuing/v1?_=1528278727351
����ʽ��post
�������:
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|categoryId|Ʒ��Id|String|Y|| |
|brandId|Ʒ��Id|String|Y|| |
|productId|��ƷId|String|Y|| |
|businessPropList|����������ֵ��Ϣ|List|Y|| |
####businessPropList
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|propId|����Id|String|Y|| |
|optionId|����ֵId|String[]|Y|| |
|extend|��չ��Ϣ|Map|N|Ŀǰ�ڱʼǱ�����ר��| |
����ʾ��:

    {
	"categoryId": "yihuigou_3",
	"brandId": "3_1",
	"productId": "5262",
	"businessPropList": [{
		"propId": "5262_ConfModel",
		"optionId": ["124"],
		"extend": {
			"confMemory": "16GB��16GB��1��",
			"confConfig": 1,
			"confModel": "ƻ�� 2016�� �¿�Macbook Pro 15Ӣ�磨MLH32CH/A��",
			"confHarddisk": "256GB",
			"confColor": "þ���Ͻ���ɫ����ջ�ɫ",
			"confCamera": "720p FaceTime HD����ͷ",
			"confProce": "Intel ���i7 6700HQ",
			"confScreen": "15.4Ӣ��",
			"confCard": "˫�Կ������ż������Կ��������Կ���",
			"confDrive": "�����ù���"
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
��Ӧ����:
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|price|���ۼ۸�|Long|Y|��λ:��| |
|categoryId|Ʒ��Id|String|Y|| |
|categoryName|Ʒ������|String|Y|| |
|brandId|Ʒ��Id|String|Y|| |
|brandName|Ʒ������|String|Y|| |
|productId|��ƷId|String|Y|| |
|productName|��Ʒ����|String|Y|| |
|productImg|��ƷͼƬ����|String|Y|| |
|valuingPropList|���۵�����|List|Y|| |
####valuingPropList
|������|���ĺ���|����|�Ƿ����|��ע|
|:----|:----|:---| :--: |:-:|:---------|
|propId|����Id|Long|Y|��λ:��| |
|prop|��������|String|Y|| |
|multi|�Ƿ��ѡ|String|Y|| |
|optionId|����ֵ|String[]|Y|| |
|option|����ֵ����|String[]|Y|| |
|extend|��չ��Ϣ|Map|N|Ŀǰ�ڱʼǱ�����ר��| |
��Ӧʾ��:

     {
        "categoryId": "yihuigou_3",
        "brandId": "3_1",
        "productId": "5262",
        "businessPropList": [{
        	"propId": "5262_ConfModel",
        	"optionId": ["124"],
        	"optionName": ["��MLH32CH/A��"],
        	"multi": false,
        	"extend": {
        		"confMemory": "16GB��16GB��1��",
        		"confConfig": 1,
        		"confModel": "ƻ�� 2016�� �¿�Macbook Pro 15Ӣ�磨MLH32CH/A��",
        		"confHarddisk": "256GB",
        		"confColor": "þ���Ͻ���ɫ����ջ�ɫ",
        		"confCamera": "720p FaceTime HD����ͷ",
        		"confProce": "Intel ���i7 6700HQ",
        		"confScreen": "15.4Ӣ��",
        		"confCard": "˫�Կ������ż������Կ��������Կ���",
        		"confDrive": "�����ù���"
        	}
        }, {
        	"propId": "6055",
        	"optionId": ["16928"],
        	"optionName": ["������������"],
        	"multi": false
        }, {
        	"propId": "6056",
        	"optionId": ["16930"],
        	"optionName": ["������"],
        	"multi": false
        }, {
        	"propId": "6057",
        	"optionId": ["16931"],
        	"optionName": ["��Ļ������"],
        	"multi": false
        }, {
        	"propId": "6058",
        	"optionId": ["16932"],
        	"optionName": ["��Ļ��ʾ����"],
        	"multi": false
        }, {
        	"propId": "6059",
        	"optionId": ["16925"],
        	"optionName": ["�������/�����쳣"],
        	"multi": true
        }],
        "channelId": "h5"
        }




