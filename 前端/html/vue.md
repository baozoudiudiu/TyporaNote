### 计算型属性

#### 单纯的只读属性

```javascript
<template>
        <view>
            <view>Original message: "{{ message }}"</view>
            <view>Computed reversed message: "{{ reversedMessage }}"</view>
        </view>
    </template>
    <script>
        export default {
            data() {
                return {
                    message: 'Hello'
                }
            },
            computed: {
                // 计算属性的 getter
                reversedMessage(){
                  return this.message.split('').reverse().join('')
                }
            }
        }
    </script>
```

#### setter getter 

```javascript
<template>
        <view>
            <view>{{ fullName }}</view>
        </view>
    </template>
    <script>
        export default {
            data() {
                return {
                    firstName: 'Foo',
                    lastName: 'Bar'
                }
            },
            computed: {
                fullName: {
                    // getter
                    get(){
                        return this.firstName + ' ' + this.lastName
                    },
                    // setter
                    set(newValue){
                        var names = newValue.split(' ')
                        this.firstName = names[0]
                        this.lastName = names[names.length - 1]
                    }
                }
            }
        }
    </script>
```

