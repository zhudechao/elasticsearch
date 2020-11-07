```
GET /movies/_search?q=2012&df=title&sort=year:desc&from=0&size=10&timeout=1s


//带profile 查看elasticsearch 是如何查询的
GET /movies/_search?q=2012&df=title
{
  "profile": "true"
}


//泛查询,正对_all,所有字段
GET /movies/_search?q=2012
{
  "profile": "true"
}


//指定字段
GET /movies/_search?q=title:2012
{
  "profile": "true"
}


//使用引号，Phrase查询
GET /movies/_search?q=title:"Beautiful Mind"
{
  "profile": "true"
}


//Mind为泛查询
GET /movies/_search?q=title:Beautiful Mind
{
  "profile": "true"
}


//分组，Bool查询
GET /movies/_search?q=title:(Beautiful Mind)
{
  "profile": "true"
}


//bool查询,两个必须满足
GET /movies/_search?q=title:(Beautiful AND MIND)
{
  "profile": "true"
}


//bool查询,满足一个
GET /movies/_search?q=title:(Beautiful NOT Mind)
{
  "profile": "true"
}


//%2B 代表 + 号
GET /movies/_search?q=title:(Beautiful %2BMind)
{
  "profile": "true"
}


//范围查询
GET /movies/_search?q=year:>=1980
{
  "profile": "true"
}


//通配符查询
GET /movies/_search?q=title:b*
{
  "profile": "true"
}


//模糊匹配
GET /movies/_search?q=title:beautifl~1
{
  "profile": "true"
}


//模糊，近似度匹配
GET /movies/_search?q=title:"Lord Rings"~2
{
  "profile": "true"
}
```

```
搜索的高级用法 Request Body Search

POST /kibana_sample_data_ecommerce/_search
{
  "from": 10,
  "size": 20,
  "query": {
    "match_all": {}
  }
}


//对日期排序
POST /kibana_sample_data_ecommerce/_search
{
  "sort": [
    {"order_date":"desc"}
  ],
  "query": {
    "match_all": {}
  }
}


//source 过滤
POST /kibana_sample_data_ecommerce/_search
{
  "_source": ["order_date"],
  "query": {
    "match_all": {}
  }
}


//脚步字段
GET /kibana_sample_data_ecommerce/_search
{
  "script_fields": {
    "new_field": {
      "script": {
        "lang": "painless",
        "source": "doc['order_date'].value+'_hello'"
      }
    }
  },
  "query": {
    "match_all": {}
  }
}


//一起出现或出现一个
POST /movies/_search
{
  "query": {
    "match": {
      "title": "Last Christmas"
    }
  }
}


//同时出现
POST /movies/_search
{
  "query": {
    "match": {
      "title": {
        "query": "Last Christmas",
        "operator": "and"
      }
    }
  }
}


POST /movies/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "one love"
      }
    }
  }
}


POST /movies/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "one love",
        "slop": 1
      }
    }
  }
}
```

```
Query String 查询

POST /movies/_search
{
  "query": {
    "query_string": {
      "default_field": "title",
      "query": "one AND love"
    }
  }
}

POST /movies/_search
{
  "query": {
    "query_string": {
      "fields": ["title","genre"],
      "query": "(Grumpier AND Old) OR (Drama)"
    }
  }
}

```

```
Simple Query String 查询

POST /movies/_search
{
  "query": {
    "simple_query_string": {
      "query": "Beauty AND Day",
      "fields": ["title"]
    }
  }
}

POST /movies/_search
{
  "query": {
    "simple_query_string": {
      "query": "Sleeping Beauty",
      "fields": ["title"],
      "default_operator": "AND"
    }
  }
}
```

