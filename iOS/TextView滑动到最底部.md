UITextView使用代码滑动到最底部 (swift代码为例,OC同理)

```
self.textView.layoutManager.allowsNonContiguousLayout = false;
self.textView.scrollRangeToVisible(NSRange.init(location: str.count , length: 1))
```

