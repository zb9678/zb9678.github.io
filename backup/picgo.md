## 首先安装 Node.js
- Node.js 是一个免费、开源、跨平台的 JavaScript 运行时环境，它让开发人员能够创建服务器、Web 应用、命令行工具和脚本。
- https://nodejs.org/zh-cn/
- node-v22.11.0-x64.msi

================================================

## 全局安装 picgo
- https://picgo.github.io/PicGo-Core-Doc/zh/guide/getting-started.html#%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85
- 进入    C:\Users\z\AppData\Roaming\picgo
- 右键cmder
- - **npm install picgo -g**

<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241117122231.png" style='width:400px;'><br><br>

================================================

## 安装插件 autocopy
- 上传后自动将 URL 复制到剪贴板的插件
- https://www.npmjs.com/package/picgo-plugin-autocopy
- C:\Users\z\\.picgo  一定要在此目录下安装
- - **npm i picgo-plugin-autocopy**

================================================

## 将上面复制的 URL改为 html  (自定)格式
- D:\ahk1.0\Lib\0 tool\picgo-croe\picgo   config备份
- 右键cmder

---------------------------------------------------

λ        **picgo set plugin autocopy**
? template:
  markdown
  HTML
  URL
  UBB
> Custom  回车
----------------------------------------------------

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

至此，全部设置完成
================================================

## 上传后　剪贴板中内容将如下
`<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241109175935.png" style='width:400px;'>`

## 效果
<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241109175935.png" style='width:400px;'><br><br>
================================================