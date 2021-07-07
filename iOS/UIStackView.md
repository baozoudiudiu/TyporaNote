## 前言

接触过前端布局后，再回头来看iOS的autolayout布局有些一言难尽。apple现在推出了swiftUI，但出于最低使用版本是iOS13的局限性，一时半会swiftUI还使用不起来。不过之前苹果在iOS9之后推出了类似前端flex布局的控件UIStackView。在项目中某些场景，这玩意还是挺好用的。

## 1、demo示例

<img src="Jietu20210630-155514-HD.gif" alt="示例" style="zoom:75%; float:left" />

demo地址见文末

## 2、创建

先创建，后设置子视图

```swift
let stackView = UIStackView()
stackView.addArrangedSubview(UIView())
```

创建时设置子视图

```swift
let stackView = UIStackView(arrangedSubviews: [UIView(), UIView()])
```

## 3、布局方式（Axis）

### 3.1、横向布局（x轴，自左向右）

```swift
stackView.axis = .horizontal
```

<img src="/Users/chenwang/Desktop/chenwang/TyporaNote/iOS/截屏2021-06-30 下午4.15.51.png" alt="截屏2021-06-30 下午4.15.51" style="zoom:80%; float:left" />

### 3.2、纵向布局（y轴，自上而下）

```swift
stackView.axis = .vertical
```

<img src="/Users/chenwang/Desktop/chenwang/TyporaNote/iOS/截屏2021-06-30 下午4.16.44.png" alt="截屏2021-06-30 下午4.16.44" style="zoom:80%;float:left" />

布局的方向我们称之为：**主轴**，与主轴垂直的方向我们称之为：**副轴**。

* 横向布局时，x轴为主轴，y轴为副轴
* 纵向布局时，y轴为主轴，x轴为副轴。

## 4、主轴布局方式（Distribution）

UIStackView的`distribution`枚举属性用来控制主轴的布局方式

| 枚举值                      | 作用 | 补充 |
| --------------------------- | ---- | ---- |
| case fill = 0               | 默认样式，充满stackView | |
| case fillEqually = 1        | 按子视图等宽或等高方式，充满stackView | 横向布局则等宽，纵向布局则等高 |
| case fillProportionally = 2 | 按子视图按比例分布方式，充满stackView | |
| case equalSpacing = 3       | 按子视图之间间距相等方式，充满stackView | |
| case equalCentering = 4     | 按子视图中心点间距相等方式，充满stackView | |

相同的枚举值，在stackView尺寸（横向布局时指宽度，纵向布局时指高度）`固定`和`动态`两种情况下效果可能会有所不同，这里分开讨论。

### 4.1、动态尺寸

#### 4.1.1、横向布局

创建stackView时不限制宽度，并添加三个子视图，宽度分别为30、60、30.

这里只贴上核心代码，布局代码就不贴了。

```swift
let view1 = createItem(title: "11111111", bgColor: .red, width: 30, prio: 900)
let view2 = createItem(title: "2222222222222222222", bgColor: .orange, width: 60, prio: 900)
let view3 = createItem(title: "3333333333333333333333", bgColor: .yellow, width: 30, prio: 900)

self.stackView.addArrangedSubview(view1)
self.stackView.addArrangedSubview(view2)
self.stackView.addArrangedSubview(view3)
```


