##  无须输入密码登录windows

- 分为2种情况

- 1. 安装windows时，密码为空，那么 `AutoAdminLogon`  值为` 0 `即可自动登录不用输密码。

此时注册表中只有一个  DefaultUserName，登录用户名。

- 2. 安装windows时，密码不为空，那么 `AutoAdminLogon`  值为` 1 `即自动登录不用输密码。

此时注册表中会有一个DefaultPassword，即登录密码。 DefaultUserName，登录用户名。


<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.15:18:26:24.png" style="width:400px;"></p><br>