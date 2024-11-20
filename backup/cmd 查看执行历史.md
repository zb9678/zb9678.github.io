## 运行 cmd
`C:\Users\z>`

## 进入桌面
```
C:\Users\z>cd c:\users\z\desktop
c:\Users\z\Desktop>
```

## 查看桌面文件 h.bat 的内容

- /history可以使用/h取代
```
C:\Users\z\Desktop>type h.bat
doskey /h
```

## 执行 h.bat
`C:\Users\z\Desktop>h`

相当于执行了下面
`C:\Users\z\Desktop>doskey /h`

### 显示出执行过的命令历史

```
dir
doskey /h
type 1.bat
```

## 将执行过的命令输出到 1.cmd 文件中

### 先制作 1.bat

```
@echo off
doskey /h > C:\Users\z\Desktop\1.cmd
echo %CD% | clip
// 将路径输出到剪贴板
```

### 执行 1.bat
`c:\Users\z\Desktop>s`

### 查看 1.cmd 中的输出内容
`c:\Users\z\Desktop>type 1.cmd`

```
cd c:\users\z\desktop
h
s
```
