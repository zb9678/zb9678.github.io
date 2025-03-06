## singbox设置 导入订阅

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:14:54.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:16:26.png" style="width:400px;"></p><br>

## 普通节点转为singbox订阅

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:17:56.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:19:31.png" style="width:400px;"></p><br>

## 根据vless节点配置 singbox **订阅**

```
vless://803f17dc-afc3-44d2-b02b-a1fdfd938882@kj.zbb25.filegear-sg.me:443?encryption=none&security=tls&sni=kj.zbb25.filegear-sg.me&fp=randomized&type=ws&host=kj.zbb25.filegear-sg.me&path=%2F%3Fed%3D2048#kj.zbb25.filegear-sg.me

vless://1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1@[2606:4700::5e12:b05b]:443?encryption=none&security=tls&sni=ff.v07.us.kg&fp=random&type=ws&host=ff.v07.us.kg&path=%2F%3Fed%3D2560#3%60
--------------------------------------------------------------
[
  {
    "type": "vless",
    "tag": "01",
    "server": "kj.zbb25.filegear-sg.me",
    "server_port": 443,
    "uuid": "803f17dc-afc3-44d2-b02b-a1fdfd938882",
    "transport": {
      "path": "/?ed=2560",
      "type": "ws",
      "headers": {
        "Host": "kj.zbb25.filegear-sg.me"
      }
    },
    "tls": {
      "enabled": true,
      "server_name": "kj.zbb25.filegear-sg.me",
      "insecure": true
    },
    "tcp_fast_open": false
  },
 {
    "type": "vless",
    "tag": "02",
    "server": "2606:4700::5e12:b05b",
    "server_port": 443,
    "uuid": "1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1",
    "transport": {
      "path": "/?ed=2560",
      "type": "ws",
      "headers": {
        "Host": "ff.v07.us.kg"
      }
    },
    "tls": {
      "enabled": true,
      "server_name": "ff.v07.us.kg",
      "insecure": true
    },
    "tcp_fast_open": false
  },{
    "type": "vless",
    "tag": "03",
    "server": "2606:4700::0ED1:627E",
    "server_port": 443,
    "uuid": "457c8796-830f-4cbf-a54a-c8abea1e5991",
    "transport": {
      "path": "/?ed=2560",
      "type": "ws",
      "headers": {
        "Host": "ff.zbb25.filegear-sg.me"
      }
    },
    "tls": {
      "enabled": true,
      "server_name": "ff.zbb25.filegear-sg.me",
      "insecure": true
    },
    "tcp_fast_open": false
  }
]
```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:28:38.png" style="width:400px;"></p><br>

## 配置

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:30:09.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:31:45.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:33:00.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:33:54.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:34:36.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:36:32.png" style="width:400px;"></p><br>

##

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:52:39.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:53:45.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:54:24.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:55:14.png" style="width:400px;"></p><br>
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.06:11:51:18.png" style="width:400px;"></p><br>


