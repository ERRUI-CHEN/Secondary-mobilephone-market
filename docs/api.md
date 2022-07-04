## 练习接口文档及相关说明

- 主色调范围：**#30cfd0→#330867**

- 有些post接口是application/x-www-form-urlencoded，用的方法是myRequestPost2（），接口类型是application/json，用的方法是myRequestPost（）

- 页面5和6用的URI是baseUrl2，方法是myRequestGet2（）

- ```js
  //遇到的问题
  1.TypeError: getDetailInfo() is not a function：getDetailInfo接口没有写到method模块里
  2.常见问题接口，data[{.id=286..},{...},{...}],二维数组解决方法
  this.probleminfo =res.data
  
  <view v-for="(item,index) in probleminfo" :key="item" v-if="index<10">
  {{index+1}}.{{item.title}}//完成遍历
  </view>
  3.轮播图接口
  this.lunboinfo = res.data.goods.skuImageList
  <swiper-item v-for="item in lunboinfo" :key="item">		
  	<image :src="item"></image>
  </swiper-item>
  4.语法错误: Unexpected token, expected "," (20:1)，没有注意模块用，隔开
  5.对于接口数据多级遍历可以使用v-for二次遍历的方法
  <view  v-for="(item,index) in pic" :key='item'>
  <view v-for="(item,index) in item.tags">
  <text>{{index}}---{{item}}</text>
  </view>
  </view>
  6.小程序无法跳转，取消hbuilder中的小程序位置接口
  7.固定底部样式方法：position: absolute;
  		position:fixed;
  		bottom:0;
  8.跳转手机联系录：methods: {
  			tel:function(){
  				uni.makePhoneCall({
  					phoneNumber:"4001806996"
  				})
  			},}
  <view class="anniu" @click="tel">联系我们</view>
  9.post接口application/x-www-form-urlencoded需要添加参数才能调用
  10.sourcetree分支上传问题
  11.错误：does not have a method "showToast" to handle event "tap".
  12.uniapp 开发微信小程序 app.json未找到问题：使用微信开发者工具打开小程序项目的时候，选择【mp-weixin】文件夹，让app.json文件暴露在最外层。"miniprogramRoot":"./unpackage/dist/dev/mp-weixin"
  ```

## 1.index主页

### 1.轮播图接口

接口地址：/sapi/gateway/shs-mall-api/v1/main-page/cache-info?channelId=79595&modelId=20

请求方式：GET

参数：无

数据格式：

```json
{
  "success": true,
  "code": 0,
  "data": {
    "bsBannerList": [
      {
        "bannerid": 10071,
        "bannername": "微信端每周推荐",
        "orderid": 0,
        "channelid": 79595,
        "begintm": 1612368000000,
        "endtm": 1638201600000,
        "status": 1,
        "modelid": 20,
        "bannerurl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2021-02-04/50a397bc-b102-45f2-9ef8-cc6f5163aba7.png",
        "jumpurl": "/pages/product-level/index",
        "v2jumpurl": "/pages/product-level/index",
        "updatetm": 1612409689000,
        "createtm": 1612407407000,
        "backgroundColor": "#3046C1"
      }
    ]
  }
}
```

### 2.每日特价接口

接口地址：/sapi/gateway/shs-mall-api/v1/goods/goods-list/page-info

请求方式：POST——application/x-www-form-urlencoded

参数：

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "prdId": 5315,
            "prdName": "小米10 青春版",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-27/16064b01-e8fd-4c81-b030-c2063e4b860a.jpg",
            "shopName": "【二手9成新】 小米10 青春版 全网通 8G+256G 白桃乌龙 国行",
            "skuCode": "20072093434",
            "sellingPrice": 1569,
            "stockNum": 1,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/110/5315/1.jpg",
            "views": 17140,
            "sort": 0,
            "minPrice": 1569,
            "saleNum": 5,
            "updatetm": 1618392451000,
            "firstOnShelfTime": 1596270243000
        },
        {
            "prdId": 5096,
            "prdName": "Redmi K30",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-12-25/2826ed3d-4648-4298-9121-89347c865fd7.jpg",
            "shopName": "【二手9成新】 Redmi K30 全网通 8G+128G 紫玉幻境 国行",
            "skuCode": "20021879304",
            "sellingPrice": 1039,
            "stockNum": 1,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/110/5096/1.jpg",
            "views": 9610,
            "sort": 0,
            "minPrice": 1039,
            "saleNum": 18,
            "updatetm": 1613728122000,
            "firstOnShelfTime": 1591264986000
        },
        {
            "prdId": 5677,
            "prdName": "Redmi K30 至尊纪念版",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-26/7e3c79f0-223d-4371-8280-23189a7bb105.png",
            "shopName": "【二手95新】 Redmi K30 至尊纪念版 全网通 8G+128G 薄荷绿 国行",
            "skuCode": "20100998692",
            "sellingPrice": 1499,
            "stockNum": 1,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/110/5677/1.jpg",
            "views": 5164,
            "sort": 0,
            "minPrice": 1399,
            "saleNum": 7,
            "updatetm": 1618392451000,
            "firstOnShelfTime": 1603074637000
        }
    ]
}
```

### 3.首页猜你喜欢接口

#### 1.猜你喜欢

接口地址：/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type

请求方式：POST——application/json

参数：

"totalPage": 16,
"totalCount": 91,

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "totalPage": 16,
        "totalCount": 91,
        "list": [
            {
                "prdId": 4932,
                "prdName": "iPhone 11",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 128G 黑色 有保一个月以上 国行",
                "skuCode": "19122877082",
                "sellingPrice": 3949,
                "prdSaleType": 1,
                "views": 221460,
                "smlCoupon": {
                    "id": 188,
                    "shopCode": "ALIPAYSHOP",
                    "couponName": "100元优惠劵",
                    "couponPrice": 100,
                    "rulesJson": "{\"maxLimit\":\"100\",\"recycleMaxLimit\":0,\"ticketType\":\"2\",\"prdLimit\":\"4932,5109,5201,6399\"}",
                    "couponDesc": "新人领券满100减100",
                    "type": 1,
                    "delayTime": 3,
                    "timeType": 0,
                    "createUser": "何都威",
                    "createtm": 1620789820000,
                    "updatetm": 1620789837000,
                    "category": 1,
                    "receviedUrl": "alipays://platformapi/startapp?appId=2018060760255864&page=pages-activity/discount-coupon/discount-coupon?actId=20210512",
                    "receiveNum": 0,
                    "actId": 20210512,
                    "actType": 5,
                    "begindt": 1620748800000,
                    "expiredt": 1621612800000,
                    "canUse": true,
                    "checkFailReason": "该优惠券可以正常使用",
                    "fitVos": [
                        {
                            "skuCode": "201026100147",
                            "couponId": 188,
                            "canUse": true
                        }
                    ]
                }
            },
            {
                "prdId": 3159,
                "prdName": "iPhone 8 plus",
                "prdImgUrl": "//shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2017-12-20/384a66a2-29e3-49b6-9222-e520695a2edb.jpg",
                "shopName": "【二手9成新】iPhone 8 plus A1864 64G 深空灰 无保或有保一个月以下 国行",
                "skuCode": "19082564396",
                "sellingPrice": 1849,
                "prdSaleType": 1,
                "views": 119746
            },
            {
                "prdId": 4097,
                "prdName": "iPhone XS Max",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-11-14/2b42bf4b-1124-406e-9ddd-a45dc5d292b7.jpg",
                "shopName": "二手9成新|iPhone XS Max|A2104|64G|金色|无保或有保一个月以下|国行",
                "skuCode": "19083165086",
                "sellingPrice": 3139,
                "prdSaleType": 1,
                "views": 108845
            },
            {
                "prdId": 4113,
                "prdName": "iPhone XR",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-11-14/58b59b8a-aca3-4abb-9ab9-09b572b1d9e4.png",
                "shopName": "【二手9成新】 iPhone XR A2108 128G 红色 无保或有保一个月以下 国行",
                "skuCode": "20022479544",
                "sellingPrice": 2839,
                "prdSaleType": 1,
                "views": 87457
            },
            {
                "prdId": 4933,
                "prdName": "iPhone 11 Pro",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/97b24243-7228-4bc6-a742-39d9c72d6624.png",
                "shopName": "【二手95新】 iPhone 11 Pro A2217 64G 金色 有保一个月以上 国行",
                "skuCode": "19101168386",
                "sellingPrice": 4669,
                "prdSaleType": 1,
                "views": 79067
            },
            {
                "prdId": 2682,
                "prdName": "iPhone 7 Plus",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-09-15/a113fc6c-4cdf-4c9d-8293-fc1458d41421.png",
                "shopName": "【二手9成新】iPhone 7 Plus A1661 32G 银色 无保或有保一个月以下 国行",
                "skuCode": "19082864742",
                "sellingPrice": 1209,
                "prdSaleType": 1,
                "views": 53875,
                "sort": 1
            }
        ]
    }
}
```

#### 2.手机

接口地址：/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type

请求方式：POST——application/json

参数：

"totalPage": 14,
"totalCount": 83,

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "totalPage": 14,
        "totalCount": 83,
        "list": [
            {
                "prdId": 2682,
                "prdName": "iPhone 7 Plus",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-09-15/a113fc6c-4cdf-4c9d-8293-fc1458d41421.png",
                "shopName": "【二手9成新】iPhone 7 Plus A1661 32G 银色 无保或有保一个月以下 国行",
                "skuCode": "19082864742",
                "sellingPrice": 1209,
                "prdSaleType": 1,
                "views": 53876,
                "sort": 1
            },
            {
                "prdId": 3159,
                "prdName": "iPhone 8 plus",
                "prdImgUrl": "//shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2017-12-20/384a66a2-29e3-49b6-9222-e520695a2edb.jpg",
                "shopName": "【二手9成新】iPhone 8 plus A1864 64G 深空灰 无保或有保一个月以下 国行",
                "skuCode": "19082564396",
                "sellingPrice": 1849,
                "prdSaleType": 1,
                "views": 119747
            },
            {
                "prdId": 3195,
                "prdName": "华为 Mate10",
                "prdImgUrl": "//shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2017-12-20/e46c7408-5e76-4a41-a6c6-15dbd37057ae.jpg",
                "shopName": "【二手9成新】 华为 Mate10 全网通 6G+128G 亮黑色 国行",
                "skuCode": "20051689051",
                "sellingPrice": 869,
                "prdSaleType": 1,
                "views": 2715
            },
            {
                "prdId": 3499,
                "prdName": "小米8",
                "prdImgUrl": "//shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-06-22/190a2fb9-d1b3-471c-a683-2df425f35170.jpeg",
                "shopName": "【二手9成新】小米8 6G+64G 黑色 国行",
                "skuCode": "19082664517",
                "sellingPrice": 899,
                "prdSaleType": 1,
                "views": 29660
            },
            {
                "prdId": 3557,
                "prdName": "华为 Nova3",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-11-15/c77af912-3177-4d76-8825-4ed88b2bca01.png",
                "shopName": "【二手9成新】华为 Nova3 全网通 6G+128G 樱草金 国行",
                "skuCode": "19082964826",
                "sellingPrice": 799,
                "prdSaleType": 1,
                "views": 256
            },
            {
                "prdId": 3619,
                "prdName": "荣耀 Note10",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-11-14/e2aa2212-b456-4d54-8653-24bde3fb5a16.png",
                "shopName": "【二手9成新】 荣耀 Note10 6G+128G 蓝色 国行",
                "skuCode": "20080794595",
                "sellingPrice": 1079,
                "prdSaleType": 1,
                "views": 446
            }
        ]
    }
}
```

#### 3.平板电脑

接口地址：/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type

请求方式：POST——application/json

参数：

"totalPage": 2,
"totalCount": 7,

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "totalPage": 2,
        "totalCount": 7,
        "list": [
            {
                "prdId": 2694,
                "prdName": "iPad mini4",
                "prdImgUrl": "/ued/base/image/product/apple_mini4.jpg",
                "shopName": "【二手9成新】 iPad mini4 128G 黑色 WIFI 版 无保或有保一个月以下 国行",
                "skuCode": "20030279972",
                "sellingPrice": 1569,
                "prdSaleType": 2,
                "views": 3712
            },
            {
                "prdId": 3457,
                "prdName": "iPad (6th generation)",
                "prdImgUrl": "//shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-07-23/afcd14da-73e4-42e3-80c9-81ad57c43d12.jpg",
                "shopName": "【二手9成新】 iPad (6th generation) 128G 白色 WIFI 版 无保或有保一个月以下 国行",
                "skuCode": "20031282421",
                "sellingPrice": 1899,
                "prdSaleType": 2,
                "views": 5692
            },
            {
                "prdId": 4771,
                "prdName": "iPad mini5",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-07-19/99122d78-e401-43fc-bdde-0d78bc6a39f1.png",
                "shopName": "【二手9成新】 iPad mini5 WiFi 64G 灰色 无保或有保一个月以下 国行",
                "skuCode": "20042287354",
                "sellingPrice": 1999,
                "prdSaleType": 2,
                "views": 3469
            },
            {
                "prdId": 4787,
                "prdName": "iPad Air3",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-07-19/11e7e1b3-e3d0-4bcd-8a6f-f51c0cd11148.png",
                "shopName": "【二手9成新】 iPad Air3 64G 金色 WIFI 版 无保或有保一个月以下 国行",
                "skuCode": "20100698495",
                "sellingPrice": 2799,
                "prdSaleType": 2,
                "views": 1532
            },
            {
                "prdId": 4962,
                "prdName": "iPad (7th generation)",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-10-22/16dd6cce-c39a-4f86-911e-9572f8d96741.png",
                "shopName": "【二手9成新】 iPad (7th generation) WiFi 32G 银色 有保一个月以上 国行",
                "skuCode": "20080794662",
                "sellingPrice": 1869,
                "prdSaleType": 2,
                "views": 2064
            },
            {
                "prdId": 5855,
                "prdName": "iPad Air4",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2021-03-31/23893f9c-d110-4188-91fc-4c801424ce8e.png",
                "shopName": "【二手9成新】 iPad Air4 64G 深空灰色 WIFI 版 有保一个月以上 国行",
                "skuCode": "210204107183",
                "sellingPrice": 3799,
                "prdSaleType": 2,
                "views": 1055
            }
        ]
    }
}
```

#### 4.手机周边

接口地址：/sapi/gateway/shs-mall-api/v1/goods/get-good-by-type

请求方式：POST——application/json

参数：

"totalPage": 1,
"totalCount": 1,

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "totalPage": 1,
        "totalCount": 1,
        "list": [
            {
                "prdId": 5214,
                "prdName": "苹果奇门纳福手机壳",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-03-02/6f57fa4c-3e23-4120-b547-93cf99ba7611.png",
                "shopName": "【新品】 苹果奇门纳福手机壳 iPhoneXS Max",
                "skuCode": "20030279987",
                "sellingPrice": 39,
                "prdSaleType": 0,
                "views": 321
            }
        ]
    }
}
```

## 2.search搜索

### 1.搜索页

- **大家都在搜**

接口地址：/sapi/gateway/shs-mall-api/v1/log-buried-point/find-user-browse-info

请求方式：POST——application/json

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "prdName": "iPhone 11",
            "skuCode": "19101368522",
            "prdId": 4932
        },
        {
            "prdName": "iPhone 11 Pro",
            "skuCode": "19101168386",
            "prdId": 4933
        },
        {
            "prdName": "iPhone 12",
            "skuCode": "201202103413",
            "prdId": 5862
        },
        {
            "prdName": "iPhone XR",
            "skuCode": "19071158069",
            "prdId": 4113
        },
        {
            "prdName": "iPhone XS Max",
            "skuCode": "19061852333",
            "prdId": 4097
        },
        {
            "prdName": "iPhone 8 plus",
            "skuCode": "19061852230",
            "prdId": 3159
        },
        {
            "prdName": "华为 P40 Pro",
            "skuCode": "20051589002",
            "prdId": 5236
        },
        {
            "prdName": "小米10 青春版",
            "skuCode": "20052289684",
            "prdId": 5315
        },
        {
            "prdName": "iPhone 12 mini",
            "skuCode": "201130103267",
            "prdId": 5865
        },
        {
            "prdName": "小米9",
            "skuCode": "19071158083",
            "prdId": 4559
        }
    ]
}
```

### 2.搜索结果页

#### 1.筛选

##### 1.品牌

接口地址：/sapi/gateway/shs-mall-api/v1/brand/find-brand-data?prdSaleType=1&shopCode=alipayshop

请求方式：GET

参数：brandId

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "brandList": [
            {
                "brandId": 6001,
                "brandName": "IPad",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 2
            },
            {
                "brandId": 20,
                "brandName": "三星",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 1
            },
            {
                "brandId": 360,
                "brandName": "荣耀",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 1
            },
            {
                "brandId": 10,
                "brandName": "苹果",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 1
            },
            {
                "brandId": 100,
                "brandName": "华为",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 1
            },
            {
                "brandId": 110,
                "brandName": "小米",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 1
            },
            {
                "brandId": 40,
                "brandName": "OPPO",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 1
            },
            {
                "brandId": 50,
                "brandName": "vivo",
                "shopCode": "ALIPAYSHOP",
                "prdSaleType": 1
            }
        ]
    }
}
```

##### 2.机型

接口地址：/sapi/gateway/shs-mall-api/v1/model/model-list

请求方式：POST——application/json

参数：brandId: 6001,（ipad）

​						20（三星）

​						360（荣耀）

​						10（苹果）

​						100（华为）

​						110（小米）

​						40（oppo）

​						50（vivo)

数据格式：（以IPAD为例子）

```json
{
    "success": true,
    "code": 0,
    "data": {
        "modelList": [
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 6001,
                "brandName": "IPad",
                "prdId": 5856,
                "prdName": "iPad (8th generation)",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2021-03-31/4bea286d-3573-4de0-a75e-76128d1ea24b.png",
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/2/6001/5856/1.jpg",
                "stockNum": 4,
                "minPrice": 2349,
                "skuCode": "201119102353",
                "tags": "",
                "version": 128621,
                "prdSaleType": 2
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 6001,
                "brandName": "IPad",
                "prdId": 5855,
                "prdName": "iPad Air4",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2021-03-31/23893f9c-d110-4188-91fc-4c801424ce8e.png",
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/2/6001/5855/1.jpg",
                "stockNum": 3,
                "minPrice": 3799,
                "skuCode": "210204107183",
                "tags": "",
                "version": 128621,
                "prdSaleType": 2
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 6001,
                "brandName": "IPad",
                "prdId": 4771,
                "prdName": "iPad mini5",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-07-19/99122d78-e401-43fc-bdde-0d78bc6a39f1.png",
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/2/10/4771/1.jpg",
                "stockNum": 4,
                "minPrice": 1999,
                "skuCode": "20042287354",
                "tags": "",
                "version": 128621,
                "productGroup": " 50",
                "prdSaleType": 2
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 6001,
                "brandName": "IPad",
                "prdId": 2694,
                "prdName": "iPad mini4",
                "prdImgUrl": "/ued/base/image/product/apple_mini4.jpg",
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/2/10/2694/1.jpg",
                "stockNum": 1,
                "minPrice": 1569,
                "skuCode": "20030279972",
                "tags": "",
                "version": 128621,
                "productGroup": " 50 39",
                "prdSaleType": 2
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 6001,
                "brandName": "IPad",
                "prdId": 4962,
                "prdName": "iPad (7th generation)",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-10-22/16dd6cce-c39a-4f86-911e-9572f8d96741.png",
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/2/6001/4962/1.jpg",
                "stockNum": 1,
                "minPrice": 1869,
                "skuCode": "20080794662",
                "tags": "平板电脑专题",
                "version": 128621,
                "productGroup": "",
                "prdSaleType": 2
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 6001,
                "brandName": "IPad",
                "prdId": 3457,
                "prdName": "iPad (6th generation)",
                "prdImgUrl": "//shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-07-23/afcd14da-73e4-42e3-80c9-81ad57c43d12.jpg",
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/2/10/3457/1.jpg",
                "stockNum": 2,
                "minPrice": 1899,
                "skuCode": "20031282421",
                "tags": "平板电脑专题",
                "version": 128621,
                "productGroup": " 50",
                "prdSaleType": 2
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 6001,
                "brandName": "IPad",
                "prdId": 4787,
                "prdName": "iPad Air3",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-07-19/11e7e1b3-e3d0-4bcd-8a6f-f51c0cd11148.png",
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/2/6001/4787/1.jpg",
                "stockNum": 2,
                "minPrice": 2799,
                "skuCode": "20100698495",
                "tags": "平板电脑专题",
                "version": 128621,
                "productGroup": "",
                "prdSaleType": 2
            }
        ]
    }
}
```

#### 2.结果数据

接口地址：/sapi/gateway/shs-mall-api/v1/goods/get-goods-info-v2

请求方式：POST——application/json

参数：brandOrPrd——vivo，苹果，三星，荣耀，华为，IPad，小米，OPPO

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "goodsList": [
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 10,
                "brandName": "苹果",
                "prdId": 4933,
                "prdName": "iPhone 11 Pro",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/97b24243-7228-4bc6-a742-39d9c72d6624.png",
                "shopName": "【二手95新】 iPhone 11 Pro A2217 64G 金色 有保一个月以上 国行",
                "skuCode": "19101168386",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4933/1.jpg",
                "tags": "热销机型,苹果手机",
                "sellingPrice": 4669,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 79076,
                "prdStatus": 1,
                "mainImage": ""
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 10,
                "brandName": "苹果",
                "prdId": 4932,
                "prdName": "iPhone 11",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 128G 白色 有保一个月以上 国行",
                "skuCode": "20010277587",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1.jpg",
                "tags": "今日特价,以旧换新,热销机型,苹果手机",
                "sellingPrice": 3949,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 221478,
                "prdStatus": 1,
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg"
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 360,
                "brandName": "荣耀",
                "prdId": 4841,
                "prdName": "荣耀20",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-07-19/872f8f77-9c7e-4bc4-8eb8-d59bb31e7081.png",
                "shopName": "【二手9成新】 荣耀20 全网通 8G+128G 幻夜黑 国行",
                "skuCode": "20021579230",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/360/4841/1.jpg",
                "tags": "安卓手机,热销机型",
                "sellingPrice": 1389,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 2265,
                "prdStatus": 1,
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-19/153e4dfb-cb15-42ca-9f90-9e0e52225f4c.jpg"
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 10,
                "brandName": "苹果",
                "prdId": 4113,
                "prdName": "iPhone XR",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-11-14/58b59b8a-aca3-4abb-9ab9-09b572b1d9e4.png",
                "shopName": "【二手9成新】 iPhone XR A2108 128G 红色 无保或有保一个月以下 国行",
                "skuCode": "20022479544",
                "totalUsableNum": 3,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4113/1.jpg",
                "tags": "热销机型,苹果手机",
                "sellingPrice": 2839,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 87462,
                "prdStatus": 1,
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/407caae4-3480-4920-9482-9fc75be2a4a2.jpg"
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 360,
                "brandName": "荣耀",
                "prdId": 5285,
                "prdName": "荣耀30",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-28/afd6caa5-8b12-449e-964a-f3a08e6f478f.png",
                "shopName": "【二手9成新】 荣耀30 全网通 8G+128G 钛空银 国行",
                "skuCode": "20070392511",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/360/5285/1.jpg",
                "tags": "",
                "sellingPrice": 2099,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 2909,
                "prdStatus": 1,
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-21/101f81c2-b8dc-4b05-a7d5-b6727e9f4271.jpg"
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 360,
                "brandName": "荣耀",
                "prdId": 5392,
                "prdName": "荣耀 X10",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-27/8aa506cd-6b48-472e-8975-b3195514ff41.png",
                "shopName": "【二手9成新】 荣耀 X10 全网通 8G+128G 光速银 国行",
                "skuCode": "20080294371",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/360/5392/1.jpg",
                "tags": "",
                "sellingPrice": 1689,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 4954,
                "prdStatus": 1,
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/d06206cb-ffe2-49eb-8fc8-be02fd8e7444.jpg"
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 110,
                "brandName": "小米",
                "prdId": 6287,
                "prdName": "Redmi Note9 Pro",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-12-28/a0202481-0b8d-4f6e-ba33-a7216e35a486.jpg",
                "shopName": "【二手9成新】 Redmi Note9 Pro 全网通 8G+128G 静默星空 国行",
                "skuCode": "210106105570",
                "totalUsableNum": 2,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/110/6287/1.jpg",
                "tags": "",
                "sellingPrice": 1379,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 3445,
                "prdStatus": 1,
                "mainImage": ""
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 40,
                "brandName": "OPPO",
                "prdId": 6379,
                "prdName": "OPPO Reno5",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2021-01-08/da32a49d-af94-4f02-a04b-d496a96c0352.webp",
                "shopName": "【二手9成新】 OPPO Reno5 全网通 12G+256G 月夜黑 国行",
                "skuCode": "210226108132",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/40/6379/1.jpg",
                "tags": "",
                "sellingPrice": 2199,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 1411,
                "prdStatus": 1,
                "mainImage": ""
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 40,
                "brandName": "OPPO",
                "prdId": 5706,
                "prdName": "OPPO Realme V5",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-10-26/63066638-1292-4f00-8284-a1111762a64a.png",
                "shopName": "【二手9成新】 OPPO Realme V5 全网通 8G+128G 青出于蓝 国行",
                "skuCode": "210508112926",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/40/5706/1.jpg",
                "tags": "",
                "sellingPrice": 1129,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 204,
                "prdStatus": 1,
                "mainImage": ""
            },
            {
                "shopCode": "ALIPAYSHOP",
                "brandId": 100,
                "brandName": "华为",
                "prdId": 4942,
                "prdName": "华为 Mate30",
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-10-08/d760e1f3-cea0-411c-a9fa-6212d2fc0775.png",
                "shopName": "【二手9成新】 华为 Mate30 全网通 6G+128G 星河银 国行",
                "skuCode": "20011578645",
                "totalUsableNum": 1,
                "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/100/4942/1.jpg",
                "tags": "安卓手机,热销机型",
                "sellingPrice": 2369,
                "status": 1,
                "version": 128628,
                "prdSaleType": 1,
                "views": 19326,
                "prdStatus": 1,
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-19/c7d6203b-a4f5-477f-9cc9-91756451ab42.jpg"
            }
        ]
    }
}
```

## 3.commodity商品详情

### 1.商品接口

接口参数：/sapi/gateway/shs-mall-api/v1/goods/goods-detail-v2?shopCode=alipayshop&prdId=number&skuCode=number&channelId=79595

请求方式：GET

参数：prdId；skuCode购买商品ID；channelId

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "goods": {
            "shopCode": "ALIPAYSHOP",
            "brandId": 10,
            "brandName": "苹果",
            "prdId": 4932,
            "prdName": "iPhone 11",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
            "shopName": "【二手9成新】 iPhone 11 A2223 128G 紫色 无保或有保一个月以下 国行",
            "skuCode": "201026100147",
            "shopSpecification": "<table width=\"393\"><colgroup><col width=\"105\" style=\"width:79.35pt;\"/><col width=\"419\" style=\"width:314.65pt;\"/></colgroup><tbody><tr style=\"height:13.50pt;\" class=\"firstRow\"><td class=\"et2\" width=\"79\" style=\"\"><span style=\"font-size: 11px;\">iPhone11</span></td><td width=\"314\" style=\"\"><br/></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">内存</span></td><td><span style=\"font-size: 11px;\">64G，128G，256G</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">分辨率</span></td><td><span style=\"font-size: 11px;\">1792x828像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">SIM卡规格</span></td><td><span style=\"font-size: 11px;\">双卡，Nano SIM卡</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">颜色</span></td><td><span style=\"font-size: 11px;\">黑色，绿色，黄色，紫色，红色，白色</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">CPU</span></td><td><span style=\"font-size: 11px;\">苹果 A13</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">网络</span></td><td><span style=\"font-size: 11px;\">全网通</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">主屏尺寸</span></td><td><span style=\"font-size: 11px;\">6.1英寸</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">前置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">后置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万广角摄像头+1200万超广角摄像头</span></td></tr></tbody></table><p><span style=\"font-size: 11px;\"><br/></span></p>",
            "totalUsableNum": 2,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1.jpg",
            "tags": "今日特价,以旧换新,热销机型,苹果手机",
            "shopDetail": "<p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/63d04e17-68cd-4bf6-8703-70af033065be.png\" width=\"350\"/></p><p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-26/1892418c-7869-4839-84b5-f3703fef792e.jpg\" width=\"350\"/></p>",
            "sellingPrice": 3849,
            "status": 1,
            "version": 128630,
            "skuDetailList": [
                {
                    "type": "型号",
                    "value": "A2223"
                },
                {
                    "type": "存储容量",
                    "value": "128G"
                },
                {
                    "type": "颜色",
                    "value": "紫色"
                },
                {
                    "type": "保修",
                    "value": "无保或有保一个月以下"
                },
                {
                    "type": "购买渠道",
                    "value": "国行"
                },
                {
                    "type": "苹果",
                    "value": "iPhone 11"
                },
                {
                    "type": "成色",
                    "value": "二手9成新"
                }
            ],
            "skuImageList": [
                "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1230/1.jpg",
                "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1260/1.jpg",
                "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1280/1.jpg",
                "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1290/1.jpg",
                "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1291/1.jpg",
                "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1292/1.jpg"
            ],
            "prdSaleType": 1,
            "views": 221492,
            "prdStatus": 1,
            "hugelyPopularSku": 0,
            "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg",
            "productGroup": " 37 45 49 54",
            "updatetm": 1618392734000,
            "coupon": {
                "id": 188,
                "shopCode": "ALIPAYSHOP",
                "couponName": "100元优惠劵",
                "couponPrice": 100,
                "rulesJson": "{\"maxLimit\":\"100\",\"recycleMaxLimit\":0,\"ticketType\":\"2\",\"prdLimit\":\"4932,5109,5201,6399\"}",
                "couponDesc": "新人领券满100减100",
                "type": 1,
                "delayTime": 3,
                "timeType": 0,
                "createUser": "何都威",
                "createtm": 1620789820000,
                "updatetm": 1620789837000,
                "category": 1,
                "receviedUrl": "alipays://platformapi/startapp?appId=2018060760255864&page=pages-activity/discount-coupon/discount-coupon?actId=20210512",
                "receiveNum": 0,
                "actId": 20210512,
                "actType": 5,
                "begindt": 1620748800000,
                "expiredt": 1621612800000,
                "canUse": true,
                "checkFailReason": "该优惠券可以正常使用",
                "fitVos": [
                    {
                        "skuCode": "201026100147",
                        "couponId": 188,
                        "canUse": true
                    }
                ]
            },
            "afterCouponPrice": 3749
        },
        "otherGoods": [
            {
                "prdId": 4932,
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 128G 白色 有保一个月以上 国行",
                "skuCode": "20010277587",
                "shopSpecification": "<table width=\"393\"><colgroup><col width=\"105\" style=\"width:79.35pt;\"/><col width=\"419\" style=\"width:314.65pt;\"/></colgroup><tbody><tr style=\"height:13.50pt;\" class=\"firstRow\"><td class=\"et2\" width=\"79\" style=\"\"><span style=\"font-size: 11px;\">iPhone11</span></td><td width=\"314\" style=\"\"><br/></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">内存</span></td><td><span style=\"font-size: 11px;\">64G，128G，256G</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">分辨率</span></td><td><span style=\"font-size: 11px;\">1792x828像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">SIM卡规格</span></td><td><span style=\"font-size: 11px;\">双卡，Nano SIM卡</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">颜色</span></td><td><span style=\"font-size: 11px;\">黑色，绿色，黄色，紫色，红色，白色</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">CPU</span></td><td><span style=\"font-size: 11px;\">苹果 A13</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">网络</span></td><td><span style=\"font-size: 11px;\">全网通</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">主屏尺寸</span></td><td><span style=\"font-size: 11px;\">6.1英寸</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">前置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">后置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万广角摄像头+1200万超广角摄像头</span></td></tr></tbody></table><p><span style=\"font-size: 11px;\"><br/></span></p>",
                "totalUsableNum": 1,
                "shopDetail": "<p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/63d04e17-68cd-4bf6-8703-70af033065be.png\" width=\"350\"/></p><p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-26/1892418c-7869-4839-84b5-f3703fef792e.jpg\" width=\"350\"/></p>",
                "sellingPrice": 3949,
                "skuDetailList": [
                    {
                        "type": "型号",
                        "value": "A2223"
                    },
                    {
                        "type": "存储容量",
                        "value": "128G"
                    },
                    {
                        "type": "颜色",
                        "value": "白色"
                    },
                    {
                        "type": "保修",
                        "value": "有保一个月以上"
                    },
                    {
                        "type": "购买渠道",
                        "value": "国行"
                    },
                    {
                        "type": "苹果",
                        "value": "iPhone 11"
                    },
                    {
                        "type": "成色",
                        "value": "二手9成新"
                    }
                ],
                "skuImageList": [
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1230/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1260/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1280/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1290/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1291/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1292/1.jpg"
                ],
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg"
            },
            {
                "prdId": 4932,
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 64G 黑色 无保或有保一个月以下 国行",
                "skuCode": "20071092849",
                "shopSpecification": "<table width=\"393\"><colgroup><col width=\"105\" style=\"width:79.35pt;\"/><col width=\"419\" style=\"width:314.65pt;\"/></colgroup><tbody><tr style=\"height:13.50pt;\" class=\"firstRow\"><td class=\"et2\" width=\"79\" style=\"\"><span style=\"font-size: 11px;\">iPhone11</span></td><td width=\"314\" style=\"\"><br/></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">内存</span></td><td><span style=\"font-size: 11px;\">64G，128G，256G</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">分辨率</span></td><td><span style=\"font-size: 11px;\">1792x828像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">SIM卡规格</span></td><td><span style=\"font-size: 11px;\">双卡，Nano SIM卡</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">颜色</span></td><td><span style=\"font-size: 11px;\">黑色，绿色，黄色，紫色，红色，白色</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">CPU</span></td><td><span style=\"font-size: 11px;\">苹果 A13</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">网络</span></td><td><span style=\"font-size: 11px;\">全网通</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">主屏尺寸</span></td><td><span style=\"font-size: 11px;\">6.1英寸</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">前置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">后置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万广角摄像头+1200万超广角摄像头</span></td></tr></tbody></table><p><span style=\"font-size: 11px;\"><br/></span></p>",
                "totalUsableNum": 1,
                "shopDetail": "<p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/63d04e17-68cd-4bf6-8703-70af033065be.png\" width=\"350\"/></p><p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-26/1892418c-7869-4839-84b5-f3703fef792e.jpg\" width=\"350\"/></p>",
                "sellingPrice": 3459,
                "skuDetailList": [
                    {
                        "type": "型号",
                        "value": "A2223"
                    },
                    {
                        "type": "存储容量",
                        "value": "64G"
                    },
                    {
                        "type": "颜色",
                        "value": "黑色"
                    },
                    {
                        "type": "保修",
                        "value": "无保或有保一个月以下"
                    },
                    {
                        "type": "购买渠道",
                        "value": "国行"
                    },
                    {
                        "type": "苹果",
                        "value": "iPhone 11"
                    },
                    {
                        "type": "成色",
                        "value": "二手9成新"
                    }
                ],
                "skuImageList": [
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1230/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1260/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1280/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1290/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1291/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1292/1.jpg"
                ],
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg"
            },
            {
                "prdId": 4932,
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 128G 白色 无保或有保一个月以下 国行",
                "skuCode": "20101098760",
                "shopSpecification": "<table width=\"393\"><colgroup><col width=\"105\" style=\"width:79.35pt;\"/><col width=\"419\" style=\"width:314.65pt;\"/></colgroup><tbody><tr style=\"height:13.50pt;\" class=\"firstRow\"><td class=\"et2\" width=\"79\" style=\"\"><span style=\"font-size: 11px;\">iPhone11</span></td><td width=\"314\" style=\"\"><br/></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">内存</span></td><td><span style=\"font-size: 11px;\">64G，128G，256G</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">分辨率</span></td><td><span style=\"font-size: 11px;\">1792x828像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">SIM卡规格</span></td><td><span style=\"font-size: 11px;\">双卡，Nano SIM卡</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">颜色</span></td><td><span style=\"font-size: 11px;\">黑色，绿色，黄色，紫色，红色，白色</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">CPU</span></td><td><span style=\"font-size: 11px;\">苹果 A13</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">网络</span></td><td><span style=\"font-size: 11px;\">全网通</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">主屏尺寸</span></td><td><span style=\"font-size: 11px;\">6.1英寸</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">前置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">后置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万广角摄像头+1200万超广角摄像头</span></td></tr></tbody></table><p><span style=\"font-size: 11px;\"><br/></span></p>",
                "totalUsableNum": 1,
                "shopDetail": "<p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/63d04e17-68cd-4bf6-8703-70af033065be.png\" width=\"350\"/></p><p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-26/1892418c-7869-4839-84b5-f3703fef792e.jpg\" width=\"350\"/></p>",
                "sellingPrice": 3849,
                "skuDetailList": [
                    {
                        "type": "型号",
                        "value": "A2223"
                    },
                    {
                        "type": "存储容量",
                        "value": "128G"
                    },
                    {
                        "type": "颜色",
                        "value": "白色"
                    },
                    {
                        "type": "保修",
                        "value": "无保或有保一个月以下"
                    },
                    {
                        "type": "购买渠道",
                        "value": "国行"
                    },
                    {
                        "type": "苹果",
                        "value": "iPhone 11"
                    },
                    {
                        "type": "成色",
                        "value": "二手9成新"
                    }
                ],
                "skuImageList": [
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1230/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1260/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1280/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1290/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1291/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1292/1.jpg"
                ],
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg"
            },
            {
                "prdId": 4932,
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 64G 紫色 无保或有保一个月以下 国行",
                "skuCode": "201102100850",
                "shopSpecification": "<table width=\"393\"><colgroup><col width=\"105\" style=\"width:79.35pt;\"/><col width=\"419\" style=\"width:314.65pt;\"/></colgroup><tbody><tr style=\"height:13.50pt;\" class=\"firstRow\"><td class=\"et2\" width=\"79\" style=\"\"><span style=\"font-size: 11px;\">iPhone11</span></td><td width=\"314\" style=\"\"><br/></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">内存</span></td><td><span style=\"font-size: 11px;\">64G，128G，256G</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">分辨率</span></td><td><span style=\"font-size: 11px;\">1792x828像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">SIM卡规格</span></td><td><span style=\"font-size: 11px;\">双卡，Nano SIM卡</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">颜色</span></td><td><span style=\"font-size: 11px;\">黑色，绿色，黄色，紫色，红色，白色</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">CPU</span></td><td><span style=\"font-size: 11px;\">苹果 A13</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">网络</span></td><td><span style=\"font-size: 11px;\">全网通</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">主屏尺寸</span></td><td><span style=\"font-size: 11px;\">6.1英寸</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">前置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">后置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万广角摄像头+1200万超广角摄像头</span></td></tr></tbody></table><p><span style=\"font-size: 11px;\"><br/></span></p>",
                "totalUsableNum": 1,
                "shopDetail": "<p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/63d04e17-68cd-4bf6-8703-70af033065be.png\" width=\"350\"/></p><p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-26/1892418c-7869-4839-84b5-f3703fef792e.jpg\" width=\"350\"/></p>",
                "sellingPrice": 3459,
                "skuDetailList": [
                    {
                        "type": "型号",
                        "value": "A2223"
                    },
                    {
                        "type": "存储容量",
                        "value": "64G"
                    },
                    {
                        "type": "颜色",
                        "value": "紫色"
                    },
                    {
                        "type": "保修",
                        "value": "无保或有保一个月以下"
                    },
                    {
                        "type": "购买渠道",
                        "value": "国行"
                    },
                    {
                        "type": "苹果",
                        "value": "iPhone 11"
                    },
                    {
                        "type": "成色",
                        "value": "二手9成新"
                    }
                ],
                "skuImageList": [
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1230/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1260/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1280/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1290/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1291/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1292/1.jpg"
                ],
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg"
            },
            {
                "prdId": 4932,
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 128G 红色 无保或有保一个月以下 国行",
                "skuCode": "20090396341",
                "shopSpecification": "<table width=\"393\"><colgroup><col width=\"105\" style=\"width:79.35pt;\"/><col width=\"419\" style=\"width:314.65pt;\"/></colgroup><tbody><tr style=\"height:13.50pt;\" class=\"firstRow\"><td class=\"et2\" width=\"79\" style=\"\"><span style=\"font-size: 11px;\">iPhone11</span></td><td width=\"314\" style=\"\"><br/></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">内存</span></td><td><span style=\"font-size: 11px;\">64G，128G，256G</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">分辨率</span></td><td><span style=\"font-size: 11px;\">1792x828像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">SIM卡规格</span></td><td><span style=\"font-size: 11px;\">双卡，Nano SIM卡</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">颜色</span></td><td><span style=\"font-size: 11px;\">黑色，绿色，黄色，紫色，红色，白色</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">CPU</span></td><td><span style=\"font-size: 11px;\">苹果 A13</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">网络</span></td><td><span style=\"font-size: 11px;\">全网通</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">主屏尺寸</span></td><td><span style=\"font-size: 11px;\">6.1英寸</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">前置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">后置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万广角摄像头+1200万超广角摄像头</span></td></tr></tbody></table><p><span style=\"font-size: 11px;\"><br/></span></p>",
                "totalUsableNum": 1,
                "shopDetail": "<p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/63d04e17-68cd-4bf6-8703-70af033065be.png\" width=\"350\"/></p><p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-26/1892418c-7869-4839-84b5-f3703fef792e.jpg\" width=\"350\"/></p>",
                "sellingPrice": 3849,
                "skuDetailList": [
                    {
                        "type": "型号",
                        "value": "A2223"
                    },
                    {
                        "type": "存储容量",
                        "value": "128G"
                    },
                    {
                        "type": "颜色",
                        "value": "红色"
                    },
                    {
                        "type": "保修",
                        "value": "无保或有保一个月以下"
                    },
                    {
                        "type": "购买渠道",
                        "value": "国行"
                    },
                    {
                        "type": "苹果",
                        "value": "iPhone 11"
                    },
                    {
                        "type": "成色",
                        "value": "二手9成新"
                    }
                ],
                "skuImageList": [
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1230/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1260/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1280/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1290/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1291/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1292/1.jpg"
                ],
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg"
            },
            {
                "prdId": 4932,
                "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
                "shopName": "【二手9成新】 iPhone 11 A2223 128G 绿色 有保一个月以上 国行",
                "skuCode": "19123077351",
                "shopSpecification": "<table width=\"393\"><colgroup><col width=\"105\" style=\"width:79.35pt;\"/><col width=\"419\" style=\"width:314.65pt;\"/></colgroup><tbody><tr style=\"height:13.50pt;\" class=\"firstRow\"><td class=\"et2\" width=\"79\" style=\"\"><span style=\"font-size: 11px;\">iPhone11</span></td><td width=\"314\" style=\"\"><br/></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">内存</span></td><td><span style=\"font-size: 11px;\">64G，128G，256G</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">分辨率</span></td><td><span style=\"font-size: 11px;\">1792x828像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">SIM卡规格</span></td><td><span style=\"font-size: 11px;\">双卡，Nano SIM卡</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">颜色</span></td><td><span style=\"font-size: 11px;\">黑色，绿色，黄色，紫色，红色，白色</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">CPU</span></td><td><span style=\"font-size: 11px;\">苹果 A13</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">网络</span></td><td><span style=\"font-size: 11px;\">全网通</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">主屏尺寸</span></td><td><span style=\"font-size: 11px;\">6.1英寸</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">前置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万像素</span></td></tr><tr style=\"height:13.50pt;\"><td style=\"\"><span style=\"font-size: 11px;\">后置摄像头</span></td><td><span style=\"font-size: 11px;\">1200万广角摄像头+1200万超广角摄像头</span></td></tr></tbody></table><p><span style=\"font-size: 11px;\"><br/></span></p>",
                "totalUsableNum": 1,
                "shopDetail": "<p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-08-01/63d04e17-68cd-4bf6-8703-70af033065be.png\" width=\"350\"/></p><p style=\"text-align: center;\"><img src=\"https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-05-26/1892418c-7869-4839-84b5-f3703fef792e.jpg\" width=\"350\"/></p>",
                "sellingPrice": 3949,
                "skuDetailList": [
                    {
                        "type": "型号",
                        "value": "A2223"
                    },
                    {
                        "type": "存储容量",
                        "value": "128G"
                    },
                    {
                        "type": "颜色",
                        "value": "绿色"
                    },
                    {
                        "type": "保修",
                        "value": "有保一个月以上"
                    },
                    {
                        "type": "购买渠道",
                        "value": "国行"
                    },
                    {
                        "type": "苹果",
                        "value": "iPhone 11"
                    },
                    {
                        "type": "成色",
                        "value": "二手9成新"
                    }
                ],
                "skuImageList": [
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1230/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1260/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1280/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1290/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1291/1.jpg",
                    "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1292/1.jpg"
                ],
                "mainImage": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-04-16/80ae82ad-eea7-48d2-9df2-2892732ceb08.jpg"
            }
        ],
        "discussCount": 0,
        "enableFormat": "颜色,存储容量,型号,购买渠道,保修,成色"
    }
}
```

### 2.热销接口

接口参数：/sapi/gateway/shs-mall-api/v1/goods/goods-list/page-info

请求方式：POST——application/x-www-form-urlencoded

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "prdId": 4932,
            "prdName": "iPhone 11",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/8f3c06e3-26d7-48dc-adb1-5e80d3ae7e58.png",
            "shopName": "【二手9成新】 iPhone 11 A2223 128G 绿色 有保一个月以上 国行",
            "skuCode": "20051288808",
            "sellingPrice": 3949,
            "stockNum": 1,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4932/1.jpg",
            "views": 221494,
            "sort": 0,
            "minPrice": 3459,
            "saleNum": 41,
            "updatetm": 1618392734000,
            "firstOnShelfTime": 1591264972000
        },
        {
            "prdId": 3159,
            "prdName": "iPhone 8 plus",
            "prdImgUrl": "//shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2017-12-20/384a66a2-29e3-49b6-9222-e520695a2edb.jpg",
            "shopName": "【二手9成新】iPhone 8 plus A1864 64G 深空灰 无保或有保一个月以下 国行",
            "skuCode": "19082964863",
            "sellingPrice": 1849,
            "stockNum": 1,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/3159/1.jpg",
            "views": 119767,
            "sort": 0,
            "minPrice": 1739,
            "saleNum": 53,
            "updatetm": 1618392734000,
            "firstOnShelfTime": 1591264942000
        },
        {
            "prdId": 4097,
            "prdName": "iPhone XS Max",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-11-14/2b42bf4b-1124-406e-9ddd-a45dc5d292b7.jpg",
            "shopName": "二手9成新|iPhone XS Max|A2104|64G|金色|无保或有保一个月以下|国行",
            "skuCode": "19083165086",
            "sellingPrice": 3139,
            "stockNum": 2,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4097/1.jpg",
            "views": 108856,
            "sort": 0,
            "minPrice": 3139,
            "saleNum": 16,
            "updatetm": 1618392734000,
            "firstOnShelfTime": 1591264942000
        },
        {
            "prdId": 4113,
            "prdName": "iPhone XR",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2018-11-14/58b59b8a-aca3-4abb-9ab9-09b572b1d9e4.png",
            "shopName": "【二手9成新】 iPhone XR A2108 128G 红色 无保或有保一个月以下 国行",
            "skuCode": "210409111029",
            "sellingPrice": 2839,
            "stockNum": 2,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4113/1.jpg",
            "views": 87466,
            "sort": 0,
            "minPrice": 2699,
            "saleNum": 11,
            "updatetm": 1618392734000,
            "firstOnShelfTime": 1591264942000
        },
        {
            "prdId": 4933,
            "prdName": "iPhone 11 Pro",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2019-09-21/97b24243-7228-4bc6-a742-39d9c72d6624.png",
            "shopName": "【二手95新】 iPhone 11 Pro A2217 64G 金色 有保一个月以上 国行",
            "skuCode": "19101168386",
            "sellingPrice": 4669,
            "stockNum": 1,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/4933/1.jpg",
            "views": 79081,
            "sort": 0,
            "minPrice": 4669,
            "updatetm": 1618392734000,
            "firstOnShelfTime": 1591264972000
        },
        {
            "prdId": 2682,
            "prdName": "iPhone 7 Plus",
            "prdImgUrl": "https://shanhs.oss-cn-shenzhen.aliyuncs.com/newboss/2020-09-15/a113fc6c-4cdf-4c9d-8293-fc1458d41421.png",
            "shopName": "【二手9成新】iPhone 7 Plus A1661 32G 银色 无保或有保一个月以下 国行",
            "skuCode": "19070357410",
            "sellingPrice": 1209,
            "stockNum": 1,
            "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/10/2682/1.jpg",
            "views": 53886,
            "sort": 1,
            "minPrice": 1209,
            "saleNum": 5,
            "updatetm": 1608624743000,
            "firstOnShelfTime": 1591264921000
        }
    ]
}
```

## 4.submit提交订单

接口参数：/sapi/gateway/shs-mall-api/v1/goods/get-goods-simple-info?skuCode=number

请求接口：GET

参数：skuCode商品参数

数据格式：

```json
{
    "success": true,
    "code": 0,
    "data": {
        "skuCode": "20030279987",
        "prdId": 5214,
        "shopName": "【新品】 苹果奇门纳福手机壳 iPhoneXS Max",
        "shopMainUrl": "https://shanhs-malls.oss-cn-shenzhen.aliyuncs.com/1/3400/5214/1.jpg",
        "sellingPrice": 39,
        "totalUsableNum": 1
    }
}
```

## 5.about关于我们

接口参数：/sapi/gateway/boss-system-api/nb-agreement/by-type

接口类型：POST——application/x-www-form-urlencoded

## 6.problem常见问题

接口参数：/sapi//gateway/online-sapi/v1/knowledge/mmenu/getNbKnowledge?code=shanfish_mine

接口类型;GET
