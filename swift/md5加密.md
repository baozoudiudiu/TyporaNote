## swift md5加密

```swift
    func md5(_ send: String) -> String {
        let str = send.cString(using: .utf8)
        let strLen = CUnsignedInt(send.lengthOfBytes(using: .utf8))
        let digestLen = Int(CC_MD5_DIGEST_LENGTH)
        let result = UnsafeMutablePointer<CUnsignedChar>.allocate(capacity: digestLen)
        CC_MD5(str, strLen, result)
        var hash: String = ""
        for i in 0..<digestLen {
            hash.append(String.init(format: "%02x",result[i]))
        }
        result.deallocate()
        return hash
    }
```

