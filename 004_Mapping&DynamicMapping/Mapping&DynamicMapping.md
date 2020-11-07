```
PUT /mapping_test/_doc/1
{
  "firstName":"Zhu",
  "lastName":"DeChao",
  "loginDate":"2020-11-07T10:00:00.100Z"
}


//查看字段类型定义
GET /mapping_test/_mapping


DELETE /mapping_test


PUT /mapping_test/_doc/1
{
  "uid":"123",
  "isVip":false,
  "isAdmin":"true",
  "age":19,
  "heigh":187
}


GET /mapping_test/_mapping
```