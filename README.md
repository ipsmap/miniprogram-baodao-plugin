# 小程序插件报到功能接入文档

### 在小程序后台添加插件

登录自己的小程序管理后台: [https://mp.weixin.qq.com](https://mp.weixin.qq.com)  ， 小程序开发者可在`小程序管理后台-设置-第三方服务-插件管理`中，根据AppID查找需要的插件，并申请使用。插件开发者在24小时内通过后，小程序开发者可在小程序内使用该插件。

### 接入使用插件

微信小程序官方插件使用文档参考：[https://developers.weixin.qq.com/miniprogram/dev/framework/plugin/using.html](https://developers.weixin.qq.com/miniprogram/dev/framework/plugin/using.html)

#### 引入插件代码包

对于插件的使用者，使用插件前要在`app.json`中声明需要使用的插件，例如：

```js
{
  "plugins": {
    "ipsPlugin": {
      "version": "1.0.0",
      "provider": "wxxxxxxxxxxxxxxxxx"
    }
  }
}
```

如上例所示， `plugins` 定义段中可以包含多个插件声明，每个插件声明中都必须指明插件的 appid 和需要使用的版本号。

#### 使用插件的 js 接口

如果需要使用插件的 js 接口，可以使用 `requirePlugin` 方法：

```js
var ipsPlugin = requirePlugin("ipsPlugin")

//appKey和mapID 需要向我方获取
//设置appkey和mapid    建议写在onLoad中
ipsPlugin.init({ ipsAppKey: 'fnAs1mE5HP', ipsMapId: 'VhsehJzuZA'});

//设置导航目的id  写在需要修改导航目的地Id的地方
ipsPlugin.init({ ipsTargetId: '1111'});

//报到成功回调   建议写在onLoad中
ipsPlugin.init({ipsReportSuccess:() => {
    //when success to do...
    console.log('报到 成功')
}});

//打开弹框，开启报到  写在需要报道的地方
ipsPlugin.open();
```

#### 使用插件的自定义组件

使用插件提供的自定义组件，和使用普通自定义组件的方式相仿。在 `json` 文件定义需要引入的自定义组件时，使用 `plugin://`

协议即可，例如：

```js
{
  "usingComponents": {
    "show": "plugin://ipsPlugin/show"
  }
}
```

在 `wxml` 文件中添加如下代码

```js
<show />
```

现在你就可以愉快地使用插件进行报道功能了哦

### 注意事项

* 不能通过关键字搜索，只能使用ID

* 搜索出来没有这个插件的介绍和如何使用，只有头像和名称

* 需要插件开发者在24小时内通过才能使用



