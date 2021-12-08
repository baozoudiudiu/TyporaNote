# stylus
#### 1.定义有参数类型的样式
```stylus
flex_center()
  display: flex
  flex-direction: arguments //传递进来的参数，可以动态修改类型
  justify-content: center
  align-items: center

.flex_row_center
  flex_center: row // 传row

.flex_column_center
  flex_center: column // 传colum
```

#### 2.直接重复使用某个属性的值

```stylus
#logo
   position: absolute
   top: 50%
   left: 50%
   width: 150px
   height: 80px
   margin-left: -(@width / 2)
   margin-top: -(@height / 2)
```

#### 3.定义常量

```stylus
mainColor = red;


.class
	background-color: mainColor
  
font-size = 14px
font-stack = "Lucida Grande", Arial, sans-serif

body
  font font-size font-stack
```

