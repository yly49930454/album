# 毕业纪念APP
# PRD价值主张设计
## 加值宣言
很多人都会有，想不起来这个人，但当一旦看到或接触到就会激发起脑海深处的记忆。我构想的毕业纪念APP的功能有：
1. 上传你的影像：你可以上传你的信息以及你的照片、和同学的合影，你可以上传纪念属于你的美好回忆
2. “可能认识的人”：你可以在你上传的照片中标识出「你」，然后可以通过人脸识别API分析哪些合影里「可能」含有你的影像，那个上传合影的人可能就是你的遗忘多年的好友哦
3. “影像朋友圈”：如果你合影里的人也有账户，那么你可以直接添加该人的信息到图像上，系统会建立你的合影关系网络，系统也会推送你合影上「可能」有的人哦
4. “联系你的同学！”：你可以直接在APP上联系你的同学，当然交换号码也可以！

## 核心价值
产品的核心价值是通过用户上传的影像，构建属于用户的回忆网络，帮助用户找到学生时代的同学和伙伴，你的关系网络人数越多你的合影判断就越精准

## 用户使用场景
* 场景一： 毕业时想继续和同学们保持联系，在毕业时将合影和同伴的账号添加到自己的APP上，组建一个关系网络，这样在过多少年，再拿出来都能回忆起来了
* 场景二： 毕业后的想找回学生时代的同学，将当时的合影上传到APP，希望APP能帮忙找回几个学生时代的同学

## 人工智能概率性和用户痛点
* AZURE面部检测：检测图中是否有人脸，有几张人脸。用来判断图上的人脸及其数量

* AZURE人脸验证：判断人脸相似度，超过一定阀值的人脸会被认为是同一名用户。用于判断是否合影中的人是否同一名用户

## 需求列表与人工智能API加值


需求 | API | 重要程度 
-|-|-
用户想知道照片上有谁 | 面部检测 | 重要|
用户想知道哪些照片有自己 | 人脸验证 | 重要 |


                                                       
# 原型
### 个人信息
* 你可以在个人信息页面对自己的信息和同学录进行编辑，并且分享你的同学录，让你的同学也加入进来
![个人信息](https://github.com/yly49930454/album/blob/master/media/%E4%B8%AA%E4%BA%BA%E4%BF%A1%E6%81%AF.png)

### 我的相册
* 你可以在此处观看你上传的照片到你设置的文件夹里，你随时可以查看你上传的照片
![我的相册](https://github.com/yly49930454/album/blob/master/media/%E6%88%91%E7%9A%84%E7%9B%B8%E5%86%8C.png)

### 我的关系网
* 你可以在此处看有多少同学在你同学录里，会成为一个关系网，你可以通过右下角的查找查询「可能」有你存在的照片
![我的关系网](https://github.com/yly49930454/album/blob/master/media/%E6%88%91%E7%9A%84%E5%85%B3%E7%B3%BB%E7%BD%91.png)

### 聊天栏
* 当你找到你的老同学，你可以给他发信息，交换号码，立刻就可以交流
![聊天栏](https://github.com/yly49930454/album/blob/master/media/%E8%81%8A%E5%A4%A9%E6%A0%8F.png)






# API的使用
1. Azure 人脸API
* HTTP方法：POST
* 请求URL：https://<My Endpoint String>.com/face/v1.0/detect
* API价值主张：人脸 API 可以检测图像中的人脸，并返回其位置的矩形坐标。 （可选）人脸检测可以提取一系列人脸相关的属性。
* 请求代码实例：
``` python
import requests
import json

# set to your own subscription key value
subscription_key = ‘’
assert subscription_key

# replace <My Endpoint String> with the string from your endpoint URL
face_api_url = ‘https://<My Endpoint String>.com/face/v1.0/detect’

image_url = ‘https://upload.wikimedia.org/wikipedia/commons/3/37/Dagestani_man_and_woman.jpg’

headers = {‘Ocp-Apim-Subscription-Key’: subscription_key}

params = {
    ‘returnFaceId’: ‘true’,
    ‘returnFaceLandmarks’: ‘false’,
    ‘returnFaceAttributes’: ‘age,gender,headPose,smile,facialHair,glasses,emotion,hair,makeup,occlusion,accessories,blur,exposure,noise’,
}

response = requests.post(face_api_url, params=params,
                         headers=headers, json={“url”: image_url})
print(json.dumps(response.json()))
```

* 面部识别返回实例
``` javascript
 {
    “faceId”: “9b17fcf6-efaf-4d61-ba0c-45ac6a0763ca”,
    “faceRectangle”: {
      “top”: 101,
      “left”: 96,
      “width”: 218,
      “height”: 307
    },
    “faceAttributes”: null,
    “faceLandmarks”: null
  },
  {
    “faceId”: “74262c17-184f-450d-88a7-fb110c7f3bde”,
    “faceRectangle”: {
      “top”: 286,
      “left”: 728,
      “width”: 96,
      “height”: 120
    },
    “faceAttributes”: null,
    “faceLandmarks”: null
  },
  {
    “faceId”: “2dd9f0a9-5889-46f2-913d-bcb97ef8334d”,
    “faceRectangle”: {
      “top”: 296,
      “left”: 385,
      “width”: 86,
      “height”: 116
    },
```

* 人脸验证返回实例
``` 
{
            “color”: “black”,
            “confidence”: 0.98
          }
```






