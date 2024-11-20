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
## 配置文件内容 1

```
<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241121000947.png" style='width:400px;'><br><br>
```

```
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
      "path": "im2/",
      "customUrl": "https://cdn.jsdelivr.net/gh/zcr07/img@main",
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
          "path": "im2/",
          "customUrl": "https://cdn.jsdelivr.net/gh/zcr07/img@main",
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

--------------------------------------------------------------------------------------------

## 配置文件内容 2

```
- 注意有２条要改
- "customUrl": "",
- "token": "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",
- 

- "customUrl": "https://img.r08.us.kg/img/main",
- "token": "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",
```

## raw.githubusercontent.com
- https://raw.githubusercontent.com/zcr07/img/main/im2/20241119213553.png

```
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

----------------------------------------------------------------------------------------

## img.r08.us.kg
- https://img.r08.us.kg/img/main/im2/20241119215535.png

```
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
      "path": "im2/",
      "customUrl": "https://img.r08.us.kg/img/main",
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
          "path": "im2/",
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

- https://github.com/zcr07/img/tree/main
- img.r08.us.kg

## 2种链接的区别

- 不稳定，但不用翻墙

- https://img.r08.us.kg/img/main/im2/20241119220301.png

- 稳定，但要翻墙

- https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:21:36:21.png


==================================================

## 上传后　剪贴板中内容将如下

`<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241109175935.png" style='width:400px;'>`

## 效果

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241109175935.png" style='width:400px;'><br><br>
================================================

## github　申请Tokey 

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117165357.png" style='width:400px;'><br><br>

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117202252.png" style='width:400px;'><br><br>


<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117165750.png" style='width:400px;'><br><br>

=================================================

## cloudflare 设置

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117173656.png" style='width:400px;'><br><br>


- https://dash.cloudflare.com/addfe9fc56c06acb158fd7b4883b478f/workers/services/edit/imgpic/production

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/main/images/20241117173446.png" style='width:400px;'><br><br>

## worker.js

```
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url)
  const path = url.pathname
  
  // 定义环境变量 GITHUB_USERNAME 和 GITHUB_PAT
   const GITHUB_USERNAME = 'zcr07' // 替换为你的 GitHub 用户名
   const GITHUB_PAT = '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' // 替换为你的 GitHub PAT，只开放 repo 权限即可
  
  // 构建 GitHub raw 内容的 URL
  const githubUrl = `https://raw.githubusercontent.com/${GITHUB_USERNAME}${path}`
  
  // 创建新的请求，添加必要的头部
  const modifiedRequest = new Request(githubUrl, {
    method: request.method,
    headers: {
      ...request.headers,
      'Authorization': `token ${GITHUB_PAT}`,
      'Accept': 'application/vnd.github.v3.raw'
    }
  })
  
  // 发送请求并返回响应
  try {
    const response = await fetch(modifiedRequest)
    
    // 如果响应不成功，抛出错误
    if (!response.ok) {
      throw new Error(`GitHub API responded with ${response.status}: ${response.statusText}`)
    }
    
    // 创建新的响应，保留原始内容但移除敏感头部
    const newResponse = new Response(response.body, response)
    newResponse.headers.delete('Authorization')
    
    return newResponse
  } catch (error) {
    return new Response(`Error: ${error.message}`, { status: 500 })
  }
}
```

=========================================================






<!--EndFragment-->
</body>
</html>