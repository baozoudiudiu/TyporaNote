## 1前端:

```vue
<template>
	<!-- <img alt="Vue logo" src="./assets/logo.png"> -->
	<!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
	<button @click="buttonClick">点击发送消息</button>
	<button @click="buttonClick2">\关闭</button>
</template>

<script>
	import HelloWorld from './components/HelloWorld.vue'
	export default {
		name: 'App',
		components: {
			// HelloWorld
		},
		mounted: function() {
			var ws = new WebSocket("ws://192.168.3.97:8088");
			ws.onopen = function() {
				console.log('已连接上！');
			}
			ws.onmessage = function(e) {
				console.log(e.data);
			}
			ws.onclose = function() {
				console.log('连接已关闭！');
			}
			this.ws = ws
		},
		methods: {
			buttonClick: function() {
				this.ws.send('111111')
			},
			buttonClick2: function() {
				this.ws.send('close')
				this.ws.close()
			}
		}
	}
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>

```

## 服务端:

```javascript
import ws from './node_modules/nodejs-websocket/index.js'
let server = undefined
function main() {
	console.log("开始建立连接...");
	server = ws.createServer(function(connect) {
    	connect.on("text",function(msg){
        	console.log("收到的消息是：" + msg); 
        	if (msg) {
        		if (msg == 'close') {
        			console.log(server)
        			server.close()
        			return
        		}
           		connect.send('服务端已收到消息：' + msg + '服务端发来消息： Hello,' + msg);
        	}  
    	});  
	})
	server.listen(8088)
}

main()
setTimeout(()=>{
	console.log('延时触发')
	server.close()
}, 10000)
```

