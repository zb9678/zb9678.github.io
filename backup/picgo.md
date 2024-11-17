## 首先安装
node-v20.15.0-x64.msi
================================================

## 全局安装
                   进入    C:\Users\z\AppData\Roaming\picgo
右键cmder
                     npm install picgo -g
================================================

## 安装 自动复制插件
- https://www.npmjs.com/package/picgo-plugin-autocopy
- 上传后自动将 URL 复制到剪贴板的插件
C:\Users\z\.picgo  一定要在此目录下安装
　　　　　npm i picgo-plugin-autocopy
================================================

## 将上面复制的 URL改为 html 格式
进入D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
右键　cmders Here

D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
λ                             picgo set plugin autocopy
? template:
  markdown
  HTML
  URL
  UBB
> Custom  回车

D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
λ picgo set plugin autocopy
? template: Custom
? Please place the $url to where you want. ($url)　　直接在后面粘贴<p align='center'><img src="$url" style='width:400px;'><br><br>
如下
? Please place the $url to where you want. ($url)<p align='center'><img src="$url" style='width:400px;'><br><br>
再回车
D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
λ picgo set plugin autocopy
? template: Custom
? Please place the $url to where you want. <p align='center'><img src="$url" style='width:400px;'><br><br>
[PicGo SUCCESS]: Configure config successfully!
[PicGo INFO]: If you want to use this config, please run 'picgo use plugins'

D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
λ
设置完成

上传后　剪贴板中内容将如下
<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241109175935.png" style='width:400px;'><br><br>
================================================