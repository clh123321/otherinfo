
### 0，
> [增删改查，映射，结构化查询，聚合](https://blog.csdn.net/xj626852095/article/details/54343182)
### 1，请求关键词
关键词 | 说明 | 备注
---|---|---
size | 表示查询多少条文档 |size默认为10，[size 超过10000结果解决方法](https://blog.csdn.net/qq_18145031/article/details/53489370)，[size 深度分页的缺陷](https://note.youdao.com/)，[解决深分页](https://blog.csdn.net/feifantiyan/article/details/54096138)
from | 表示从第几行开始 |默认为0
scroll | 游标(url增加上一次请求_scroll_id) |[Scroll (游标)API详解](https://blog.csdn.net/xj626852095/article/details/50708213)，[数据遍历和深度分页](http://lxwei.github.io/posts/%E4%BD%BF%E7%94%A8scroll%E5%AE%9E%E7%8E%B0Elasticsearch%E6%95%B0%E6%8D%AE%E9%81%8D%E5%8E%86%E5%92%8C%E6%B7%B1%E5%BA%A6%E5%88%86%E9%A1%B5.html)
order | 排序 |默认是按照doc_count倒序排列的， 可以改变默认情况 “order” : { “_count” : “asc” } 这是按照doc_count升序排列 “order” : { “_term” : “asc” } 这是按照字母表升序排列
term | 过滤 |用于精确匹配哪些值，比如数字，日期，布尔值或not_analyzed的字符串(未经分析的文本数据类型)
terms | 过滤|terms 跟 term 有点类似，但 terms 允许指定多个匹配条件。如果某个字段指定了多个值，那么文档需要一起去做匹配
range  | 过滤|允许我们按照指定范围查找一批数据范围操作符包含：<br/>gt :: 大于<br/>gte:: 大于等于<br/>lt :: 小于<br/>lte:: 小于等于
exists  | 过滤|exists 和 missing 过滤可以用于查找文档中是否包含指定字段或没有某个字段，类似于SQL语句中的IS_NULL条件
missing  | 过滤|exists 和 missing 过滤可以用于查找文档中是否包含指定字段或没有某个字段，类似于SQL语句中的IS_NULL条件
bool  | 过滤|过滤可以用来合并多个过滤条件查询结果的布尔逻辑，它包含一下操作符：<br/>must ::多个查询条件的完全匹配,相当于 and。<br/>must_not :: 多个查询条件的相反匹配，相当于 not。<br/>should ::至少有一个查询条件匹配, 相当于 or。
match_all |查询 |match_all 可以查询到所有文档，是没有查询条件下的默认语句
match | 查询 |查询是一个标准查询，不管你需要全文本查询还是精确查询基本上都要用到它
multi_match | 查询 | 查询允许你做match查询的基础上同时搜索多个字段
bool | 查询 | bool 查询与 bool过滤相似，用于合并多个查询子句。不同的是，bool过滤可以直接给出是否匹配成功， 而bool查询要计算每一个查询子句的_score（相关性分值）<br/>must::查询指定文档一定要被包含。<br/>must_not::查询指定文档一定不要被包含。<br/>should::查询指定文档，有则可以为文档相关性加分。
filter | 过滤 |         [过滤查询以及聚合](https://my.oschina.net/LucasZhu/blog/1504544)
aggs\aggregations  | 聚合 [聚合搜索总结](https://my.oschina.net/LucasZhu/blog/1504396) |两个主要概念：<br/>Buckets(桶)：<br/>满足某个条件的文档集合。<br/>Metrics(指标)：<br/>为某个桶中的文档计算得到的统计信息。<br>每个聚合只是简单地由一个或者多个桶，零个或者多个指标组合而成<br> ~~SELECT COUNT(color) FROM table GROUP BY color~~<br>COUNT(color)就相当于指标。GROUP BY color则相当于桶
terms | terms桶 |
avg | 平均指标 | avg指标嵌套在terms桶中
min | 最小指标 |
max | 最大指标 |
top_hits|  |
collapse ||
histogram | 柱状图桶 | 常规的histogram通常使用条形图来表示 
interval | 区间指标 | 间隔为20000意味着我们能够拥有区间[0-19999, 20000-39999, 等]
extended_stats |统计信息 指标| 包括[count、min、max、avg、sum、sum_of_squares、variance、std_deviation、std_deviation_bounds、upper、lower]
date_histogram |日期柱状图桶|date_histogram倾向于被装换为线图(Line Graph)来表达时间序列(Time Series)
format |  |
min_doc_count | 强制返回空桶 |
extended_bounds | 强制返回一整年的数据 |
post_filter、term | 过滤器 (先查询再过滤)| 过滤器不影响评分，而评分计算让搜索变得复杂，而且需要CPU资源，因而尽量使用过滤器，而且过滤器容易被缓存，进一步提升查询的整体性能。
filtered | 先过滤再查询，速度快 |
post_filter、range|范围过滤器|范围操作符包含：<br/>gt :: 大于<br/>gte:: 大于等于<br/>lt :: 小于<br/>lte:: 小于等于
exists|过滤器|过滤掉给定字段没有值的文档
missing|过滤器|
script|脚本过滤器|
type|类型过滤器|
limit|限定过滤器|
ids|标识符过滤器|
should、must|组合过滤器|
post_filter|后置过滤器|
aggs、filter|过滤桶(Filter Bucket)|
### 2，结果关键词
关键词 | 说明 | 备注
---|---|---
hits | 返回结果集 |  跟size有关
total | 起始页码 |默认为0
doc_count| 该词条的文档数量 |
### 3，请求样例
##### 1，post_filter(先查询再过滤)
请求
```
{
    "query" : {
        "match":{"color":"red"}
    },
    "post_filter":{
    	"term":{"make":"honda"}
    },
    "aggs" : {
        "single_avg_price": {
            "avg" : { "field" : "price" } 
        }
    }
}
```
结果 聚合查询调用的域是query的域，post_filter 过滤后的域
```
{
    "took": 25,
    "timed_out": false,
    "_shards": {
        "total": 5,
        "successful": 5,
        "failed": 0
    },
    "hits": {
        "total": 3,
        "max_score": 0.6931472,
        "hits": [
            {
                "_index": "cars",
                "_type": "transactions",
                "_id": "AV27esc_P4ExfZbT0LYK",
                "_score": 0.6931472,
                "_source": {
                    "price": 20000,
                    "color": "red",
                    "make": "honda",
                    "sold": "2014-11-05"
                }
            },
            {
                "_index": "cars",
                "_type": "transactions",
                "_id": "AV27esc_P4ExfZbT0LYF",
                "_score": 0.13353139,
                "_source": {
                    "price": 10000,
                    "color": "red",
                    "make": "honda",
                    "sold": "2014-10-28"
                }
            },
            {
                "_index": "cars",
                "_type": "transactions",
                "_id": "AV27esc_P4ExfZbT0LYG",
                "_score": 0.13353139,
                "_source": {
                    "price": 20000,
                    "color": "red",
                    "make": "honda",
                    "sold": "2014-11-05"
                }
            }
        ]
    },
    "aggregations": {
        "single_avg_price": {
            "value": 32500
        }
    }
}
```
##### 2,先过滤再查询，速度快
请求
```
{
    "query": {
        "bool": {
            "must": {
                "match": {
                    "color": "red"
                }
            }, 
            "filter": {
                "term": {
                    "make": "honda"
                }
            }
        }
    },
    "aggs" : {
        "single_avg_price": {
            "avg" : { "field" : "price" } 
        }
    }
}
```
结果 此bool中过滤器在聚合函数中可以生效。
```

```
##### 3，范围过滤器
请求
```
{
   "post_filter":{
         "range":{
             "price":{
                 "gte":10000,
                 "lte":30000
             }
         }
    }
}
```
结果
```
{
    "query": {
        "bool": {
            "must": {
                "match": {
                    "color": "red"
                }
            }, 
            "filter": {
                "range": {
                    "price": {
                    	"gte":10000,
                    	"lte":30000
                    }
                }
            }
        }
    },
    "aggs" : {
        "single_avg_price": {
            "avg" : { "field" : "price" } 
        }
    }
}
```
##### 4,exists过滤器
请求 过滤掉给定字段没有值的文档
```
{
   "post_filter":{
         "exists":{
             "field":"price"
         }
    }
}
```
结果 
```
```
##### 5，missing过滤器
请求 过滤掉给定字段没有值的文档
```
{
   "post_filter":{
         "missing":{
             "field":"year",
             "null_value":0,
             "existence":true
         }
    }
}
```
结果 
```
```
##### 5，脚本过滤器
请求 过滤掉发表在一个世纪以前的书
```
{
   "post_filter":{
         "script":{
             "script":"now - doc['year'].value > 100",
             "params":{"now":2012}
         }
    }
}
```
结果 
```
```
##### 6，类型过滤器
请求 当查询运行在多个索引上时，有用
```
{
   "post_filter":{
         "type":{
             "value":"book"
         }
    }
}
```
结果 
```
```
##### 7，限定过滤器
请求 限定每个分片返回的文档数
```
{
   "post_filter":{
         "limit":{
             "value":1
         }
    }
}
```
结果 
```
```
##### 8，标识符过滤器
请求 
```
{
   "post_filter":{
         "ids":{
             "type":["book"],
             "values":[1,2,3]
         }
    }
}
```
结果 
```
```
##### 9，组合过滤器
请求 
```
{
    "query": {
        "bool": {
            "must": {
                "range": {
                    "year": {
                        "gte": 1930, 
                        "lte": 1990
                    }
                }
            }, 
            "should": {
                "term": {
                    "available": true
                }
            }, 
            "boost": 1
        }
    }
}
```
结果 
```
```
##### 10，filtered查询
请求 
```
{
    "query": {
        "bool": {
            "filter": {
                "range": {
                    "price":{
                    	"gte":10000
                    }
                }
            }
        }
    },
    "aggs" : {
        "single_avg_price": {
            "avg" : { "field" : "price" } 
        }
    }
}
```
结果 从本质上而言，使用filtered查询和使用match查询并无区别，正如我们在上一章所讨论的那样。该查询(包含了一个过滤器)返回文档的一个特定子集，然后聚合工作在该子集上。
```
```
##### 11，过滤桶(Filter Bucket)
请求 
```
{
   "query":{
      "match": {
         "make": "ford"
      }
   },
   "aggs":{
      "recent_sales": {
         "filter": { 
            "range": {
               "sold": {
                  "from": "now-60M"
               }
            }
         },
         "aggs": {
            "average_price":{
               "avg": {
                  "field": "price" 
               }
            }
         }
      }
   }
}
```
结果 
```
{
    "took": 30,
    "timed_out": false,
    "_shards": {
        "total": 5,
        "successful": 5,
        "failed": 0
    },
    "hits": {
        "total": 2,
        "max_score": 0.9808292,
        "hits": [
            {
                "_index": "cars",
                "_type": "transactions",
                "_id": "AV2_X_JrP4ExfZbT0LYb",
                "_score": 0.9808292,
                "_source": {
                    "price": 30000,
                    "color": "green",
                    "make": "ford",
                    "sold": "2014-05-18"
                }
            },
            {
                "_index": "cars",
                "_type": "transactions",
                "_id": "AV2_X_JsP4ExfZbT0LYf",
                "_score": 0.2876821,
                "_source": {
                    "price": 25000,
                    "color": "blue",
                    "make": "ford",
                    "sold": "2014-02-12"
                }
            }
        ]
    },
    "aggregations": {
        "recent_sales": {
            "doc_count": 2,
            "average_price": {
                "value": 27500
            }
        }
    }
}
```
##### 12，后置过滤器(Post Filter)
请求  post_filter元素是一个顶层元素，只会对搜索结果进行过滤。
```
{
    "query": {
        "match": {
            "make": "ford"
        }
    },
    "post_filter": {    
        "term" : {
            "color" : "green"
        }
    },
    "aggs" : {
        "all_colors": {
            "terms" : { "field" : "color" }
        }
    },
    "size":0
}
```
结果 
```

```  
### C#
```
			_elasticClient.Search<T>(s => s
                .From(skip)
                .Filter(fd => fd.Term(f => f.Language, language))
                .Size(pageSize)
                .SearchType(SearchType.Count)
                .Query(
                    q => q.Wildcard(f => f.Title, query, 2.0)
                         || q.Wildcard(f => f.Description, query)
                )
                .Aggregations(agd =>
                    agd.Terms("groupId", tagd => tagd
                        .Field("groupId")
                        .Size(0)
                    .Aggregations(tagdaggs =>
                        tagdaggs.TopHits("top_tag_hits", thagd => thagd
                            .Size(1)))
                    )
                )
                );

                var groupIdAggregation = result.Aggs.Terms("groupId");

                var topHits =
                    groupIdAggregation.Items.Select(key => key.TopHits("top_tag_hits"))
                        .SelectMany(topHitMetric => topHitMetric.Documents<ProductDocument>()).ToList();
```