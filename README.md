# Vue_learn
The learning journey of Vue



# 定义一个方法并给别处调用

1. 编写一个js：auth.js

   ```javascript
   export function getToken() {
     ...
   }
     
   export function setToken(token) {
     ...
   }
   ```

2. 引入 auth.js

   ```javascript
   import { getToken, setToken } from '@/utils/auth'
   
   ... // 开始调用
   ```

# 国密SM2

>npm install --save sm-crypto

```javascript
const sm2 = require('sm-crypto').sm2
const cipherMode = 1  // 1 - C1C3C2，0 - C1C2C3，默认为1
let pwd= sm2.doEncrypt(this.password, "公钥", cipherMode) // sm2加密
```

*sm2的加解密时有两种方式即0——C1C2C3、1——C1C3C2，如果选用的了C1C2C3的加密方式时是在加密后的密文前面需要加04的*

*还需要安装md5*

```javascript
npm install --save md5
```

# 时间格式化

*摘自别处：做同样事情的两个软件在大小上可能差异很大。Moment.js 是最流行的日期操作库，每周有超过 1200 万下载量，但它代码简化做得并不好，会向你的项目增加 300KB 大小。Day.js 拥有几乎相同的 API，但只有 2KB。事实上，Moment.js 现在推荐使用 Day.js 和其它日期库作为替代。*

[官方介绍](https://momentjs.com/docs/#/-project-status/)

```javascript
npm install --save dayjs
```

# 截取路由的部分路径当作请求参数

[官方文档](https://router.vuejs.org/zh/guide/)

1. 路由路径中使用“动态路径参数”(dynamic segment) 

   /aaa/:siteCode/bbb

2. 设置一个上下文存放

   ```javascript
   const context = {
     siteCode: ''
   }
   
   export default context
   ```

3. VueRouter.beforeEach

   ```javascript
   import context from '@/..../context'
   
   router.beforeEach((to, from, next) => {
     const siteCode = to.params.siteCode
     context.siteCode = siteCode
   }
   ```

4. 使用axios

   ```javascript
   import context from '@/..../context'
   
   // 创建axios实例
   const service = axios.create({
     ... // 其他代码
     params: {}
   })
   
   // request拦截器
   service.interceptors.request.use(
     config => {
      	... // 其他代码
       config.params.companyCode = context.companyCode
       config.params.siteCode = context.siteCode
       return config
     },
     error => {
       Promise.reject(error)
     }
   )
   ```

   # Vuex.Store

   *感觉有一点点像像是一个JavaBaseClass的感觉____2020-12-31*

   [概念](https://vuex.vuejs.org/zh/)

   