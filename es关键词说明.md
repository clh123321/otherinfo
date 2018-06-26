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
filter | 过滤 |
must_not  | |
must_not  | |
### 2，结果关键词
关键词 | 说明 | 备注
---|---|---
hits | 返回结果集 |  跟size有关
total | 起始页码 |默认为0
