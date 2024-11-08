
## rem 和 ::注释命令
注释行不执行操作

## pause暂停命令
运行该命令时，将显示下面的消息：请按任意键继续 . . .
一般用于看清楚屏幕上显示的内容

## copy
copy 1.txt + 2.txt 3.txt     #合并 1.txt 和 2.txt 的内容，保存为 3.txt 文件如果不指定 3.txt ，则保存到 1.txt
copy 1.txt +                 #复制文件到自己，实际上是修改了文件日期

## prn
代表打印机

## copy拷贝文件
copy c:\test.txt d:\                  #复制 c:\test.txt 文件到 d:\
copy c:\test.txt d:\test.bak     #复制 c:\test.txt 文件到 d:\ ，并重命名为 test.bak
copy c:\*.*                              #复制 c:\ 所有文件到当前目录，不包括隐藏文件和系统文件，不指定目标路径，则默认目标路径为当前目录.
copy con test.txt                   #从屏幕上等待输入，按 Ctrl+Z 结束输入，输入内容存为test.txt文件con代表屏幕。

## cls
清屏

## type显示文件内容
type c:\boot.ini    #显示指定文件的内容，程序文件一般会显示乱码
type *.txt             #显示当前目录里所有.txt文件的内容

## ren文件重命名
ren 1.txt 2.bat         #把 1.txt 更名为 2.bat
ren *.txt *.ini            #把当前目录里所有.txt文件改成.ini文件
ren d:\temp tmp     #对文件夹的重命名

## del删除文件
del d:\test.txt                   #删除指定文件，不能是隐藏、系统、只读文件
del *.*                              #删除当前目录里的文件(不包括隐藏、系统、只读文件)，要求按 Y 确认
del /q/a/f d:\temp\*.*     #删除 所有文件(不包括子目录)
del /q/a/f/s d:\temp\*.*  #删除 所有文件(包括子目录)

## echo 和 @回显控制命令
@                       #关闭单行回显
echo off             #从下一行开始关闭回显
@echo off         #从本行开始关闭回显。一般批处理第一行都是这个
echo on            #从下一行开始打开回显
echo                 #显示当前是 echo off 状态还是 echo on 状态
echo.                #输出空行
echo hello        #输出  hello
"关闭回显"是指运行批处理文件时，不显示文件里的每条命令，只显示运行结果批处理开始和结束时，系统都会自动打开

## dir
显示目录中的文件和子目录列表
dir                 #显示当前目录中的文件和子目录
dir /a              #显示当前目录中的文件和子目录，包括隐藏文件和系统文件
dir c: /a:d         #显示 C 盘当前目录中的目录
dir c:\ /a:-d       #显示 C 盘根目录中的文件
dir d:\mp3 /b/p     #逐屏显示 d:\mp3 目录里的文件
dir .               #显示当前目录中的文件和子目录
dir ..              #显示上级目录中的文件和子目录

## cd
更改当前目录
cd abc              #进入当前目录中的 abc 目录
cd ..                  #进入当前目录中的上级目录
cd\                   #进入根目录
cd                    #显示当前目录
cd /d d:\abc    #可以同时更改盘符和目录
cd "Documents and Settings"\All users文件名带空格，路径前需要加上引号

## md创建目录
md abc              #在当前目录里建立子目录 abc
md d:\a\b\c         #如果 d:\a 不存在，将会自动创建

## rd删除目录
rd abc              #删除当前目录里的 abc 子目录，要求为空目录
rd /s/q d:\temp     #删除 d:\temp 文件夹及其子文件夹和文件，不需要按 Y 确认

color 2f 
颜色值 设置cmd控制台 字体颜色　和　背景颜色;
A=淡绿、B=淡浅绿、C=淡红、D=淡紫、E=淡黄、F=亮白
0=黑、1=蓝、2=绿、3=浅绿、4=红、5=紫、6=黄、7=白、8=灰、9=淡蓝

## title  
cmd窗口顶部标题名字

## ver 
在cmd窗口下显示  版本信息

## goto
标签将cmd.exe导向到批处理程序中带标签的行(标签必须单独一行，且以冒号打头，例如:“:start”标签)

## call
路径批处理文件名从批处理程序中调用另一个批处理程序

## start
程序名或命令/max 或/min 新开一个新窗口并最大化 (最小化) 运行某程序或命令

====================================================

17 date 和 time日期和时间
date          #显示当前日期，并提示输入新日期，按"回车"略过输入
date/t        #只显示当前日期，不提示输入新日期
time          #显示当前时间，并提示输入新时间，按"回车"略过输入
time/t        #只显示当前时间，不提示输入新时间

18 goto 和 :跳转命令
:label        #行首为:表示该行是标签行，标签行不执行操作
goto label    #跳转到指定的标签那一行

19 find (外部命令)查找命令
find "abc" c:\test.txt在 c:\test.txt 文件里查找含 abc 字符串的行如果找不到，将设 errorlevel 返

回码为1
find /i "abc" c:\test.txt查找含 abc 的行，忽略大小写
find /c "abc" c:\test.txt显示含 abc 的行的行数

20 more (外部命令)逐屏显示
more c:\test.txt    #逐屏显示 c:\test.txt 的文件内容

21 tree显示目录结构
tree d:\            #显示D盘的文件目录结构

22 &顺序执行多条命令，而不管命令是否执行成功
c: & cd\ & dir /w相当于把下面3行命令写到1行去了c:cd\dir /w

23 &&顺序执行多条命令，当碰到执行出错的命令后将不执行后面的命令
f: && cd\ && dir >c:\test.txt注意如果f盘不存在，那么后面2条命令将不会执行
find "ok" c:\test.txt && echo 成功如果找到了"ok"字样，就显示"成功"，找不到就不显示

24 ||顺序执行多条命令，当碰到执行正确的命令后将不执行后面的命令

find "ok" c:\test.txt || echo 不成功如果找不到"ok"字样，就显示"不成功"，找到了就不显示

25 |管道命令
前一个命令的执行结果输出到后一个命令
dir *.* /s/a | find /c ".exe"管道命令表示先执行 dir 命令，对其输出的结果执行后面的 find 命令该

命令行结果：

输出当前文件夹及所有子文件夹里的.exe文件的个数
type c:\test.txt|more这个和 more c:\test.txt 的效果是一样的

26 > 和 >>输出重定向命令
> 清除文件中原有的内容后再写入>> 追加内容到文件末尾，而不会清除原有的内容主要将本来显示在屏幕

上的内容输出

到指定文件中指定文件如果不存在，则自动生成该文件
echo hello world>c:\test.txt生成c:\test.txt文件，内容为hello world这个格式在批处理文件里用得很

多，可以生成 

.reg .bat .vbs 等临时文件
type c:\test.txt >prn屏幕上不显示文件内容，转向输出到打印机
echo hello world>con在屏幕上显示hello world，实际上所有输出都是默认 >con 的
copy c:\test.txt f: >nul拷贝文件，并且不显示"文件复制成功"的提示信息，但如果f盘不存在，还是会

显示出错信息
copy c:\test.txt f: >nul 2>nul不显示"文件复制成功"的提示信息，并且f盘不存在的话，也不显示错误

提示信息
echo ^^W ^> ^W>c:\test.txt生成的文件内容为 ^W > W^ 和 > 是控制命令，要把它们输出到文件，必须在

前面加个 ^ 

符号
27 <从文件中获得输入信息，而不是从屏幕上
一般用于 date time label 等需要等待输入的命令
[@echo](http://my.oschina.net/yuning0502) offecho 2005-05-01>temp.txtdate <temp.txtdel temp.txt这样就可以不等待输入直接修改当前日

期

28.
%0 %1 %2 %3 %4 %5 %6 %7 %8 %9 %*命令行传递给批处理的参数
%0 批处理文件本身%1 第一个参数%9 第九个参数%* 从第一个参数开始的所有参数在C盘根目录新建

test.bat，内容如下：
[@echo](http://my.oschina.net/yuning0502) off
echo %0
echo %1
echo %2
echo %*
复制代码
运行cmd，输入 c:\test.bat "/a" /b /c /d可以看出每个参数的含意
修改test.bat内容如下
[@echo](http://my.oschina.net/yuning0502) off
echo %1
echo %~1
echo %0
echo %~f0
echo %~d0
echo %~p0
echo %~n0
echo %~x0
echo %~s0
echo %~a0
echo %~t0
echo %~z0
复制代码
再运行cmd，输入 c:\test.bat "/a" /b /c /d可以参照 call/? 或 for/? 看出每个参数的含意注意这里可

以对文件进行日期比较和大小比较
echo load "%%1" "%%2">c:\test.txt
复制代码
生成的文件内容为 load "%1" "%2"
批处理文件里，用这个格式把命令行参数输出到文件

31 set设置变量
引用变量可在变量名前后加 % ，即 %变量名%
set                    #显示目前所有可用的变量，包括系统变量和自定义的变量
echo %SystemDrive%     #显示系统盘盘符。系统变量可以直接引用
set p                  #显示所有以p开头的变量，要是一个也没有就设errorlevel=1
set p=aa1bb1aa2bb2     #设置变量p，并赋值为 = 后面的字符串，即aa1bb1aa2bb2
echo %p%               #显示变量p代表的字符串，即aa1bb1aa2bb2
echo %p:~6%            #显示变量p中第6个字符以后的所有字符，即aa2bb2
echo %p:~6,3%          #显示第6个字符以后的3个字符，即aa2
echo %p:~0,3%          #显示前3个字符，即aa1
echo %p:~-2%           #显示最后面的2个字符，即b2
echo %p:~0,-2%         #显示除了最后2个字符以外的其它字符，即aa1bb1aa2b
echo %p:aa=c%          #用c替换变量p中所有的aa，即显示c1bb1c2bb2
echo %p:aa=%           #将变量p中的所有aa字符串置换为空，即显示1bb12bb2
echo %p:*bb=c%         #第一个bb及其之前的所有字符被替换为c，即显示c1aa2bb2
set p=%p:*bb=c%        #设置变量p，赋值为 %p:*bb=c% ，即c1aa2bb2
set /a p=39            #设置p为数值型变量，值为39
set /a p=39/10         #支持运算符，有小数时用去尾法，39/10=3.9，去尾得3，p=3set /a p=p/10     

     #用 /a 

参数时，在 = 后面的变量可以不加%直接引用set /a p="1&0"         #"与"运算，要加引号。其它支持的

运算符参见

set/?
set p=                 #取消p变量
set /p p=请输入屏幕上显示"请输入"，并会将输入的字符串赋值给变量p注意这条可以用来取代 choice 命

令
注意变量在 if 和 for 的复合语句里是一次性全部替换的，如
[@echo](http://my.oschina.net/yuning0502) off
set p=aaa
if %p%==aaa (    
  echo %p%   
  set p=bbb    
  echo %p%    )
结果将显示aaaaaa因为在读取 if 语句时已经将所有 %p% 替换为aaa这里的"替换"，在 /? 帮助里就是指"

扩充"、"环境

变量扩充"可以启用"延缓环境变量扩充"，用 ! 来引用变量，即 !变量名!
[@echo](http://my.oschina.net/yuning0502) off
SETLOCAL ENABLEDELAYEDEXPANSION
set p=aaaif %p%==aaa (  
  echo %p%    
set p=bbb    
echo !p!    )
ENDLOCAL
结果将显示aaabbb
还有几个动态变量，运行 set 看不到
%CD%                  #代表当前目录的字符串
%DATE%                #当前日期
%TIME%                #当前时间
%RANDOM%              #随机整数，介于0~32767
%ERRORLEVEL%          #当前ERRORLEVEL 值
%CMDEXTVERSION%       #当前命令处理器扩展名版本号
%CMDCMDLINE%          #调用命令处理器的原始命令行可以用echo命令查看每个变量值，如 echo %time%

注意 %time% 

精确到毫秒，在批处理需要延时处理时可以用到

32 start批处理中调用外部程序的命令，否则等外部程序完成后才继续执行剩下的指令
start explorer d:\调用图形界面打开D盘
[@echo](http://my.oschina.net/yuning0502) offcd /d %~dp0regedit /s 劲舞团.regstart patcher.exe
不加 start 命令的话，"劲舞团"运行时，后面会有个黑乎乎的cmd窗口

33 call批处理中调用另外一个批处理的命令，否则剩下的批处理指令将不会被执行有时有的应用程序用

start调用出错的

，也可以call调用

34 choice (外部命令)选择命令让用户输入一个字符，从而选择运行不同的命令，返回码errorlevel为1234

……win98里

是choice.comwin2000pro里没有，可以从win98里拷过来win2003里是choice.exechoice /N /C y /T 5 /D 

y>nul延时5秒

下面是个 choice 语句的例子
[@echo](http://my.oschina.net/yuning0502) off
rem 以下在win2000pro运行通过，从win98里拷的chioce.com文件
choice /c:abc aaa,bbb,ccc
if errorlevel 3 goto ccc
if %errorlevel%==2 goto bbb
if errorlevel==1 goto aaa
rem 必须先判断数值高的返回码rem 可以看到 errorlevel 值的判断有3种写法，有时某种写法不好用，可

以用另外的写法
rem 直接运行

chioce相当于运行
choice /c:yn:aaa
echo aaa
goto end
:bbb
echo bbb
goto end
:ccc
echo ccc
goto end
:end

35 assoc 和 ftype文件关联assoc 设置'文件扩展名'关联，关联到'文件类型'ftype 设置'文件类型'关联

，关联到'执行程序和参数'当你双击一个.txt文件时，windows并不是根据.txt直接判断用 notepad.exe 打

开而是先判断.txt属于 txtfile '文件类型'再调用 txtfile 关联的命令行 txtfile=%SystemRoot%

\system32\NOTEPAD.EXE %1可以在"文件夹选项"→"文件类型"里修改这2种关联
assoc           #显示所有'文件扩展名'关联
assoc .txt      #显示.txt代表的'文件类型'，结果显示 .txt=txtfile
assoc .doc      #显示.doc代表的'文件类型'，结果显示 .doc=Word.Document.8
assoc .exe      #显示.exe代表的'文件类型'，结果显示 .exe=exefile
ftype           #显示所有'文件类型'关联
ftype exefile   #显示exefile类型关联的命令行，结果显示 exefile="%1" %* assoc 

.txt=Word.Document.8设置.txt为word类型的文档，可以看到.txt文件的图标都变了
assoc .txt=txtfile恢复.txt的正确关联 ftype exefile="%1" %*恢复 exefile 的正确关联

如果该关联已经被破坏，可以运行 command.com ，再输入这条命令

36 pushd 和 popd切换当前目录
[@echo](http://my.oschina.net/yuning0502) off
c: & cd\ & md mp3       #在 C:\ 建立 mp3 文件夹
md d:\mp4               #在 D:\ 建立 mp4 文件夹
cd /d d:\mp4            #更改当前目录为 d:\mp4
pushd c:\mp3            #保存当前目录，并切换当前目录为 c:\mp3
popd                    #恢复当前目录为刚才保存的 d:\mp4一般用处不大，在当前目录名不确定时，会

有点帮助

32 subst (外部命令)映射磁盘。
subst z: \\server\d     #这样输入z:就可以访问\\server\d了
subst z: /d             #取消该映射
subst                   #显示目前所有的映

38  xcopy (外部命令)文件拷贝
xcopy d:\mp3 e:\mp3 /s/e/i/y复制 d:\mp3 文件夹、所有子文件夹和文件到 e:\ ，覆盖已有文件加 /i 

表示如果 e:\ 没有 mp3 文件夹就自动新建一个，否则会有询问

39 一些不常用的内部命令
>& 将一个句柄的输出写入到另一个句柄的输入中
<& 从一个句柄读取输入并将其写入到另一个句柄输出中shift 命令行传递给批处理的参数不止9个时，用以

切换参数color 设置cmd窗口的显示颜色
pormpt 更改命令提示符号，默认都是 盘符:\路径\> ，如 c:\>

40 format (外部命令)格式化硬盘
format c: /q/u/autotest/q表示快速格式化，/autotest表示自动格式化，不需要按 Y 确认/u表示每字节

用 

F6 覆盖硬盘数据，使其不可用软件恢复format c: /c格式化C盘，并检测坏道

41 fdisk (外部命令)硬盘分区win2000不带

该命令win98里的fdisk不支持80G以上大硬盘，winme里的支持fdisk/mbr重建硬盘分区表，一般用于清除引

导区病毒、还

原精灵注意使用该命令不能从硬盘启动，必须软驱或光驱启动后直接运行

42 ping (外部命令)
ping -l 65500 -t 192.168.1.200不停的向192.168.1.200计算机发送大小为65500byte的数据包
ping -n 10 127.0.0.1>nulping自己10次，可用于批处理延时10秒

43 SC (外部命令)服务控制命令
sc create aaa displayname= bbb start= auto binpath= "C:\WINDOWS\System32\alg.exe"创建服务，服

务名称aaa，显示名称bbb，启动类型:自动可执行文件的路径"C:\WINDOWS\System32\alg.exe"
sc description aaa "ccc"更改aaa的描述为ccc
sc config aaa start= disabled binpath= "C:\WINDOWS\System32\svchost.exe -k netsvcs"更改aaa的启

动类型:已禁用更改aaa的可执行文件的路径"C:\WINDOWS\System32\svchost.exe -k netsvcs"
sc config aaa start= demand displayname= ddd更改aaa的启动类型:手动更改aaa的显示名称ddd
sc start aaa启动aaa服务
sc stop aaa停止aaa服务
sc delete aaa删除aaa服务