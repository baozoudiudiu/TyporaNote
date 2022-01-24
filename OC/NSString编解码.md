```objective-c
  NSString *str = @"我是测试字符串";

  NSLog(@"编码前: %@", str);

  

  // iOS 9.0一下

  NSString *str1 = [str stringByAddingPercentEscapesUsingEncoding:NSUnicodeStringEncoding];

  NSLog(@"9.0之前编码后: %@", str1);

  NSLog(@"解码: %@", [str1 stringByReplacingPercentEscapesUsingEncoding:NSUnicodeStringEncoding]);

  // iOS 9.0以上

  NSCharacterSet *charset = [[NSCharacterSet characterSetWithCharactersInString:@"!*'();:@&=+$,/?%#[]"]invertedSet];

  NSString *str2 = [str stringByAddingPercentEncodingWithAllowedCharacters:charset];

  NSLog(@"9.0之后编码后: %@", str2);

  NSLog(@"解码: %@", [str2 stringByRemovingPercentEncoding]);


```

