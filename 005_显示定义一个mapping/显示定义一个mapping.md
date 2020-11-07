```
//创建一个users索引,mobile字段不被索引
PUT /users
{
  "mappings": {
    "properties": {
      "firstName":{
        "type": "text"
      },
      "lastName":{
        "type": "text"
      },
      "mobile":{
        "type": "text",
        "index": false
      }
    }
  }
}


//创建一个文档
PUT /users/_doc/1
{
  "firstName":"小白",
  "lastName":"小盒",
  "mobile":"18798765543"
}


//没有索引的字段无法搜索
POST /users/_search
{
  "query": {
    "match": {
      "mobile": "18798765543"
    }
  }
}


//设置空值
PUT /users_v2
{
  "mappings": {
    "properties": {
      "firstName":{
        "type": "text"
      },
      "lastName":{
        "type": "text"
      },
      "mobile":{
        "type": "keyword",
        "null_value": "NULL"
      }
    }
  }
}


//创建文档
PUT /users_v2/_doc/1
{
  "firstName":"闭关",
  "lastName":"修炼",
  "mobile":null
}


POST /users_v2/_search
{
  "query": {
    "match": {
      "mobile": "NULL"
    }
  }
}


//使用copy_to
PUT /users_v3
{
  "mappings": {
    "properties": {
      "firstName":{
        "type": "text",
        "copy_to": "fullName"
      },
      "lastName":{
        "type": "text",
        "copy_to": "fullName"
      }
    }
  }
}


DELETE /users_v3


PUT /users_v3/_doc/1
{
  "firstName":"Zdc",
  "lastName":"小溪"
}


GET /users_v3/_search?q=fullName:(Zdc)


//数组
PUT /users_v3/_doc/1
{
  "name":"two",
  "interests":["reading","music"]
}


POST /users_v3/_search
{
  "query": {
    "match_all": {}
  }
}

```