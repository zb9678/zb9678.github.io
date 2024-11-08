## winget upgrade
查看需要更新的软件

## winget upgrade 软件ID
开始更新

一定是复制软件ID
1.使用Winget安装、升级、卸载软件的常用命令
winget list    | 查看已安装的软件 |
winget search 7zip     |  搜索软件  |
winget install 7zip.zip   |  安装软件  |
winget upgrade 7zip.zip   |  升级软件  |
winget upgrade all    |  升级所有软件  |
winget uninstall 软件ID   |  卸载软件  |

2.使用Winget安装软件时自定义安装路径
格式为：winget install 软件ID --location "自定义路径"
例子：winget install 7zip.7zip --location "D:\Program Files\7zip"


![winget upgrade](https://github.com/user-attachments/assets/52a96e40-3341-4565-b193-e0e190cba5dc)
