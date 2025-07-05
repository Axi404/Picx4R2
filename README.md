## Picx4R2

A free image service based on cloudflare Pages & R2.

这是一款基于 Cloudflare 的 Worker、R2、Pages 实现的图床应用。

### 具有以下特点

* 每月 10GB 的免费存储空间。
* 每月 100 万次 (1 million requests/month) 的 A 类操作。
* 每月 1000 万次 (10 million requests/month) B 类操作。
* 不需要自己购买服务器，克隆代码后部署 CloudFlare 即可使用。
* 独立部署不需要担心被第三方删除数据。

![cf-r2-price](https://static.weiyan.tech/r2/cloudflare-r2-price.webp)

### 已实现功能

* 图片批量上传
* 图片列表查询
* 图片删除
* 目录创建
* 按目录查询
* 链接地址点击复制
* 简单的身份认证功能，进入管理页面需要授权

### 已知问题

1. 上传的图片默认按照 **`Year/Month`** 的路径保存，无法上传到指定的目录。
2. 新建目录后，在新建的目录下会默认生成一个 **未命名的对象**，目前这个对象需要登录 Cloudflare R2 才能删除。

对于已知问题，如果有小伙伴已经有解决方案，欢迎 PR 或者其他任何的方式告知一下，非常感谢。

### 部署教程

1. Fork 项目到自己的 GitHub
2. 创建 Page 项目
3. 输入编译参数

    1. 框架预设：无
    2. 构建命令：`npm run build`
    3. 输出目录：`dist`

4. 完成创建
5. 设置环境变量

    1. `AUTH_TOKEN`：授权码，这个可以自定义填写，后面页面登录需要用到；
    2. `COPY_URL`：复制的路径，如有 R2 存储桶自定义域名则填写自定义域名，否则开启并填写公共 R2.dev 存储桶的 URL；
    3. `NODE_VERSION`：`20.11.1`；
    4. `NPM_VERSION`：`10.2.4`。
    
6. 创建 KV 命名空间

    1. 在 "Workers 和 Pages" 创建 KV 命名空间。
    ![](https://static.weiyan.tech/picx/kv.webp)

7. 设置函数，KV 命名空间绑定

    1. 回到 cloudflare page，点击 "设置" → "函数" 中 "KV 命名空间绑定"。
    ![](https://static.weiyan.tech/picx/kv-name.webp)
   
8. 设置函数，绑定 R2

   变量名为：`R2`
   ![](https://static.weiyan.tech/picx/r2-storage.webp)
   
10. 重新部署

## 使用教程

1. 登录页面
   ![picx4r2-login](https://static.weiyan.tech/picx/picx4r2-login.png)

2. 登录后的界面
   ![picx4r2-main](https://static.weiyan.tech/picx/picx4r2-main.png)

3. 上传图片界面
   ![picx4r2-upload](https://static.weiyan.tech/picx/picx4r2-upload.png)

4. 图片管理界面
   ![picx4r2-manage](https://static.weiyan.tech/picx/picx4r2-manage.png)


### 感谢

本项目 fork 自 [shenweiyan/roim-picx](https://github.com/shenweiyan/Picx4R2)
