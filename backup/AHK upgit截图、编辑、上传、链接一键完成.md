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