# FMDB分页查询

```objective-c
NSString *str = [NSString stringWithFormat:@"select * from test order by id ASC LIMIT %d,10;", 0];

test: 表名
%d: 表示从第几个数据开始
10: 表示每页10个数据

比如我想每页10个数据
那么(前面都是一样的,这里只写末尾几个关键代码)
第一页: %d,10;” 0]
第二页: %d,10;” 10]
第三页: %d,10;” 20]
…
第n页: %d,10;” 10 * (n - 1)]
```

