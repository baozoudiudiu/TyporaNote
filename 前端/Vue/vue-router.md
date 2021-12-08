## vue-router

### 1. 安装

参考：[官方教程](https://next.router.vuejs.org/zh/installation.html)

### 2. router-link

代码示例：点击后跳转到某个页面

```vue
<router-link to="/about">Go to about</router-link>
```

### 3. 传递参数

#### 1. 定义参数

`router/index.js`

```javascript
import { createRouter, createWebHashHistory } from 'vue-router'
const routes = [
  {
    path: '/',
    name: 'Home',
    component: () => import('../views/Home.vue')
  }, {
    path: '/about/:id', // 给About页面定义一个动态参数id
    name: 'About',
    component: () => import('../views/About.vue')
  }
]
const router = createRouter({
  history: createWebHashHistory(),
  routes
})
export default router
```

#### 2. 传递参数

`Home.vue`

```javascript
this.$router.push("/about/123");
```

#### 3. 获取参数

`About.vue`

```javascript
console.log(this.$route.params)
```

控制台log：

```javascript
{id: 123}
```

#### 4. 有多个参数时

* 定义如下：

```javascript
{
    path: '/about/:id/name/:name', // 给About页面定义一个动态参数id
    name: 'About',
    component: () => import('../views/About.vue')
  }
```

* 上级页面传递参数

```javascript
this.$router.push('/about/123/name/diudiu')
```

* 下级页面获取参数

```javascript
console.log(this.$route.params)
```

* 控制台log如下：

```javascript
{id: '123', name: 'diudiu'}
```

#### 5.组件的复用

当同一个路由带有不同参数时，相比销毁后重新创建，复用显得更加高效。但是生命周期钩子将不会被调用，可以采用属性监听的方式来监听路由的变化。

比如从`/about/123/name/diudiu`导航到`/about/321/name/xdd`。并不会重新创建新的组件，而是直接复用之前的组件`About.vue`。

可以通过监听的方式来拿到路由的变化从而判断页面的消失和展示

```vue
watch: {
    $route(newV, oldV) {
      console.log(newV, oldV)
    }
}
```

oldV记录的是导航前的路由信息，newV记录的是导航后的路由信息。

### 4.上一页下一页

```javascript
// 向前移动一条记录，与 router.forward() 相同
router.go(1)

// 返回一条记录，与router.back() 相同
router.go(-1)

// 前进 3 条记录
router.go(3)

// 如果没有那么多记录，静默失败
router.go(-100)
router.go(100)
```



