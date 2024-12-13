## 当打开KeePass时自动填写密码并打开

```
#Persistent
#SingleInstance Force
SetTimer, passwd, 500

passwd:
if WinExist("打开数据库 - 9_34_31.kdbx")
{
    WinActivate ; 激活窗口
    Sleep, 100 ; 等待100毫秒以确保窗口激活
EnvGet, password, KeePassPassword
SendInput, %password%{Enter}
}
return

```