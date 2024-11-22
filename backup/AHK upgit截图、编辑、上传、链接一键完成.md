## 脚本部分

```
F1 & s::
    ; 显示上传中提示
    Text := "⭕ 上传图片中 ⭕"
    btt(Text, 600, 0, , "Style4")

    ; 启动截图程序
    Run, "D:\ahk1.0\Lib\0 tool\9金山截图王\kscrcap.exe"
    
    ; 延迟 2 秒后弹出确认对话框
    Sleep, 2000
    MsgBox, 4,, 请在完成截图和编辑后点击“是”确认上传图片。
    IfMsgBox, No
        return ; 如果选择“否”，则直接退出脚本
    
    ; 上传图片
    Run, D:\ahk1.0\Lib\0 tool\picgo-croe\upgit.exe :clipboard -o clipboard -f ccc, , hide
    return

;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & s  上传截图到github/img   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000001-1984
```

## 图示

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/cdn/B11.22:16:33:13.png" style="width:400px;"></p>

## 配置文件 config.json
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