\1. 下面一个简单的使用正则表达式的一个例子：NSRegularExpression 类

```
-(void)parseString{

//组装一个字符串，需要把里面的网址解析出来

NSString *urlString=@"sfdsfhttp://www.[baidu.com](http://baidu.com/)";

 

//NSRegularExpression类里面调用表达的方法需要传递一个NSError的参数。下面定义一个

 NSError *error;

//http+:[^\\s]* 这个表达式是检测一个网址的。

  NSRegularExpression *regex = [NSRegularExpression regularExpressionWithPattern:@"http+:[^\\s]*" options:0 error:&error];

  if (regex != nil) {

  NSTextCheckingResult *firstMatch=[regex firstMatchInString:urlString options:0range:NSMakeRange(0, [urlString length])];

  if (firstMatch) {

   NSRange resultRange = [firstMatch rangeAtIndex:0]; //等同于 firstMatch.range --- 相匹配的范围

   //从urlString当中截取数据

  NSString *result=[urlString substringWithRange:resultRange];

  //输出结果

  NSLog(@"%@",result);

  }

 

  }

}
```



 

2.使用正则表达式来判断

```objective-c
//初始化一个NSRegularExpression 对象，并设置检测对象范围为：0-9 

NSRegularExpression *regex2 = [NSRegularExpression regularExpressionWithPattern:@"^[0-9]*$" options:0 error:nil];

​    if (regex2)

​    {//对象进行匹配

​       NSTextCheckingResult *result2 = [regex2 firstMatchInString:textField.text options:0 range:NSMakeRange(0, [textField.text length])];

​      if (result2) {

​      }

}
```



## 　**一、什么是正则表达式**

**接下来我介绍另一种使用正则表达式匹配的方法：**

**NSRegularExpression**

**如果正则表达式掌握的话，其实使用起来很简单，主要有三种：**

**一、创建正则表达式**

```objective-c
1. **// @param pattern 正则表达式** 
2. **// @param options 正则表达式的选项** 
3. **// @return RegularExpression对象** 
4. **+ (****NSRegularExpression** ***)regularExpressionWithPattern:(****NSString** ***)pattern** 
5. ​                       **options****:(NSRegularExpressionOptions)options** 
6. ​                        **error****:(****NSError** ***** **_Nullable** ***)error** 
7. **/\*** 
8.   **enum {** 
9.    **NSRegularExpressionCaseInsensitive       = 1 << 0,  // 不区分大小写的** 
10.    **NSRegularExpressionAllowCommentsAndWhitespace = 1 << 1,  // 忽略空格和# -** 
11.    **NSRegularExpressionIgnoreMetacharacters    = 1 << 2,  // 整体化** 
12.    **NSRegularExpressionDotMatchesLineSeparators  = 1 << 3,  // 匹配任何字符，包括行分隔符** 
13.    **NSRegularExpressionAnchorsMatchLines      = 1 << 4,  // 允许^和$在匹配的开始和结束行** 
14.    **NSRegularExpressionUseUnixLineSeparators    = 1 << 5,  // (查找范围为整个的话无效)** 
15.    **NSRegularExpressionUseUnicodeWordBoundaries  = 1 << 6  // (查找范围为整个的话无效)** 
16.   **}** 
17. ***/** 
```

**二、使用正则表达式的Searchig字符串**

```obj
**// @param string 匹配的字符串** 

1. **// @param options 匹配的规则** 
2. **// @param range 匹配的范围** 
3. **// @return 获得符合匹配的个数(通过等于0，来验证邮箱，电话...，代替NSPredicate)** 
4. **- (NSUInteger)numberOfMatchesInString:(****NSString** ***)string** 
5. ​               **options****:(NSMatchingOptions)options** 
6. ​                **range****:(NSRange)range** 
7.  
8. **// @param string 匹配的字符串** 
9. **// @param options 匹配的规则** 
10. **// @param range 匹配的范围** 
11. **// @param block 列举符合规则的字符串** 
12. **- (****void****)enumerateMatchesInString:(****NSString** ***)string** 
13. ​             **options****:(NSMatchingOptions)options** 
14. ​              **range****:(NSRange)range** 
15. ​           **usingBlock****:(****void** **(^)(****NSTextCheckingResult** ***result,** 
16. ​                      **NSMatchingFlags flags,** 
17. ​                      **BOOL****BOOL** ***stop))block;** 
18.  
19. **// @param string 匹配的字符串** 
20. **// @param options 匹配的规则** 
21. **// @param range 匹配的范围** 
22. **// @return 所有匹配结果的集合(适合从一段字符串中提取我们想要匹配的所有数组)** 
23. **- (NSArray<****NSTextCheckingResult** ***> \*)matchesInString:(****NSString** ***)string** **options****:(NSMatchingOptions)options** **range****:(NSRange)range;** 
24.  
25. **// @param string 匹配的字符串** 
26. **// @param options 匹配的规则** 
27. **// @param range 匹配的范围** 
28. **// @return 返回第一个匹配的结果。匹配的结果保存在 NSTextCheckingResult 类型中** 
29. **- (****NSTextCheckingResult** ***)firstMatchInString:(****NSString** ***)string** 
30. ​                   **options****:(NSMatchingOptions)options** 
31. ​                    **range****:(NSRange)range** 
32.  
33. **// @param string 匹配的字符串** 
34. **// @param options 匹配的规则** 
35. **// @param range 匹配的范围** 
36. **// @return 返回第一个正确匹配结果字符串的NSRange** 
37. **- (NSRange)rangeOfFirstMatchInString:(****NSString** ***)string** 
38. ​               **options****:(NSMatchingOptions)options** 
39. ​                **range****:(NSRange)range** 
40.  
41. **// 下面2个枚举貌似都没什么意义,除了在block方法中,一般情况下,直接给0吧**  
42.   **/\**** 
43.    *** enum {** 
44.    **NSMatchingReportProgress     = 1 << 0,** 
45.    **NSMatchingReportCompletion    = 1 << 1,** 
46.    **NSMatchingAnchored        = 1 << 2,** 
47.    **NSMatchingWithTransparentBounds = 1 << 3,** 
48.    **NSMatchingWithoutAnchoringBounds = 1 << 4** 
49.    **};** 
50.    **typedef NSUInteger NSMatchingOptions;** 
51.    ***/**  
52.  
53.   **/\** 此枚举值只在5.block方法中用到** 
54.    *** enum {** 
55.    **NSMatchingProgress        = 1 << 0,** 
56.    **NSMatchingCompleted       = 1 << 1,** 
57.    **NSMatchingHitEnd         = 1 << 2,** 
58.    **NSMatchingRequiredEnd      = 1 << 3,** 
59.    **NSMatchingInternalError     = 1 << 4** 
60.    **};** 
61.    **typedef NSUInteger NSMatchingFlags;** 
62.    ***/****</span>** 
```

**三、使用正则表达式替换字符串**

**[objc]** [view plain](http://blog.csdn.net/hmh007/article/details/71191981#) [copy](http://blog.csdn.net/hmh007/article/details/71191981#)

1. **<span style=****"font-size:14px;"****>****// @param string 匹配的字符串** 
2. **// @param options 匹配的规则** 
3. **// @param range 匹配的范围** 
4. **// @param template 替换的字符串** 
5. **// @return 转换匹配字符串的数目** 
6. **- (NSUInteger)replaceMatchesInString:(****NSMutableString** ***)string** 
7. ​               **options****:(NSMatchingOptions)options** 
8. ​                **range****:(NSRange)range** 
9. ​            **withTemplate****:(****NSString** ***)****template** 
10.  
11. **// @param string 匹配的字符串** 
12. **// @param options 匹配的规则** 
13. **// @param range 匹配的范围** 
14. **// @param template 替换的字符串**  
15. **// @return 返回一个替换后的字符串** 
16. **- (****NSString** ***)stringByReplacingMatchesInString:(****NSString** ***)string** 
17. ​                    **options****:(NSMatchingOptions)options** 
18. ​                     **range****:(NSRange)range** 
19. ​                 **withTemplate****:(****NSString** ***)****template****</span>** 

**下面直接上代码，一个小Demo，想要源码的可以私我，前面的博客有联系方法。**

**[objc]** [view plain](http://blog.csdn.net/hmh007/article/details/71191981#) [copy](http://blog.csdn.net/hmh007/article/details/71191981#)

1. **///正则表达式的基本使用** 
2. **void** **test****2** **()** 
3. **{** 
4.   **NSString** ***userName =** **@"asdavasvadv231414as"****;** 
5.    
6.   **/\**** 
7.    **使用正则表达式的步骤：** 
8.    **1.创建正则表达式对象** 
9.    
10.    **2.利用正则表达式对象 来测试 相应的字符串** 
11.    ***/** 
12.    
13.    
14.   **//创建正则表达式** 
15.   **//Pattern : 样式、规则** 
16.    
17.   **// “[]”只会查找内部的某一个字符而已** 
18.   **//    NSString \*Pattern = @"[0-9]";** 
19.   **//    NSString \*Pattern = @"[a-zA-Z]";** 
20.    
21.   **//代表找两个连在一起的数字** 
22.   **//    NSString \*Pattern = @"[0-9][0-9]";** 
23.   **NSString** ***Pattern =** **@"\\d\\d"****;** **//两个//代表两个数字** 
24.   **//    NSString \*Pattern = @"\\d{3}a{2}";** 
25.    
26.   **//找到两到四个数字的** 
27.   **//    NSString \*Pattern1 = @"\\d{2,4}";** 
28.    
29.   **//找到特殊字符 ? + \*** 
30.   **// ? : 0个或者1个** 
31.   **// + : 至少一个** 
32.   **// \* : 0个或者多个** 
33.   **//    NSString \*Pattern2 = @"\\d?";** 
34.    
35.    
36.   **//表示找一个数字并且要以数字开头的“^” ("$"表示以它结束)** 
37.   **//    NSString \*Pattern1 = @"^\\d";** 
38.   **//    NSString \*Pattern2 = @"\\d{3}$";** 
39.    
40.   **//表示以数字开头并且以数字结尾 ("."点表示除换行符以外的任意字符，\*表示0个或多个)** 
41.   **//    NSString \*Pattern = @"^\\d.\*\\d$";** 
42.    
43.   **NSRegularExpression** ***regex = [[NSRegularExpression** **alloc****]** **initWithPattern****:Pattern** **options****:****0** **error****:nil****];** 
44.    
45.   **//2.测试字符串** 
46.   **NSArray** ***results = [regex** **matchesInString****:userName** **options****:****0** **range****:NSMakeRange(****0****, userName****.length****)];** 
47.    
48.   **//3.遍历结果** 
49.   **for** **(****NSTextCheckingResult** ***result in results) {** 
50. ​     
51. ​    **NSLog(****@"%@ , %@"****,NSStringFromRange(result****.range****),[userName** **substringWithRange****:result****.range****]);** 
52.   **}** 
53.    
54.   **NSLog(****@"%zd"****,results****.count****);** 
55. **}** 

　　正则表达式，又称正规表示法，是对字符串操作的一种逻辑公式。正则表达式可以检测给定的字符串是否符合我们定义的逻辑，也可以从字符串中获取我们想要的特定部分。它可以迅速地用极简单的方式达到字符串的复杂控制。

![img](data:image/jpeg;base64,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)

## 　**二、正则表达式的语法**

　　看一个过滤纯数字的例子

\- (BOOL)validateNumber:(NSString *) textString

{

NSString* number=@"^[0-9]+$";

NSPredicate *numberPre = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",number];

return [numberPre evaluateWithObject:textString];

}

　　其中下述语句就是一个正则表达式

@"^[0-9]+$"

　　它代表了字符串中只能包含>=1个0-9的数字，语法是不是有一些怪异？

　　下面我们先撇开iOS中的正则表达式的语法，用通俗的正则表达式语法来为介绍一下。（iOS语法与通俗的正则表达式语法相同，不同在于对转义字符的处理上(语言类的都相同)）

　　语法：

　　首先，特殊符号’^'和’$'。他们的作用是分别指出一个字符串的开始和结束。eg：

　　“^one”：表示所有以”one”开始的字符串（”one cat”，”one123″，·····）；

　　类似于:- (BOOL)hasPrefix:(NSString *)aString;

　　“a dog$”：表示所以以”a dog”结尾的字符串（”it is a dog”，·····）；

　　类似于:- (BOOL)hasSuffix:(NSString *)aString;

　　“^apple$”：表示开始和结尾都是”apple”的字符串，这个是唯一的~；

　　“banana”：表示任何包含”banana”的字符串。

　　类似于 iOS8的新方法- (BOOL)containsString:(NSString *)aString,搜索子串用的。

　　‘*’，’+'和’?'这三个符号，表示一个或N个字符重复出现的次数。它们分别表示“没有或更多”（[0,+∞]取整），“一次或更多”（[1,+∞]取整），“没有或一次”（[0,1]取整）。下面是几个例子：

　　“ab*”：表示一个字符串有一个a后面跟着零个或若干个b（”a”, “ab”, “abbb”,……）；

　　“ab+”：表示一个字符串有一个a后面跟着至少一个b或者更多（ ”ab”, “abbb”,……）；

　　“ab?”：表示一个字符串有一个a后面跟着零个或者一个b（ ”a”, “ab”）；

　　“a?b+$”：表示在字符串的末尾有零个或一个a跟着一个或几个b（ ”b”, “ab”,”bb”,”abb”,……）。

　　可以用大括号括起来（{}），表示一个重复的具体范围。例如

　　“ab{4}”：表示一个字符串有一个a跟着4个b（”abbbb”）；

　　“ab{1,}”：表示一个字符串有一个a跟着至少1个b（”ab”,”abb”,”abbb”,……)；

　　“ab{3,4}”：表示一个字符串有一个a跟着3到4个b（”abbb”,”abbbb”)。

　　那么，“*”可以用{0，}表示，“+”可以用{1，}表示，“?”可以用{0，1}表示

　　注意：可以没有下限，但是不能没有上限！例如“ab{,5}”是错误的写法

　　“ | ”表示“或”操作：

　　“a|b”：表示一个字符串里有”a”或者”b”；

　　“(a|bcd)ef”：表示”aef”或”bcdef”；

　　“(a|b)*c”：表示一串”a”"b”混合的字符串后面跟一个”c”；

　　方括号”[ ]“表示在括号内的众多字符中，选择1-N个括号内的符合语法的字符作为结果，例如

　　“[ab]“：表示一个字符串有一个”a”或”b”（相当于”a|b”）；

　　“[a-d]“：表示一个字符串包含小写的’a'到’d'中的一个（相当于”a|b|c|d”或者”[abcd]“）；

　　“^[a-zA-Z]“：表示一个以字母开头的字符串；

　　“[0-9]a”：表示a前有一位的数字；

　　“[a-zA-Z0-9]$”：表示一个字符串以一个字母或数字结束。

　　“.”匹配除“\r\n”之外的任何单个字符：

　　“a.[a-z]“：表示一个字符串有一个”a”后面跟着一个任意字符和一个小写字母；

　　“^.{5}$”：表示任意1个长度为5的字符串；

　　“\num” 其中num是一个正整数。表示”\num”之前的字符出现相同的个数，例如

　　“(.)\1″：表示两个连续的相同字符。

　　“10\{1,2\}” : 表示数字1后面跟着1或者2个0 (“10″,”100″)。

　　” 0\{3,\} ” 表示数字为至少3个连续的0 （“000”，“0000”，······）。

　　在方括号里用’^'表示不希望出现的字符，’^'应在方括号里的第一位。

　　“@[^a-zA-Z]4@”表示两个”@”中不应该出现字母）。

　　常用的还有：

　　“ \d ”匹配一个数字字符。等价于[0-9]。

　　“ \D”匹配一个非数字字符。等价于[^0-9]。

　　“ \w ”匹配包括下划线的任何单词字符。等价于“[A-Za-z0-9_]”。

　　“ \W ”匹配任何非单词字符。等价于“[^A-Za-z0-9_]”。

　　iOS中书写正则表达式，碰到转义字符，多加一个“\”,例如：

　　全数字字符：@”^\\d\+$”

##  

## **iOS中的正则运用**

### **一、NSRegularExpression**

#### **1. 正则表达式的创建**

**+ (nullable NSRegularExpression \*)regularExpressionWithPattern:(NSString \*)pattern options:(NSRegularExpressionOptions)options error:(NSError \**)error;**

**- (nullable instancetype)initWithPattern:(NSString \*)pattern options:(NSRegularExpressionOptions)options error:(NSError \**)error**

**该类中的属性**

- **pattern** **返回正则表达式模式**
- **options** **返回创建正则表达式选项时使用的选项**
- **numberOfCaptureGroups** **返回正则表达式模式**

**options 定义的枚举类型如下：**

  **typedef NS_OPTIONS(NSUInteger, NSRegularExpressionOptions) {**

​    **NSRegularExpressionCaseInsensitive       = 1 << 0, //不区分大小写的**

​    **NSRegularExpressionAllowCommentsAndWhitespace = 1 << 1, //忽略空格和# -**

​    **NSRegularExpressionIgnoreMetacharacters    = 1 << 2, //整体化**

​    **NSRegularExpressionDotMatchesLineSeparators  = 1 << 3, //匹配任何字符，包括行分隔符**

​    **NSRegularExpressionAnchorsMatchLines      = 1 << 4, //允许^和$在匹配的开始和结束行**

​    **NSRegularExpressionUseUnixLineSeparators    = 1 << 5, //(查找范围为整个无效)**

​    **NSRegularExpressionUseUnicodeWordBoundaries  = 1 << 6 //(查找范围为整个无效)**

   **};**

#### **2. 搜索字符串**

**//枚举允许Block处理每个正则表达式匹配的字符串**

**- (void)enumerateMatchesInString:(NSString \*)string options:(NSMatchingOptions)options range:(NSRange)range usingBlock:(void (NS_NOESCAPE ^)(NSTextCheckingResult \* _Nullable result, NSMatchingFlags flags, BOOL \*stop))block;**

**//返回一个数组，包含字符串中正则表达式的所有匹配项**

**- (NSArray<NSTextCheckingResult \*> \*)matchesInString:(NSString \*)string options:(NSMatchingOptions)options range:(NSRange)range;**

**//返回字符串指定范围内匹配数**

**- (NSUInteger)numberOfMatchesInString:(NSString \*)string options:(NSMatchingOptions)options range:(NSRange)range;**

**//返回字符串指定范围内第一个匹配项。**

**- (nullable NSTextCheckingResult \*)firstMatchInString:(NSString \*)string options:(NSMatchingOptions)options range:(NSRange)range;**

**//返回字符串指定范围内第一个匹配的范围**

**- (NSRange)rangeOfFirstMatchInString:(NSString \*)string options:(NSMatchingOptions)options range:(NSRange)range;**

**NSMatchingOptions的定义如下:**

**typedef NS_OPTIONS(NSUInteger, NSMatchingOptions) {**

  **NSMatchingReportProgress     = 1 << 0,    /\* 在长时间运行的匹配操作中定期调用Block \*/**

  **NSMatchingReportCompletion    = 1 << 1,    /\* 完成任何匹配后，调用Block一次\*/**

  **NSMatchingAnchored        = 1 << 2,    /\*指定匹配仅限于搜索范围开始时的匹配 \*/**

  **NSMatchingWithTransparentBounds = 1 << 3,    /\* 定匹配可以检查超出搜索范围的范围的字符串的部分，以用于诸如字边界检测，前瞻等。如果搜索范围包含整个字符串，该常量将不起作用 \*/**

  **NSMatchingWithoutAnchoringBounds = 1 << 4    /\* 指定^并且$不会自动匹配搜索范围的开始和结束，但仍将与整个字符串的开头和结尾相匹配。如果搜索范围包含整个字符串，则该常量不起作用 \*/**

**};**

#### **3.替换字符串**

**//返回与模板字符串替换的匹配正则表达式的新字符串**

**- (NSString \*)stringByReplacingMatchesInString:(NSString \*)string options:(NSMatchingOptions)options range:(NSRange)range withTemplate:(NSString \*)templ;**

**//返回替换的个数**

**- (NSUInteger)replaceMatchesInString:(NSMutableString \*)string options:(NSMatchingOptions)options range:(NSRange)range withTemplate:(NSString \*)templ;**

**//自定义替换功能**

**- (NSString \*)replacementStringForResult:(NSTextCheckingResult \*)result inString:(NSString \*)string offset:(NSInteger)offset template:(NSString \*)templ;**

**//通过根据需要添加反斜杠转义来返回模板字符串，以保护符合模式元字符的任何字符**

**+ (NSString \*)escapedTemplateForString:(NSString \*)string;**

**使用示例**

  **NSString \*str = @"aabbcccdeaargdo14141214aaghfh56821d3gad4";**

  **NSRegularExpression \*expression = [NSRegularExpression regularExpressionWithPattern:@"aa" options:NSRegularExpressionCaseInsensitive error:NULL];**

  **if (expression != nil) {**

​    **//匹配到的第一组**

​    **NSTextCheckingResult \*firstMatch = [expression firstMatchInString:str options:NSMatchingReportProgress range:NSMakeRange(0, str.length)];**

​    **NSRange range = [firstMatch rangeAtIndex:0];**

​    **NSString \*result = [str substringWithRange:range];**

​    **NSLog(@"匹配到的第一组:%@",result);**

​    **//匹配到的个数**

​    **NSInteger number = [expression numberOfMatchesInString:str options:NSMatchingReportProgress range:NSMakeRange(0, str.length)];**

​    **NSLog(@"匹配到的个数%ld",number);**

​    **//配到到的所有数据**

​    **NSArray \*allMatch = [expression matchesInString:str options:NSMatchingReportProgress range:NSMakeRange(0, str.length)];**

​    **for (int i = 0; i < allMatch.count; i ++) {**

​      **NSTextCheckingResult \*matchItem = allMatch[i];**

​      **NSRange range = [matchItem rangeAtIndex:0];**

​      **NSString \*result = [str substringWithRange:range];**

​      **NSLog(@"匹配到的数据:%@",result);**

​    **}**

​    **//匹配到第一组的位置**

​    **NSRange firstRange = [expression rangeOfFirstMatchInString:str options:NSMatchingReportProgress range:NSMakeRange(0, str.length)];**

​    **NSLog(@"匹配到第一组的位置:开始位置%lu--长度%lu",(unsigned long)firstRange.location,(unsigned long)firstRange.length);**

​    

​    **//替换字符串**

​    **NSString \*resultStr = [expression stringByReplacingMatchesInString:str options:NSMatchingReportProgress range:NSMakeRange(0, str.length) withTemplate:@"bbbb"];**

​    **NSLog(@"替换后的字符串:%@",resultStr);**

​    

​    **NSInteger resultNum = [expression replaceMatchesInString:[str mutableCopy] options:NSMatchingReportProgress range:NSMakeRange(0, str.length) withTemplate:@"bbbb"];**

​    **NSLog(@"替换的个数;%ld",(long)resultNum);**

  **}**

**打印log:**

**2017-08-13 23:28:53.898 NSRegularExpressionDemo[82046:8220904] 匹配到的第一组:aa**

**NSRegularExpressionDemo[82046:8220904] 匹配到的个数3**

**NSRegularExpressionDemo[82046:8220904] 匹配到的数据:aa**

**NSRegularExpressionDemo[82046:8220904] 匹配到的数据:aa**

**NSRegularExpressionDemo[82046:8220904] 匹配到的数据:aa**

**NSRegularExpressionDemo[82046:8220904] 匹配到第一组的位置:开始位置0--长度2**

**NSRegularExpressionDemo[82046:8220904] 替换后的字符串:bbbbbbcccdebbbbrgdo14141214bbbbghfh56821d3gad4**

**NSRegularExpressionDemo[82046:8220904] 替换的个数;3**

### **二、字符串**

**//NSStringCompareOptions --> NSRegularExpressionSearch**

**- (NSRange)rangeOfString:(NSString \*)searchString options:(NSStringCompareOptions)mask;**

**- (NSRange)rangeOfString:(NSString \*)searchString options:(NSStringCompareOptions)mask range:(NSRange)rangeOfReceiverToSearch;**

**- (NSRange)rangeOfString:(NSString \*)searchString options:(NSStringCompareOptions)mask range:(NSRange)rangeOfReceiverToSearch locale:(nullable NSLocale \*)locale**

**从上面的api可以看出，只能匹配到第一组**

**使用示例**

  **NSString \*str = @"aabbcccdeaargdo14141214aaghfh56821d3gad4";**

  **NSRange strMatchStr = [str rangeOfString:@"aa" options:NSRegularExpressionSearch];**

  **NSLog(@"匹配到字符串的位置:开始位置%lu--长度%lu",(unsigned long)strMatchStr.location,(unsigned long)strMatchStr.length)**

**打印log:**

**NSRegularExpressionDemo[82080:8224265] 匹配到字符串的位置:开始位置0--长度2**

### **三、谓词**

**使用示例**

  **NSString \*str2 = @"aabbcc";**

  **NSPredicate \*predicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",@"^aa(.)\*cc$"];**

  **BOOL isMatch = [predicate evaluateWithObject:str2];**

  **NSLog(@"匹配的结果:%d",isMatch);**

**打印log:**

**NSRegularExpressionDemo[82679:8253019] 匹配的结果:1**

## 

##  

## 　**四、常用的正则表达式**

　　以下红色字符串是常用的正则表达式（以下正则表达式来自百度百科）

　　1.验证用户名和密码：”^[a-zA-Z]\w{5,15}$”

　　2.验证电话号码：（”^(\\d{3,4}-)\\d{7,8}$”）

　　eg：021-68686868 0511-6868686；

　　3.验证手机号码：”^1[3|4|5|7|8][0-9]\\d{8}$”；

　　4.验证身份证号（15位或18位数字）：”\\d{14}[[0-9],0-9xX]”；

　　5.验证Email地址：(“^\\w+([-+.]\\w+)*@\\w+([-.]\\w+)*\.\\w+([-.]\\w+)*$”)；

　　6.只能输入由数字和26个英文字母组成的字符串：(“^[A-Za-z0-9]+$”) ;

　　7.整数或者小数：^[0-9]+([.]{0,1}[0-9]+){0,1}$

　　8.只能输入数字：”^[0-9]*$”。

　　9.只能输入n位的数字：”^\\d{n}$”。

　　10.只能输入至少n位的数字：”^\\d{n,}$”。

　　11.只能输入m~n位的数字：”^\\d{m,n}$”。

　　12.只能输入零和非零开头的数字：”^(0|[1-9][0-9]*)$”。

　　13.只能输入有两位小数的正实数：”^[0-9]+(.[0-9]{2})?$”。

　　14.只能输入有1~3位小数的正实数：”^[0-9]+(\.[0-9]{1,3})?$”。

　　15.只能输入非零的正整数：”^\+?[1-9][0-9]*$”。

　　16.只能输入非零的负整数：”^\-[1-9][]0-9″*$。

　　17.只能输入长度为3的字符：”^.{3}$”。

　　18.只能输入由26个英文字母组成的字符串：”^[A-Za-z]+$”。

　　19.只能输入由26个大写英文字母组成的字符串：”^[A-Z]+$”。

　　20.只能输入由26个小写英文字母组成的字符串：”^[a-z]+$”。

　　21.验证是否含有^%&’,;=?$\”等字符：”[^%&',;=?$\x22]+”。

　　22.只能输入汉字：”^[\u4e00-\u9fa5]{0,}$”。

　　23.验证URL：”^http://([\\w-]+\.)+[\\w-]+(/[\\w-./?%&=]*)?$”。

　　24.验证一年的12个月：”^(0?[1-9]|1[0-2])$”正确格式为：”01″～”09″和”10″～”12″。

　　25.验证一个月的31天：”^((0?[1-9])|((1|2)[0-9])|30|31)$”正确格式为；”01″～”09″、”10″～”29″和“30”~“31”。

　　26.获取日期正则表达式：\\d{4}[年|\-|\.]\\d{\1-\12}[月|\-|\.]\\d{\1-\31}日?

　　评注：可用来匹配大多数年月日信息。

　　27.匹配双字节字符(包括汉字在内)：[^\x00-\xff]

　　评注：可以用来计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）

　　28.匹配空白行的正则表达式：\n\s*\r

　　评注：可以用来删除空白行

　　29.匹配HTML标记的正则表达式：<(\S*?)[^>]*>.*?</>|<.*? />

　　评注：网上流传的版本太糟糕，上面这个也仅仅能匹配部分，对于复杂的嵌套标记依旧无能为力

　　30.匹配首尾空白字符的正则表达式：^\s*|\s*$

　　评注：可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式

　　31.匹配网址URL的正则表达式：[a-zA-z]+://[^\s]*

　　评注：网上流传的版本功能很有限，上面这个基本可以满足需求

　　32.匹配帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$

　　评注：表单验证时很实用

　　33.匹配腾讯QQ号：[1-9][0-9]\{4,\}

　　评注：腾讯QQ号从10 000 开始

　　34.匹配中国邮政编码：[1-9]\\d{5}(?!\d)

　　评注：中国邮政编码为6位数字

　　35.匹配ip地址：((2[0-4]\\d|25[0-5]|[01]?\\d\\d?)\.){3}(2[0-4]\\d|25[0-5]|[01]?\\d\\d?)。

　　下面给出正则表达式的元字符（来自百度百科）

## 　**五、正则表达式中的元字符**

 

| 元字符       | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| \            | 将下一个字符标记为一个特殊字符、或一个原义字符、或一个向后引用、或一个八进制转义符。例如，“\\n”匹配\n。“\n”匹配换行符。序列“\\”匹配“\”而“\(”则匹配“(”。 |
| ^            | 匹配输入字符串的开始位置。如果设置了RegExp对象的Multiline属性，^也匹配“\n”或“\r”之后的位置。 |
| $            | 匹配输入字符串的结束位置。如果设置了RegExp对象的Multiline属性，$也匹配“\n”或“\r”之前的位置。 |
| *            | 匹配前面的子表达式零次或多次(大于等于0次)。例如，zo*能匹配“z”，“zo”以及“zoo”。*等价于{0,}。 |
| +            | 匹配前面的子表达式一次或多次(大于等于1次）。例如，“zo+”能匹配“zo”以及“zoo”，但不能匹配“z”。+等价于{1,}。 |
| ?            | 匹配前面的子表达式零次或一次。例如，“do(es)?”可以匹配“do”或“does”中的“do”。?等价于{0,1}。 |
| {n}          | n是一个非负整数。匹配确定的n次。例如，“o{2}”不能匹配“Bob”中的“o”，但是能匹配“food”中的两个o。 |
| {n,}         | n是一个非负整数。至少匹配n次。例如，“o{2,}”不能匹配“Bob”中的“o”，但能匹配“foooood”中的所有o。“o{1,}”等价于“o+”。“o{0,}”则等价于“o*”。 |
| {n,m}        | m和n均为非负整数，其中n<=m。最少匹配n次且最多匹配m次。例如，“o{1,3}”将匹配“fooooood”中的前三个o。“o{0,1}”等价于“o?”。请注意在逗号和两个数之间不能有空格。 |
| ?            | 当该字符紧跟在任何一个其他限制符（*,+,?，{n}，{n,}，{n,m}）后面时，匹配模式是非贪婪的。非贪婪模式尽可能少的匹配所搜索的字符串，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。例如，对于字符串“oooo”，“o+?”将匹配单个“o”，而“o+”将匹配所有“o”。 |
| .点          | 匹配除“\r\n”之外的任何单个字符。要匹配包括“\r\n”在内的任何字符，请使用像“[\s\S]”的模式。 |
| (pattern)    | 匹配pattern并获取这一匹配。所获取的匹配可以从产生的Matches集合得到，在VBScript中使用SubMatches集合，在JScript中则使用$0…$9属性。要匹配圆括号字符，请使用“\(”或“\)”。 |
| (?:pattern)  | 匹配pattern但不获取匹配结果，也就是说这是一个非获取匹配，不进行存储供以后使用。这在使用或字符“(\|)”来组合一个模式的各个部分是很有用。例如“industr(?:y\|ies)”就是一个比“industry\|industries”更简略的表达式。 |
| (?=pattern)  | 正向肯定预查，在任何匹配pattern的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。例如，“Windows(?=95\|98\|NT\|2000)”能匹配“Windows2000”中的“Windows”，但不能匹配“Windows3.1”中的“Windows”。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。 |
| (?!pattern)  | 正向否定预查，在任何不匹配pattern的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。例如“Windows(?!95\|98\|NT\|2000)”能匹配“Windows3.1”中的“Windows”，但不能匹配“Windows2000”中的“Windows”。 |
| (?<=pattern) | 反向肯定预查，与正向肯定预查类似，只是方向相反。例如，“(?<=95\|98\|NT\|2000)Windows”能匹配“2000Windows”中的“Windows”，但不能匹配“3.1Windows”中的“Windows”。 |
| (?<!pattern) | 反向否定预查，与正向否定预查类似，只是方向相反。例如“(?<!95\|98\|NT\|2000)Windows”能匹配“3.1Windows”中的“Windows”，但不能匹配“2000Windows”中的“Windows”。 |
| x\|y         | 匹配x或y。例如，“z\|food”能匹配“z”或“food”。“(z\|f)ood”则匹配“zood”或“food”。 |
| [xyz]        | 字符集合。匹配所包含的任意一个字符。例如，“[abc]”可以匹配“plain”中的“a”。 |
| [^xyz]       | 负值字符集合。匹配未包含的任意字符。例如，“[^abc]”可以匹配“plain”中的“plin”。 |
| [a-z]        | 字符范围。匹配指定范围内的任意字符。例如，“[a-z]”可以匹配“a”到“z”范围内的任意小写字母字符。注意:只有连字符在字符组内部时,并且出现在两个字符之间时,才能表示字符的范围; 如果出字符组的开头,则只能表示连字符本身. |
| [^a-z]       | 负值字符范围。匹配任何不在指定范围内的任意字符。例如，“[^a-z]”可以匹配任何不在“a”到“z”范围内的任意字符。 |
| \b           | 匹配一个单词边界，也就是指单词和空格间的位置。例如，“er\b”可以匹配“never”中的“er”，但不能匹配“verb”中的“er”。 |
| \B           | 匹配非单词边界。“er\B”能匹配“verb”中的“er”，但不能匹配“never”中的“er”。 |
| \cx          | 匹配由x指明的控制字符。例如，\cM匹配一个Control-M或回车符。x的值必须为A-Z或a-z之一。否则，将c视为一个原义的“c”字符。 |
| \d           | 匹配一个数字字符。等价于[0-9]。                              |
| \D           | 匹配一个非数字字符。等价于[^0-9]。                           |
| \f           | 匹配一个换页符。等价于\x0c和\cL。                            |
| \n           | 匹配一个换行符。等价于\x0a和\cJ。                            |
| \r           | 匹配一个回车符。等价于\x0d和\cM。                            |
| \s           | 匹配任何空白字符，包括空格、制表符、换页符等等。等价于[ \f\n\r\t\v]。 |
| \S           | 匹配任何非空白字符。等价于[^ \f\n\r\t\v]。                   |
| \t           | 匹配一个制表符。等价于\x09和\cI。                            |
| \v           | 匹配一个垂直制表符。等价于\x0b和\cK。                        |
| \w           | 匹配包括下划线的任何单词字符。等价于“[A-Za-z0-9_]”。         |
| \W           | 匹配任何非单词字符。等价于“[^A-Za-z0-9_]”。                  |
| \xn          | 匹配n，其中n为十六进制转义值。十六进制转义值必须为确定的两个数字长。例如，“\x41”匹配“A”。“\x041”则等价于“\x04&1”。正则表达式中可以使用ASCII编码。 |
| \num         | 匹配num，其中num是一个正整数。对所获取的匹配的引用。例如，“(.)\1”匹配两个连续的相同字符。 |
| \n           | 标识一个八进制转义值或一个向后引用。如果\n之前至少n个获取的子表达式，则n为向后引用。否则，如果n为八进制数字（0-7），则n为一个八进制转义值。 |
| \nm          | 标识一个八进制转义值或一个向后引用。如果\nm之前至少有nm个获得子表达式，则nm为向后引用。如果\nm之前至少有n个获取，则n为一个后跟文字m的向后引用。如果前面的条件都不满足，若n和m均为八进制数字（0-7），则\nm将匹配八进制转义值nm。 |
| \nml         | 如果n为八进制数字（0-7），且m和l均为八进制数字（0-7），则匹配八进制转义值nml。 |
| \un          | 匹配n，其中n是一个用四个十六进制数字表示的Unicode字符。例如，\u00A9匹配版权符号（&copy;）。 |
| \< \>        | 匹配词（word）的开始（\<）和结束（\>）。例如正则表达式\<the\>能够匹配字符串”for the wise”中的”the”，但是不能匹配字符串”otherwise”中的”the”。注意：这个元字符不是所有的软件都支持的。 |
| \( \)        | 将 \( 和 \) 之间的表达式定义为“组”（group），并且将匹配这个表达式的字符保存到一个临时区域（一个正则表达式中最多可以保存9个），它们可以用 \1 到\9 的符号来引用。 |
| \|           | 将两个匹配条件进行逻辑“或”（Or）运算。例如正则表达式(him\|her) 匹配”it belongs to him”和”it belongs to her”，但是不能匹配”it belongs to them.”。注意：这个元字符不是所有的软件都支持的。 |
| +            | 匹配1或多个正好在它之前的那个字符。例如正则表达式9+匹配9、99、999等。注意：这个元字符不是所有的软件都支持的。 |
| ?            | 匹配0或1个正好在它之前的那个字符。注意：这个元字符不是所有的软件都支持的。 |
| {i} {i,j}    | 匹配指定数目的字符，这些字符是在它之前的表达式定义的。例如正则表达式A[0-9]{3} 能够匹配字符”A”后面跟着正好3个数字字符的串，例如A123、A348等，但是不匹配A1234。而正则表达式[0-9]{4,6} 匹配连续的任意4个、5个或者6个数字 |

 