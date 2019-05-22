# 移动端分组发言接口

## 1.1	获取课堂和小组相关信息


> 返回的JSON示例:

```JSON
{
  "id":"5cb577db502c29a43718ecad",
  "courseId":3,
  "courseName":"20190402",
  "groupName":"A",
  "color":"#4A90E2",
  "isLeader":false
}
```

### HTTP 请求

`GET /mobile-api/v3/group-discussions/:groupId`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
id | *string* | 也许是 openid ?
courseId | *number* | 课堂id
courseName | *string* | 课堂名称
groupName | *string* | 分组名称
color | *string* | 小组主题色
isLeader | *boolean* | 该学生是否是组长


## 1.2	获取除组长外的小组成员信息


> 返回的JSON示例:

```JSON
[
  {"id": 2, "name": "吴泪泪", "avatar": ""},
  {"id": 1, "name": "刘亚雪", "avatar": ""}
]
```

### HTTP 请求

`GET /mobile-api/v3/group-discussions/:groupId/students`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
id | *string* | 学生id
name | *string* | 学生姓名
avatar | *string* | 学生头像


## 1.3	移交组长给其他组员


> 返回的JSON示例:

```JSON
{ "success": true}
```

### HTTP 请求

`PUT /mobile-api/v3/group-discussions/:groupId/leader`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
studentId | true | 无 | *number* | 移交对象的学生id

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
success | *boolean* | 请求成功提示语


## 1.4	退出当前小组


> 返回的JSON示例:

```JSON
{ "success": true}
```

### HTTP 请求

`PUT /mobile-api/v3/group-discussions/:groupId/quit`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
success | *boolean* | 请求成功提示语


## 1.5	查询当前小组发言


> 返回的JSON示例:

```JSON
{
  "features": ["5cb5a77173c7b46bb4f728ed", "5cb58e7f502c29a43718f837"],
  "msgCursor": 10,
  "msgs": [
    {
      "content": "te",
      "createTime": 1555408100659,
      "id": "5cb5a4e47b2aa06b888283e3",
      "isFeatured": false,
      "studentId": 1,
      "text": "te",
      "type": 1
    },
    {
      "content": "du",
      "courseId": 3,
      "createTime": "2019-04-18T09:33:01.575Z",
      "discussion": "5cb573bb502c29a43718eadf",
      "group": "5cb577db502c29a43718ecad",
      "id": "5cb8444d66b8b9a5154aa7b2",
      "isFeatured": false,
      "studentId": 2,
      "type": 1,
      "updatedTime": "2019-04-18T09:59:06.512Z"
    }
  ],
  "students": [
    {"id": 2, "name": "吴泪泪", "avatar": "", "isLeader": true}, 
    {"id": 1, "name": "刘雅雪", "avatar": "", "isLeader": false}
  ]
}
```

### HTTP 请求

`GET /mobile-api/v3/group-discussions/groups/:groupId`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
features | *array* | 精选发言的ids
msgCursor | *number* | 已返回的发言数量
msgs | *array* | 当前页的发言
> content | *string* | 发言内容
> courseId | *number* | 课堂id
> createTime | *string* | 发言时间
> discussion | *string* | 不知道
> group | *string* | 小组id
> id | *string* | 发言id
> isFeatured | *boolean* | 是否精选
> studentId | *number* | 学生id
> type | *number* | 1: 文本 2: 图片
> updatedTime | *string* | 发言精选更新时间
students | *array* | 小组全部成员（包括组长）
> id | *number* | 学生id
> name | *string* | 学生姓名
> avatar | *string* | 学生头像
> isLeader | *boolean* | 是否是组长


## 1.6	发送已经排序了的精选发言ids


> 返回的JSON示例:

```JSON
{ "success": true}
```

### HTTP 请求

`POST /mobile-api/v3/group-discussions/groups/:groupId/features`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
features | true | 无 | *array* | 当前小组所有的精选发言ids

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
success | *boolean* | 请求成功提示语


## 1.7	获取全部精选发言数据


> 返回的JSON示例:

```JSON
{ 
  "msgs": [
    {
      "content": "muwa",
      "courseId": 3,
      "createTime": "2019-04-16T09:59:13.629Z",
      "discussion": "5cb573bb502c29a43718eadf",
      "group": "5cb577db502c29a43718ecad",
      "id": "5cb5a77173c7b46bb4f728ed",
      "studentId": 2,
      "type": 1,
      "updatedTime": "2019-04-18T08:53:29.175Z"
    },
    {
      "content": "du",
      "courseId": 3,
      "createTime": "2019-04-18T09:33:01.575Z",
      "discussion": "5cb573bb502c29a43718eadf",
      "group": "5cb577db502c29a43718ecad",
      "id": "5cb8444d66b8b9a5154aa7b2",
      "studentId": 2,
      "type": 1,
      "updatedTime": "2019-04-18T09:59:06.512Z"
    },
  ],
  "students": [
    {"id": 1, "name": "刘雅雪", "avatar": ""}, 
    {"id": 2, "name": "吴泪泪", "avatar": ""}
  ]
}
```

### HTTP 请求

`GET /mobile-api/v3/group-discussions/groups/:groupId/features`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
msgs | *array* | 当前页的发言
> content | *string* | 发言内容
> courseId | *number* | 课堂id
> createTime | *string* | 发言时间
> discussion | *string* | 不知道
> group | *string* | 小组id
> id | *string* | 发言id
> studentId | *number* | 学生id
> type | *number* | 1: 文本 2: 图片
> updatedTime | *string* | 发言精选更新时间
students | *array* | 小组全部成员（包括组长）
> id | *number* | 学生id
> name | *string* | 学生姓名
> avatar | *string* | 学生头像


## 1.8	独立发送发言


> 返回的JSON示例:

```JSON
{ "success": true}
```

### HTTP 请求

`POST /mobile-api/v3/group-discussions/groups/:groupId/msgs`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
groupId | true | 无 | *string* | 当前小组的id
text | false(text和imgs至少有一个必须) | 无 | *string* | 发言的文本
imgs | false(text和imgs至少有一个必须) | 无 | *array* | 图片在oss上的名称

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
success | *boolean* | 请求成功提示语




# 学生签到接口


## 1.1  获取历史签到列表


> 返回的JSON示例:

```JSON
[
	{
    "date": "2019-05-14", // 签到日期
    "id": "1001", // 签到id
    "count": 4, // 该日成功签到次数
    "data": [ //time 签到时间  num 签到人数  ratio 出勤率
      { "time": "18:34", "num": 3, "ratio": "5%" },
      { "time": "17:34", "num": 3, "ratio": "5%" },
      { "time": "16:34", "num": 3, "ratio": "5%" },
      { "time": "15:34", "num": 3, "ratio": "5%" }
		]
  },
  {
    "date": "2019-05-13",
    "count": 5, // 该日成功签到次数
    "data": [ //time 签到时间  num 签到人数  ratio 出勤率
      { "time": "18:34", "num": 3, "ratio": "5" },
      { "time": "17:34", "num": 3, "ratio": "5" },
      { "time": "16:34", "num": 3, "ratio": "5" },
      { "time": "15:34", "num": 3, "ratio": "5" }
		]
  },
]
```

### HTTP 请求

`GET /xxxxxxx/:courseId`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
date | string | 签到日期
id | string | 签到id
count | 4 | 该日成功签到次数
data | object | 单次签到数据组成的数组
> time | string | 签到具体时间
> num | number | 签到人数
> ratio | string | 签到百分比(出勤率)


## 1.2  获取签到详情数据


> 返回的JSON示例:

```JSON
{
  "date": "2019-05-21 18:34:58",
  "type": "qrcode", // qrcode 二维码签到  gps GPS定位签到  normal 普通签到
  "count": "3", // 出勤人数
  "ratio": "23",  // 出勤率
  "signDistribution": {
    "0": {
      "stateCount": [10, 3, 0, 0], // 各状态人数，依次代表 [旷课, 迟到, 请假, 签到成功] 的人数
      "name": "未分组" // 分组组名  ps:未分组学生归为一组  组名为未分组
    }
  }
}
```

### HTTP 请求

`GET /xxxxxxx/:signId`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
date | string | 签到日期时间
type | string | 签到类型： qrcode 二维码签到； gps GPS定位签到； normal 普通签到
count | number | 签到人数
ratio | number | 出勤率
signDistribution | object | 分组数据统计 以组id为key(如果有id的话，没有就0，1，2...)
> stateCount | array | 各状态人数 依次为 [旷课, 迟到, 请假, 签到成功] 人数
> name | string | 分组组名 （未分组学生归为一组  组名为未分组）


## 1.3  开启签到


> 返回的JSON示例:

```JSON
{
  "channel": "/attendance/16/115/qr",
  "id": "115",
  "qrUrl": "http://app.jinkefang.cn/api/v1/qrcode/d500cd5547dd8b3dd916fbd697e66b4da81bf7e564eff33511a790ddaf309c97/attendance",
  "status": true,
  "students": [],
}
```

### HTTP 请求

`GET /xxxxxxx/:signId`

### 请求参数

参数 | 必选 | 默认 | 字段类型 | 字段说明
--------- |-------- |-------- |--------- |-----------
无

### 返回字段说明

参数  | 字段类型 | 字段说明
--------- |------------ |------------
date | string | 签到日期时间
type | string | 签到类型： qrcode 二维码签到； gps GPS定位签到； normal 普通签到
count | number | 签到人数
ratio | number | 出勤率
signDistribution | object | 分组数据统计 以组id为key(如果有id的话，没有就0，1，2...)
> stateCount | array | 各状态人数 依次为 [旷课, 迟到, 请假, 签到成功] 人数
> name | string | 分组组名 （未分组学生归为一组  组名为未分组）


