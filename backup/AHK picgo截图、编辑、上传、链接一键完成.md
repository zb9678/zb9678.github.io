## 脚本内容

```
F1 & a::
Text= ⭕       上传图片中     ⭕ 
btt(Text,600,0,,"Style4") 

    ; 启动截图程序
    Run, "D:\ahk1.0\Lib\0 tool\9金山截图王\kscrcap.exe"
    
    ; 延迟 2 秒后弹出确认对话框
    Sleep, 2000
    MsgBox, 4,, 请在完成截图和编辑后点击“是”确认上传图片。
    IfMsgBox, No
        return ; 如果选择“否”，则直接退出脚本

    ; 上传图片
	RunWait, cmd /c "picgo u",, hide
    return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & a  上传截图到github/img   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000002-2000
```

## 图示（截图效果）

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122164136.png" style='width:10px;'><br><br>

## 上传位置

- https://github.com/zcr07/img/tree/main/im2

## 配置文件 config.json 

- 注：如果失效 修改 pat = ""
- 位于 C:\Users\z\.picgo\config.json
- 注："raw.githubusercontent.com" = "cdn.jsdelivr.net/gh" 此条可删除，但得到的链接会被墙，有时显示不出。替换为https://cdn.jsdelivr.net/gh 
- 
- 具体如下图

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122171454.png" style='width:400px;'><br><br>

## config node-1.json
配置文件 config.json
- 位于 C:\Users\z\.picgo\config.json

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
        "type": "smms",
        "name": "SM.MS",
        "visible": false
      },
      {
        "type": "github",
        "name": "GitHub",
        "visible": true
      }
    ],
    "github": {
      "_configName": "node-1",
      "repo": "zcr07/node-1",
      "branch": "main",
      "token": "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",
      "path": "imgss/",
      "customUrl": "https://node.r08.us.kg",
      "_id": "dc6c8cac-b260-49d1-b260-8832960dd53d",
      "_createdAt": 1732321803260,
      "_updatedAt": 1732321803260
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
    "picgo-plugin-autocopy": true,
    "picgo-plugin-gitlab-files": true
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
          "customUrl": "https://cdn.jsdelivr.net/gh/zcr07/img@main",
          "token": "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",
          "_id": "9b921d00-95f0-47dd-9524-aea7e9ec70e4",
          "_createdAt": 1730352442411,
          "_updatedAt": 1731836528133
        },
        {
          "_configName": "node-1",
          "repo": "zcr07/node-1",
          "branch": "main",
          "token": "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",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "_id": "dc6c8cac-b260-49d1-b260-8832960dd53d",
          "_createdAt": 1732321803260,
          "_updatedAt": 1732321803260
        },
        {
          "_configName": "node-2",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "token": "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",
          "branch": "main",
          "repo": "zcr07/node-2",
          "_id": "f2e24856-c89e-4f09-9ef8-670e975cbb5d",
          "_createdAt": 1732321905575,
          "_updatedAt": 1732321905575
        },
        {
          "_configName": "node-3",
          "repo": "zcr07/node-3",
          "branch": "main",
          "token": "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",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "_id": "00642892-c82e-4b88-b522-37bb09467a17",
          "_createdAt": 1732321935850,
          "_updatedAt": 1732321935850
        }
      ],
      "defaultId": "dc6c8cac-b260-49d1-b260-8832960dd53d"
    }
  },
  "picgo-plugin-autocopy": {
    "template": "Custom",
    "customLink": "<p align='center'><img src=\"$url\" style='width:400px;'><br><br>"
  }
}
```

## 重新申请Tokens  

- 即 pat = "   " 填写内容

- https://github.com/settings/tokens

## 具体填写内容及选项

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122170036.png" style='width:400px;'><br><br>

## 复制出此 Tokens

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122170215.png" style='width:400px;'><br><br>

## config jsdelivr.json

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
        "type": "smms",
        "name": "SM.MS",
        "visible": false
      },
      {
        "type": "github",
        "name": "GitHub",
        "visible": true
      }
    ],
    "github": {
      "_configName": "img",
      "repo": "zcr07/img",
      "branch": "main",
      "path": "images/",
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
          "path": "images/",
          "customUrl": "https://cdn.jsdelivr.net/gh/zcr07/img@main",
          "token": "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",
          "_id": "9b921d00-95f0-47dd-9524-aea7e9ec70e4",
          "_createdAt": 1730352442411,
          "_updatedAt": 1731836528133
        },
        {
          "_configName": "node-1",
          "repo": "zcr07/node-1",
          "branch": "main",
          "token": "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",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "_id": "dc6c8cac-b260-49d1-b260-8832960dd53d",
          "_createdAt": 1732321803260,
          "_updatedAt": 1732321803260
        },
        {
          "_configName": "node-2",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "token": "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",
          "branch": "main",
          "repo": "zcr07/node-2",
          "_id": "f2e24856-c89e-4f09-9ef8-670e975cbb5d",
          "_createdAt": 1732321905575,
          "_updatedAt": 1732321905575
        },
        {
          "_configName": "node-3",
          "repo": "zcr07/node-3",
          "branch": "main",
          "token": "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",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "_id": "00642892-c82e-4b88-b522-37bb09467a17",
          "_createdAt": 1732321935850,
          "_updatedAt": 1732321935850
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

## config node-3.json

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
        "type": "smms",
        "name": "SM.MS",
        "visible": false
      },
      {
        "type": "github",
        "name": "GitHub",
        "visible": true
      }
    ],
    "github": {
      "_configName": "node-3",
      "repo": "zcr07/node-3",
      "branch": "main",
      "token": "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",
      "path": "imgss/",
      "customUrl": "https://node.r08.us.kg",
      "_id": "00642892-c82e-4b88-b522-37bb09467a17",
      "_createdAt": 1732321935850,
      "_updatedAt": 1732321935850
    },
    "transformer": "compress-next"
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
          "customUrl": "",
          "token": "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",
          "_id": "9b921d00-95f0-47dd-9524-aea7e9ec70e4",
          "_createdAt": 1730352442411,
          "_updatedAt": 1731836528133
        },
        {
          "_configName": "node-1",
          "repo": "zcr07/node-1",
          "branch": "main",
          "token": "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",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "_id": "dc6c8cac-b260-49d1-b260-8832960dd53d",
          "_createdAt": 1732321803260,
          "_updatedAt": 1732321803260
        },
        {
          "_configName": "node-2",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "token": "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",
          "branch": "main",
          "repo": "zcr07/node-2",
          "_id": "f2e24856-c89e-4f09-9ef8-670e975cbb5d",
          "_createdAt": 1732321905575,
          "_updatedAt": 1732321905575
        },
        {
          "_configName": "node-3",
          "repo": "zcr07/node-3",
          "branch": "main",
          "token": "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",
          "path": "imgss/",
          "customUrl": "https://node.r08.us.kg",
          "_id": "00642892-c82e-4b88-b522-37bb09467a17",
          "_createdAt": 1732321935850,
          "_updatedAt": 1732321935850
        }
      ],
      "defaultId": "00642892-c82e-4b88-b522-37bb09467a17"
    }
  },
  "picgo-plugin-autocopy": {
    "template": "Custom",
    "customLink": "<p align='center'><img src=\"$url\" style='width:400px;'><br><br>"
  }
}
```