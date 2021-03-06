Pinclub
=======

[![node version][node-image]][node-url]
[![build status](http://git.jinwanzhilian.com/liubing/nodeclub/badges/master/build.svg)](http://git.jinwanzhilian.com/liubing/nodeclub/commits/master)
[![coverage report](http://git.jinwanzhilian.com/liubing/nodeclub/badges/master/coverage.svg)](http://jiuyanlou.com/public/testcov/index.html)
[![Code Climate](https://codeclimate.com/github/pinclub/pinclub.svg)](https://codeclimate.com/github/pinclub/pinclub)
[![Gitter](https://badges.gitter.im/pinclub/pinclub.svg)](https://gitter.im/pinclub/Lobby)

[node-image]: https://img.shields.io/badge/node.js-%3E=_4.2-green.svg?style=flat-square
[node-url]: http://nodejs.org/download/

## 介绍 / Intro

Pinclub 是基于 Nodeclub 进行的二次开发. 增加了瀑布流展示方式, 主要参考花瓣网的设计风格(感谢花瓣网的设计师和前端工程师的辛勤工作), 加入了hanming距离的算法, 当然是在mongodb中使用了 function 的形式实现.

Pinclub's base code is forked from [Nodeclub](https://github.com/cnodejs/nodeclub) project. Pinclub add waterfall layout using Masonry plugin. The style of Frontend is mainly refer to [Huaban.com](http://huaban.com), thanks.
For support simulate search function simply add an mongodb function to achieve the [Hamming Distance algorithm](https://zh.wikipedia.org/wiki/%E6%B1%89%E6%98%8E%E8%B7%9D%E7%A6%BB).

## 状态 / Status

Pinclub 目前处于开发阶段，尚未发布 Stable 版本.

Pinclub is at developing statge, not stable enough.

## 图片相似度算法说明 / About HammingDistance

在 Topic 模型中加入了 image 的相关属性值, 其中就包括 image_hash, 使用 imghash 模块生成了 16 bits 的二进制字符串.

在 Mongodb 中创建了一个 function 命名为 hammingDistance, 代码如下:

At the Topic modal, we add a property named image_hash, to save the image hash of pictures, and we build a function in Mongodb, blow is the code segment of it:

```
function (a, b) {
    if (typeof(a) === "undefined" || typeof(b) === "undefined") return 64;
    var aa = a.split("");
    var bb = b.split("");
    var count = 0;
    for (var i = 0; i < aa.length; i++) if (aa[i] !== bb[i]) count++;
        return count;
}
```

通过 mongo 命令行创建 Function

创建脚本：
```
db.system.js.save(
   {
     _id: "hammingDistance",
     value : function (a, b) {
                 if (typeof(a) === "undefined" || typeof(b) === "undefined") return 64;
                 var aa = a.split("");
                 var bb = b.split("");
                 var count = 0;
                 for (var i = 0; i < aa.length; i++) if (aa[i] !== bb[i]) count++;
                     return count;
             }
   }
)
```

## Chrome 插件获取外部图片 / Chrome plugin to Get picture

如果目标网站做了引用保护，则无法完成图片的 Get 操作

[插件下载地址 / Download Chrome plugin](http://www.jiuyanlou.com/public/chromeplugin/pinclub_chrome_plugin_jiuyanlou.crx)

[插件应用商店地址 / Download Chrome plugin from web store](https://chrome.google.com/webstore/detail/pinclub-quick-add/adeaflopkflkeldipfolpccbkpmboebd)

[插件项目地址 / Plugin Project](https://github.com/pinclub/pinclub_chrome_plugin)

## TODO / How to Contribute

如果你想贡献一份力量, 请查看 [TODO](https://github.com/pinclub/pinclub/blob/master/TODO.md) 列表

## 安装部署

*不保证 Windows 系统的兼容性*

线上跑的是 [Node.js](https://nodejs.org) v4.4.0，[MongoDB](https://www.mongodb.org) 是 v3.0.5，[Redis](http://redis.io) 是 v3.0.3。

```
1. 安装 `Node.js[必须]` `MongoDB[必须]` `Redis[必须]`
2. 启动 MongoDB 和 Redis
3. `$ make install` 安装 Nodeclub 的依赖包
4. `cp config.default.js config.js` 请根据需要修改配置文件
5. `$ make test` 确保各项服务都正常
6. `$ node app.js`
7. visit `http://localhost:3000`
8. done!
```

## API接口文档

使用 npm run apidoc 命令在本地生成文档后, 访问: http://localhost:3000/public/apidoc

## 截图

![首页](https://s-media-cache-ak0.pinimg.com/originals/00/b2/ed/00b2ed90e8af4721d5acab894cef33e7.jpg)
![上传图片](https://s-media-cache-ak0.pinimg.com/originals/10/c5/e1/10c5e11cbe032138b26827b1a58e21cf.jpg)
![设置board](https://s-media-cache-ak0.pinimg.com/originals/5a/4e/d8/5a4ed82f3fe250c2051c3c463db8e397.jpg)
![图片box](https://s-media-cache-ak0.pinimg.com/originals/61/dd/c0/61ddc022328245d89cf24aba204b95a2.jpg)
![Get图片](https://s-media-cache-ak0.pinimg.com/originals/15/d0/18/15d018bcbe7fe02e2c541f648c6a1e16.jpg)
![Dashboard](https://s-media-cache-ak0.pinimg.com/564x/06/15/3c/06153c8e3c5544f4a089c848de0f692b.jpg)
![用户列表](https://s-media-cache-ak0.pinimg.com/564x/26/0d/61/260d61613e2598e424611338978ec39b.jpg)
![板块列表](https://s-media-cache-ak0.pinimg.com/564x/a0/3b/87/a03b87d957222511918cbf344ce55250.jpg)
![板块弹出模态框](https://s-media-cache-ak0.pinimg.com/564x/9f/be/c3/9fbec3406cdf86cfb1ad4f5658cc4593.jpg)

## 关于 Nodeclub

Nodeclub 是使用 **Node.js** 和 **MongoDB** 开发的社区系统，界面优雅，功能丰富，小巧迅速，
已在Node.js 中文技术社区 [CNode(http://cnodejs.org)](http://cnodejs.org) 得到应用，但你完全可以用它搭建自己的社区。

## 测试(完善中)

跑测试

```bash
$ make test
```

跑覆盖率测试

```bash
$ make test-cov
```

## 贡献

Pinclub 可以联系 [@hhdem](https://github.com/hhdem)

Nodeclub 有任何意见或建议都欢迎提 issue，或者直接提给 [@alsotang](https://github.com/alsotang)

## License

Pinclub is released under the MIT License. Have at it.
