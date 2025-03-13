## ReNamer.exe的使用方法1

彻底重命名 如下

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:28:20.png" style="width:400px;"></p><br>

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:32:06.png" style="width:400px;"></p><br>

## Excel 批量文件名  

注意01前的 `01

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:33:15.png" style="width:400px;"></p><br>

## 方法2

- 先解决编号前的补位 0

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:38:15.png" style="width:400px;"></p><br>

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:39:08.png" style="width:400px;"></p><br>

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:39:36.png" style="width:400px;"></p><br>

- 再解决第3列编号前的补位 0 

- 公式   =A1&B1

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:40:51.png" style="width:400px;"></p><br>

- 公式    =TEXT(A1,"00")&B1

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:42:12.png" style="width:400px;"></p><br>

- 公式    =CONCATENATE(TEXT(A1,"00"),B1)

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:44:10.png" style="width:400px;"></p><br>

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.13:11:46:21.png" style="width:400px;"></p><br>
