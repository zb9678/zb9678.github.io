## 首先安装 Node.js

```
- Node.js 是一个免费、开源、跨平台的 JavaScript 运行时环境，它让开发人员能够创建服务器、Web 应用、命令行工具和脚本。
- https://nodejs.org/zh-cn/
- node-v22.11.0-x64.msi
```

================================================

## 全局安装 picgo

```
- https://picgo.github.io/PicGo-Core-Doc/zh/guide/getting-started.html#%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85
- 进入    C:\Users\z\AppData\Roaming\picgo
- 右键cmder
- - **npm install picgo -g**

<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241117122231.png" style='width:400px;'><br><br>
```

================================================

## 安装插件 autocopy

```
- 上传后自动将 URL 复制到剪贴板的插件
- https://www.npmjs.com/package/picgo-plugin-autocopy
- C:\Users\z\\.picgo  一定要在此目录下安装
- - **npm i picgo-plugin-autocopy**
```

================================================

## 将上面复制的 URL改为 html  (自定)格式

```
- C:\Users\z\\.picgo
- D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份(不用此地址了)
- 右键cmder
```

---------------------------------------------------

```
λ        **picgo set plugin autocopy**
? template:
  markdown
  HTML
  URL
  UBB
> Custom  回车
```
----------------------------------------------------

```
λ         **picgo set plugin autocopy**
? template: Custom
? Please place the $url to where you want. ($url)　　直接在后面粘贴
`<p align='center'><img src="$url" style='width:400px;'><br><br>`
如下
? Please place the $url to where you want. ($url)`<p align='center'><img src="$url" style='width:400px;'><br><br>`

再回车

D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
λ **picgo set plugin autocopy**
? template: Custom
? Please place the $url to where you want. `<p align='center'><img src="$url" style='width:400px;'><br><br>`
[PicGo SUCCESS]: Configure config successfully!
[PicGo INFO]: If you want to use this config, please run 'picgo use plugins'
D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
λ
```

至此，全部设置完成
================================================

## 配置文件

```
- C:\Users\z\.picgo\config.json

<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241117122421.png" style='width:400px;'><br><br>
```

================================================

## 配置文件内容

```
- 注意有２条要改
- "customUrl": "",
- "token": "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",

- "customUrl": "https://img.r08.us.kg/img/main",
- "token": "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",

{
  "picBed": {
    "current": "github",
    "uploader": "github",
    "smms": {
      "token": ""
    },
    "list": [
      {
        "type": "tcyun",
        "name": "腾讯云COS",
        "visible": false
      },
      {
        "type": "aliyun",
        "name": "阿里云OSS",
        "visible": false
      },
      {
        "type": "smms",
        "name": "SM.MS",
        "visible": false
      },
      {
        "type": "github",
        "name": "GitHub",
        "visible": true
      },
      {
        "type": "qiniu",
        "name": "七牛云",
        "visible": false
      },
      {
        "type": "imgur",
        "name": "Imgur",
        "visible": false
      },
      {
        "type": "upyun",
        "name": "又拍云",
        "visible": false
      }
    ],
    "github": {
      "_configName": "img",
      "repo": "zcr07/img",
      "branch": "main",
      "path": "images/",
      "customUrl": "",
      "token": "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",
      "_id": "9b921d00-95f0-47dd-9524-aea7e9ec70e4",
      "_createdAt": 1730352442411,
      "_updatedAt": 1731836528133
    }
  },
  "settings": {
    "shortKey": {
      "picgo:upload": {
        "enable": true,
        "key": "CommandOrControl+Shift+P",
        "name": "upload",
        "label": "QUICK_UPLOAD"
      }
    },
    "showUpdateTip": false,
    "autoStart": false,
    "autoRename": true,
    "encodeOutputURL": false,
    "privacyEnsure": true,
    "pasteStyle": "URL"
  },
  "needReload": false,
  "picgoPlugins": {
    "picgo-plugin-compress-next": true,
    "picgo-plugin-autocopy": true
  },
  "picgo-plugin-compress-next": {
    "Compress Type": "tinypng",
    "Gif compress Type": "webp-converter",
    "Auto Refresh TinyPng Key Across Months": true,
    "TinyPng API Key": "scHQZ2CmlQDdRJnMQ9SjXKVfByCwY3YD"
  },
  "uploader": {
    "github": {
      "configList": [
        {
          "_configName": "Default",
          "_id": "d4b75295-a443-4075-ad2e-73caf72e078c",
          "_createdAt": 1730352070049,
          "_updatedAt": 1730352070049
        },
        {
          "_configName": "img",
          "repo": "zcr07/img",
          "branch": "main",
          "path": "images/",
          "customUrl": "https://img.r08.us.kg/img/main",
          "token": "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",
          "_id": "9b921d00-95f0-47dd-9524-aea7e9ec70e4",
          "_createdAt": 1730352442411,
          "_updatedAt": 1731836528133
        }
      ],
      "defaultId": "9b921d00-95f0-47dd-9524-aea7e9ec70e4"
    }
  },
  "picgo-plugin-autocopy": {
    "template": "Custom",
    "customLink": "<p align='center'><img src=\"$url\" style='width:400px;'><br><br>"
  }
}
```

================================================

## 上传后　剪贴板中内容将如下
`<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241109175935.png" style='width:400px;'>`

## 效果
<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241109175935.png" style='width:400px;'><br><br>
================================================

## github　申请Tokey 日期最多只能为一年

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117165357.png" style='width:400px;'><br><br>

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117202252.png" style='width:400px;'><br><br>


<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117165750.png" style='width:400px;'><br><br>

=================================================

## cloudflare 设置
注意：如果已将 upgit 的Token输入了，就不要再改动了。

<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241117173656.png" style='width:400px;'><br><br>


- https://dash.cloudflare.com/addfe9fc56c06acb158fd7b4883b478f/workers/services/edit/imgpic/production

<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241117173446.png" style='width:400px;'><br><br>
