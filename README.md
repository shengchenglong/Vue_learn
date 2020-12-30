# Vue_learn
The learning journey of Vue

# 国密SM2

>npm install --save sm-crypto

```javascript
const sm2 = require('sm-crypto').sm2
const cipherMode = 1  // 1 - C1C3C2，0 - C1C2C3，默认为1
let pwd= sm2.doEncrypt(this.password, "公钥", cipherMode) // sm2加密
```

*sm2的加解密时有两种方式即0——C1C2C3、1——C1C3C2，如果选用的了C1C2C3的加密方式时是在加密后的密文前面需要加04的*



