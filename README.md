# web项目一键部署( akey-deploy-web )

## 设计初衷
现有成熟的自动化部署方案大多为 `jenkins + gitlab/github` 但是需要我们配置很多繁琐的东西,而对于大多数前端开发者而言这些并不擅长 <br>
再者,杀鸡焉用宰牛刀,如果我们只是想实现前端的自动化部署,不管后端的死活那我们更不必用jenkins <bg> 
那,能否有个轻量级的前端一键部署方案呢? <br>

__今天,他来了__  哈哈

## 使用 

下载
```js
 npm/cnpm i akey-deploy-web
```
在根目录上新建配置文件 `deploy.config.js`(必须叫这个名称)
```js
module.exports = Object.freeze({
  development: {
    //测试
    SERVER_PATH: '', // ssh地址 服务器地址
    SSH_USER: '', // ssh 用户名
    //方式一 用秘钥登录服务器(推荐), private 本机私钥文件地址(需要在服务器用户目录 一般是 /root/.ssh/authorized_keys 配置公钥 并该文件权限为 600, (.ssh文件夹一般默认隐藏)
    // PRIVATE_KEY: 'C:/Users/Html5/.ssh/id_rsa',
    PASSWORD: '', //方式二 用密码连接服务器
    PATH: '' // 需要上传的服务器目录地址 如 /usr/local/nginx/html
  },
  production: {
    //正式
    SERVER_PATH: '',
    SSH_USER: 'root',
    PRIVATE_KEY: '',
    PATH: '/test/html'
  }
})

```
在package.js文件中新加命令
```js
  "scripts": {
    ...
    "d": "node node_modules/akey-deploy-web"
  },
```
运行 `npm run d` 即可实现一键部署

## 注意

+ 部署对象服务器使用ssh链接
+ 输入npm run d后会询问你填写git备注,填写则会自动把代码提交到当前git仓库,如不填写则不会提交到git

[git 地址](https://github.com/lyh0371/akey-deploy-web) 求star