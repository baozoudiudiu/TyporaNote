代码示例:

```js
<wxs module="tmp">
  function imgSrc(imgPath, faceUrl) {
    return faceUrl || imgPath
  }
  module.exports = {
    imgSrc: imgSrc
  }
</wxs>
```

