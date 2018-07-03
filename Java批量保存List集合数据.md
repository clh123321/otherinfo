### 1，通过fox循环批量保存
```
int result = 0;
int pageSize = 1000;
List<AdvertisingPushDataEntity> list = new ArrayList<>();
List<AdvertisingToShowEntity> resultList = new ArrayList<>();
for (int i = 0; i < list.Count; i++)
{
    //保存list中
    resultList.Add(requestResult);
    //判断是否是pageSize取余为0保存
    if (((i + 1) % pageSize) == 0)
    {
        result = result + BulkSave(resultList);
        //清空进行下一次循环
        resultList = new ArrayList<>();
    }
}

//进行最后一次批量插入
if (resultList.Count > 0)
{
    result = result + BulkSave(resultList);
}
```
### 2，先计算总页数在通过页数循环批量保存
#### 2.1 分页计算总页数算法 ，推荐一种 Java的写法 
```
int totalPageNum = (totalRecord  +  pageSize  - 1) / pageSize;
```
```
int result = 0;
int pageSize = 1000;
List<AdvertisingPushDataEntity> list = new ArrayList<>();
int totalPageNum = (list  +  pageSize  - 1) / pageSize;

for (int i = 0; i < totalPageNum; i++) {
    List<LoanFinanceToEsEntity> resultList2 = JinqStream.from(resultList).skip(i*pageSize).limit((i+1)*pageSize).toList();
    result = result + BulkSave(resultList2);
}
```
#### 2.2 使用Math.ceil()函数，返回大于或者等于指定表达式的最小整数头文件
```
int b = (int)Math.ceil(totalCounts/pageSize);
```
