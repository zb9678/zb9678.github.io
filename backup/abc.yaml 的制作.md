##  高级替换脚本

```
F1 & w::
    originalText := "  - {name: 01, server: 104.21.236.177, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: ""/?ed=2560"", headers: {Host: ff.v07.us.kg}}}"

    ipList := []  ; 初始化数组
    index := 1

    Loop, Read, 4.txt
    {
        ipList[index] := A_LoopReadLine  ; 逐行读取并存入数组
        index++
    }

    newText := ""  ; 存储最终文本

    ; 依次替换 IP 和 Name
    for index, ip in ipList
    {
        tempText := StrReplace(originalText, "104.21.236.177", ip)  ; 替换 IP
        tempText := StrReplace(tempText, "name: 01", "name: " Format("{:02}", index))  ; 替换 name: 01 为 01, 02, 03...
        newText .= tempText . "`n"
    }

    ; 写入剪贴板
    Clipboard := RTrim(newText, "`n")
    ; MsgBox, 生成完成，已复制到剪贴板！
return

```

## 替换 name: 01 为 name: 02 03 04.....

```
  - {name: 01, server: 104.21.236.177, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: ""/?ed=2560"", headers: {Host: ff.v07.us.kg}}}
```

## 用同目录下的4.txt中的内容替换 104.21.236.177

```
  - {name: 01, server: 104.21.236.177, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: ""/?ed=2560"", headers: {Host: ff.v07.us.kg}}}
```

## 最终效果

```
  - {name: 01, server: 2A06:98C1:3122::CACE, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 02, server: 2A06:98C1:3122::E419, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 03, server: 2A06:98C1:3122::9BE1, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 04, server: 2A06:98C1:3122::5A3C, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 05, server: 104.18.185.155, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 06, server: 104.16.243.88, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 07, server: 104.16.233.61, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 08, server: 104.18.28.153, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 09, server: 104.18.79.66, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 10, server: 1.aqdlt2023.com, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 11, server: 2.aqdlt2023.com, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
  - {name: 12, server: 3.aqdlt2023.com, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
```

## 4.txt内容如下

```
2A06:98C1:3122::CACE
2A06:98C1:3122::E419
2A06:98C1:3122::9BE1
2A06:98C1:3122::5A3C
104.18.185.155
104.16.243.88
104.16.233.61
104.18.28.153
104.18.79.66
1.aqdlt2023.com
2.aqdlt2023.com
3.aqdlt2023.com
```

===============================================================

## 将模板  abc.yaml中的此段内容替换为  上面 最终效果

```
  - {"type":"vmess","name":"233boy-grpc-t03-cf.phpman.top","grpc-opts":{"grpc-service-name":"537d21ad-49af-41ad-8089-db557b63a40e"},"server":"t03-cf.phpman.top","port":"443","uuid":"537d21ad-49af-41ad-8089-db557b63a40e","alterId":"0","cipher":"auto","network":"grpc","tls":true}
```

##  查找abc.yaml中的      - zzzaaaaaaaaaaazzzzzzzzzzaaaazzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz

```
      - zzzaaaaaaaaaaazzzzzzzzzzaaaazzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
```

替换为如下

```
      - 01
      - 02
      - 03
      - 04
      - 05
      - 06
      - 07
      - 08
      - 09
      - 10
      - 11
      - 12
```

## 模板   abc.yaml

```

port: 7890
socks-port: 7891
allow-lan: true
mode: Rule
log-level: info
external-controller: 0.0.0.0:9090
proxies:
  - {name: 01, server: 2A06:98C1:3122::CACE, port: 443, type: vless, uuid: 1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1, tls: true, tfo: false, skip-cert-verify: true, servername: ff.v07.us.kg, client-fingerprint: random, network: ws, ws-opts: {path: "/?ed=2560", headers: {Host: ff.v07.us.kg}}}
proxy-groups:
  - name: 🚀 节点选择
    type: select
    proxies:
      - ♻️ 自动选择
      - DIRECT
      - zzzaaaaaaaaaaazzzzzzzzzzaaaazzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
  - name: ♻️ 自动选择
    type: url-test
    url: http://www.gstatic.com/generate_204
    interval: 300
    tolerance: 50
    proxies:
      - zzzaaaaaaaaaaazzzzzzzzzzaaaazzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
  - name: 🐟 漏网之鱼
    type: select
    proxies:
      - 🚀 节点选择
      - ♻️ 自动选择
      - zzzaaaaaaaaaaazzzzzzzzzzaaaazzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
rules:
  - DOMAIN-SUFFIX,1password.com,🚀 节点选择
  - DOMAIN-SUFFIX,v2rayse.com,🚀 节点选择
  - DOMAIN-SUFFIX,vpnse.org,🚀 节点选择
  - DOMAIN-SUFFIX,adguard.org,🚀 节点选择
  - DOMAIN-SUFFIX,bit.no.com,🚀 节点选择
  - DOMAIN-SUFFIX,btlibrary.me,🚀 节点选择
  - DOMAIN-SUFFIX,cccat.io,🚀 节点选择
  - DOMAIN-SUFFIX,cloudcone.com,🚀 节点选择
  - DOMAIN-SUFFIX,dubox.com,🚀 节点选择
  - DOMAIN-SUFFIX,gameloft.com,🚀 节点选择
  - DOMAIN-SUFFIX,garena.com,🚀 节点选择
  - DOMAIN-SUFFIX,hoyolab.com,🚀 节点选择
  - DOMAIN-SUFFIX,inoreader.com,🚀 节点选择
  - DOMAIN-SUFFIX,ip138.com,🚀 节点选择
  - DOMAIN-SUFFIX,myteamspeak.com,🚀 节点选择
  - DOMAIN-SUFFIX,notion.so,🚀 节点选择
  - DOMAIN-SUFFIX,ping.pe,🚀 节点选择
  - DOMAIN-SUFFIX,reddit.com,🚀 节点选择
  - DOMAIN-SUFFIX,teddysun.com,🚀 节点选择
  - DOMAIN-SUFFIX,tumbex.com,🚀 节点选择
  - DOMAIN-SUFFIX,twdvd.com,🚀 节点选择
  - DOMAIN-SUFFIX,unsplash.com,🚀 节点选择
  - DOMAIN-SUFFIX,xn--i2ru8q2qg.com,🚀 节点选择
  - DOMAIN-SUFFIX,yunpanjingling.com,🚀 节点选择
  - DOMAIN-SUFFIX,eu,🚀 节点选择
  - DOMAIN-SUFFIX,hk,🚀 节点选择
  - DOMAIN-SUFFIX,jp,🚀 节点选择
  - DOMAIN-SUFFIX,kr,🚀 节点选择
  - DOMAIN-SUFFIX,sg,🚀 节点选择
  - DOMAIN-SUFFIX,tw,🚀 节点选择
  - DOMAIN-SUFFIX,uk,🚀 节点选择
  - DOMAIN-SUFFIX,us,🚀 节点选择
  - DOMAIN-KEYWORD,1e100,🚀 节点选择
  - DOMAIN-KEYWORD,abema,🚀 节点选择
  - DOMAIN-KEYWORD,appledaily,🚀 节点选择
  - DOMAIN-KEYWORD,avtb,🚀 节点选择
  - DOMAIN-KEYWORD,beetalk,🚀 节点选择
  - DOMAIN-KEYWORD,blogspot,🚀 节点选择
  - DOMAIN-KEYWORD,dropbox,🚀 节点选择
  - DOMAIN-KEYWORD,facebook,🚀 节点选择
  - DOMAIN-KEYWORD,fbcdn,🚀 节点选择
  - DOMAIN-KEYWORD,github,🚀 节点选择
  - DOMAIN-KEYWORD,gmail,🚀 节点选择
  - DOMAIN-KEYWORD,google,🚀 节点选择
  - DOMAIN-KEYWORD,instagram,🚀 节点选择
  - DOMAIN-KEYWORD,porn,🚀 节点选择
  - DOMAIN-KEYWORD,sci-hub,🚀 节点选择
  - DOMAIN-KEYWORD,spotify,🚀 节点选择
  - DOMAIN-KEYWORD,telegram,🚀 节点选择
  - DOMAIN-KEYWORD,twitter,🚀 节点选择
  - DOMAIN-KEYWORD,whatsapp,🚀 节点选择
  - DOMAIN-KEYWORD,youtube,🚀 节点选择
  - DOMAIN-SUFFIX,4sqi.net,🚀 节点选择
  - DOMAIN-SUFFIX,a248.e.akamai.net,🚀 节点选择
  - DOMAIN-SUFFIX,adobedtm.com,🚀 节点选择
  - DOMAIN-SUFFIX,ampproject.org,🚀 节点选择
  - DOMAIN-SUFFIX,android.com,🚀 节点选择
  - DOMAIN-SUFFIX,aolcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,apkmirror.com,🚀 节点选择
  - DOMAIN-SUFFIX,apkpure.com,🚀 节点选择
  - DOMAIN-SUFFIX,app-measurement.com,🚀 节点选择
  - DOMAIN-SUFFIX,appspot.com,🚀 节点选择
  - DOMAIN-SUFFIX,archive.org,🚀 节点选择
  - DOMAIN-SUFFIX,armorgames.com,🚀 节点选择
  - DOMAIN-SUFFIX,aspnetcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,awsstatic.com,🚀 节点选择
  - DOMAIN-SUFFIX,azureedge.net,🚀 节点选择
  - DOMAIN-SUFFIX,azurewebsites.net,🚀 节点选择
  - DOMAIN-SUFFIX,bandwagonhost.com,🚀 节点选择
  - DOMAIN-SUFFIX,bing.com,🚀 节点选择
  - DOMAIN-SUFFIX,bkrtx.com,🚀 节点选择
  - DOMAIN-SUFFIX,blogcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,blogger.com,🚀 节点选择
  - DOMAIN-SUFFIX,blogsmithmedia.com,🚀 节点选择
  - DOMAIN-SUFFIX,blogspot.com,🚀 节点选择
  - DOMAIN-SUFFIX,blogspot.hk,🚀 节点选择
  - DOMAIN-SUFFIX,blogspot.jp,🚀 节点选择
  - DOMAIN-SUFFIX,bloomberg.cn,🚀 节点选择
  - DOMAIN-SUFFIX,bloomberg.com,🚀 节点选择
  - DOMAIN-SUFFIX,box.com,🚀 节点选择
  - DOMAIN-SUFFIX,cachefly.net,🚀 节点选择
  - DOMAIN-SUFFIX,cdnst.net,🚀 节点选择
  - DOMAIN-SUFFIX,cloudfront.net,🚀 节点选择
  - DOMAIN-SUFFIX,comodoca.com,🚀 节点选择
  - DOMAIN-SUFFIX,daum.net,🚀 节点选择
  - DOMAIN-SUFFIX,demdex.net,🚀 节点选择
  - DOMAIN-SUFFIX,deskconnect.com,🚀 节点选择
  - DOMAIN-SUFFIX,disqus.com,🚀 节点选择
  - DOMAIN-SUFFIX,disquscdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,dropbox.com,🚀 节点选择
  - DOMAIN-SUFFIX,dropboxapi.com,🚀 节点选择
  - DOMAIN-SUFFIX,dropboxstatic.com,🚀 节点选择
  - DOMAIN-SUFFIX,dropboxusercontent.com,🚀 节点选择
  - DOMAIN-SUFFIX,duckduckgo.com,🚀 节点选择
  - DOMAIN-SUFFIX,edgecastcdn.net,🚀 节点选择
  - DOMAIN-SUFFIX,edgekey.net,🚀 节点选择
  - DOMAIN-SUFFIX,edgesuite.net,🚀 节点选择
  - DOMAIN-SUFFIX,eurekavpt.com,🚀 节点选择
  - DOMAIN-SUFFIX,fastmail.com,🚀 节点选择
  - DOMAIN-SUFFIX,firebaseio.com,🚀 节点选择
  - DOMAIN-SUFFIX,flickr.com,🚀 节点选择
  - DOMAIN-SUFFIX,flipboard.com,🚀 节点选择
  - DOMAIN-SUFFIX,gfx.ms,🚀 节点选择
  - DOMAIN-SUFFIX,gongm.in,🚀 节点选择
  - DOMAIN-SUFFIX,hulu.com,🚀 节点选择
  - DOMAIN-SUFFIX,id.heroku.com,🚀 节点选择
  - DOMAIN-SUFFIX,io.io,🚀 节点选择
  - DOMAIN-SUFFIX,issuu.com,🚀 节点选择
  - DOMAIN-SUFFIX,ixquick.com,🚀 节点选择
  - DOMAIN-SUFFIX,jtvnw.net,🚀 节点选择
  - DOMAIN-SUFFIX,kat.cr,🚀 节点选择
  - DOMAIN-SUFFIX,kik.com,🚀 节点选择
  - DOMAIN-SUFFIX,kobo.com,🚀 节点选择
  - DOMAIN-SUFFIX,kobobooks.com,🚀 节点选择
  - DOMAIN-SUFFIX,licdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,live.net,🚀 节点选择
  - DOMAIN-SUFFIX,livefilestore.com,🚀 节点选择
  - DOMAIN-SUFFIX,llnwd.net,🚀 节点选择
  - DOMAIN-SUFFIX,macrumors.com,🚀 节点选择
  - DOMAIN-SUFFIX,medium.com,🚀 节点选择
  - DOMAIN-SUFFIX,mega.nz,🚀 节点选择
  - DOMAIN-SUFFIX,megaupload.com,🚀 节点选择
  - DOMAIN-SUFFIX,messenger.com,🚀 节点选择
  - DOMAIN-SUFFIX,netdna-cdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,nintendo.net,🚀 节点选择
  - DOMAIN-SUFFIX,nsstatic.net,🚀 节点选择
  - DOMAIN-SUFFIX,nytstyle.com,🚀 节点选择
  - DOMAIN-SUFFIX,overcast.fm,🚀 节点选择
  - DOMAIN-SUFFIX,openvpn.net,🚀 节点选择
  - DOMAIN-SUFFIX,periscope.tv,🚀 节点选择
  - DOMAIN-SUFFIX,pinimg.com,🚀 节点选择
  - DOMAIN-SUFFIX,pinterest.com,🚀 节点选择
  - DOMAIN-SUFFIX,potato.im,🚀 节点选择
  - DOMAIN-SUFFIX,prfct.co,🚀 节点选择
  - DOMAIN-SUFFIX,pscp.tv,🚀 节点选择
  - DOMAIN-SUFFIX,quora.com,🚀 节点选择
  - DOMAIN-SUFFIX,resilio.com,🚀 节点选择
  - DOMAIN-SUFFIX,sfx.ms,🚀 节点选择
  - DOMAIN-SUFFIX,shadowsocks.org,🚀 节点选择
  - DOMAIN-SUFFIX,slack-edge.com,🚀 节点选择
  - DOMAIN-SUFFIX,smartdnsproxy.com,🚀 节点选择
  - DOMAIN-SUFFIX,sndcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,soundcloud.com,🚀 节点选择
  - DOMAIN-SUFFIX,startpage.com,🚀 节点选择
  - DOMAIN-SUFFIX,staticflickr.com,🚀 节点选择
  - DOMAIN-SUFFIX,symauth.com,🚀 节点选择
  - DOMAIN-SUFFIX,symcb.com,🚀 节点选择
  - DOMAIN-SUFFIX,symcd.com,🚀 节点选择
  - DOMAIN-SUFFIX,textnow.com,🚀 节点选择
  - DOMAIN-SUFFIX,textnow.me,🚀 节点选择
  - DOMAIN-SUFFIX,thefacebook.com,🚀 节点选择
  - DOMAIN-SUFFIX,thepiratebay.org,🚀 节点选择
  - DOMAIN-SUFFIX,torproject.org,🚀 节点选择
  - DOMAIN-SUFFIX,trustasiassl.com,🚀 节点选择
  - DOMAIN-SUFFIX,tumblr.co,🚀 节点选择
  - DOMAIN-SUFFIX,tumblr.com,🚀 节点选择
  - DOMAIN-SUFFIX,tvb.com,🚀 节点选择
  - DOMAIN-SUFFIX,txmblr.com,🚀 节点选择
  - DOMAIN-SUFFIX,v2ex.com,🚀 节点选择
  - DOMAIN-SUFFIX,vimeo.com,🚀 节点选择
  - DOMAIN-SUFFIX,vine.co,🚀 节点选择
  - DOMAIN-SUFFIX,vox-cdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,amazon.co.jp,🚀 节点选择
  - DOMAIN-SUFFIX,amazon.com,🚀 节点选择
  - DOMAIN-SUFFIX,amazonaws.com,🚀 节点选择
  - IP-CIDR,13.32.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,13.35.0.0/17,🚀 节点选择,no-resolve
  - IP-CIDR,18.184.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,18.194.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,18.208.0.0/13,🚀 节点选择,no-resolve
  - IP-CIDR,18.232.0.0/14,🚀 节点选择,no-resolve
  - IP-CIDR,52.58.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,52.74.0.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,52.77.0.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,52.84.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,52.200.0.0/13,🚀 节点选择,no-resolve
  - IP-CIDR,54.93.0.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,54.156.0.0/14,🚀 节点选择,no-resolve
  - IP-CIDR,54.226.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,54.230.156.0/22,🚀 节点选择,no-resolve
  - DOMAIN-KEYWORD,uk-live,🚀 节点选择
  - DOMAIN-SUFFIX,bbc.co,🚀 节点选择
  - DOMAIN-SUFFIX,bbc.com,🚀 节点选择
  - DOMAIN-SUFFIX,apache.org,🚀 节点选择
  - DOMAIN-SUFFIX,docker.com,🚀 节点选择
  - DOMAIN-SUFFIX,elastic.co,🚀 节点选择
  - DOMAIN-SUFFIX,elastic.com,🚀 节点选择
  - DOMAIN-SUFFIX,gcr.io,🚀 节点选择
  - DOMAIN-SUFFIX,gitlab.com,🚀 节点选择
  - DOMAIN-SUFFIX,gitlab.io,🚀 节点选择
  - DOMAIN-SUFFIX,jitpack.io,🚀 节点选择
  - DOMAIN-SUFFIX,maven.org,🚀 节点选择
  - DOMAIN-SUFFIX,medium.com,🚀 节点选择
  - DOMAIN-SUFFIX,mvnrepository.com,🚀 节点选择
  - DOMAIN-SUFFIX,quay.io,🚀 节点选择
  - DOMAIN-SUFFIX,reddit.com,🚀 节点选择
  - DOMAIN-SUFFIX,redhat.com,🚀 节点选择
  - DOMAIN-SUFFIX,sonatype.org,🚀 节点选择
  - DOMAIN-SUFFIX,sourcegraph.com,🚀 节点选择
  - DOMAIN-SUFFIX,spring.io,🚀 节点选择
  - DOMAIN-SUFFIX,spring.net,🚀 节点选择
  - DOMAIN-SUFFIX,stackoverflow.com,🚀 节点选择
  - DOMAIN-SUFFIX,discord.co,🚀 节点选择
  - DOMAIN-SUFFIX,discord.com,🚀 节点选择
  - DOMAIN-SUFFIX,discord.gg,🚀 节点选择
  - DOMAIN-SUFFIX,discord.media,🚀 节点选择
  - DOMAIN-SUFFIX,discordapp.com,🚀 节点选择
  - DOMAIN-SUFFIX,discordapp.net,🚀 节点选择
  - DOMAIN-SUFFIX,facebook.com,🚀 节点选择
  - DOMAIN-SUFFIX,fb.com,🚀 节点选择
  - DOMAIN-SUFFIX,fb.me,🚀 节点选择
  - DOMAIN-SUFFIX,fbcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,fbcdn.net,🚀 节点选择
  - IP-CIDR,31.13.24.0/21,🚀 节点选择,no-resolve
  - IP-CIDR,31.13.64.0/18,🚀 节点选择,no-resolve
  - IP-CIDR,45.64.40.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,66.220.144.0/20,🚀 节点选择,no-resolve
  - IP-CIDR,69.63.176.0/20,🚀 节点选择,no-resolve
  - IP-CIDR,69.171.224.0/19,🚀 节点选择,no-resolve
  - IP-CIDR,74.119.76.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,103.4.96.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,129.134.0.0/17,🚀 节点选择,no-resolve
  - IP-CIDR,157.240.0.0/17,🚀 节点选择,no-resolve
  - IP-CIDR,173.252.64.0/18,🚀 节点选择,no-resolve
  - IP-CIDR,179.60.192.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,185.60.216.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,204.15.20.0/22,🚀 节点选择,no-resolve
  - DOMAIN-SUFFIX,github.com,🚀 节点选择
  - DOMAIN-SUFFIX,github.io,🚀 节点选择
  - DOMAIN-SUFFIX,githubapp.com,🚀 节点选择
  - DOMAIN-SUFFIX,githubassets.com,🚀 节点选择
  - DOMAIN-SUFFIX,githubusercontent.com,🚀 节点选择
  - DOMAIN-SUFFIX,1e100.net,🚀 节点选择
  - DOMAIN-SUFFIX,2mdn.net,🚀 节点选择
  - DOMAIN-SUFFIX,app-measurement.net,🚀 节点选择
  - DOMAIN-SUFFIX,g.co,🚀 节点选择
  - DOMAIN-SUFFIX,ggpht.com,🚀 节点选择
  - DOMAIN-SUFFIX,goo.gl,🚀 节点选择
  - DOMAIN-SUFFIX,googleapis.cn,🚀 节点选择
  - DOMAIN-SUFFIX,googleapis.com,🚀 节点选择
  - DOMAIN-SUFFIX,gstatic.cn,🚀 节点选择
  - DOMAIN-SUFFIX,gstatic.com,🚀 节点选择
  - DOMAIN-SUFFIX,gvt0.com,🚀 节点选择
  - DOMAIN-SUFFIX,gvt1.com,🚀 节点选择
  - DOMAIN-SUFFIX,gvt2.com,🚀 节点选择
  - DOMAIN-SUFFIX,gvt3.com,🚀 节点选择
  - DOMAIN-SUFFIX,xn--ngstr-lra8j.com,🚀 节点选择
  - DOMAIN-SUFFIX,youtu.be,🚀 节点选择
  - DOMAIN-SUFFIX,youtube-nocookie.com,🚀 节点选择
  - DOMAIN-SUFFIX,youtube.com,🚀 节点选择
  - DOMAIN-SUFFIX,yt.be,🚀 节点选择
  - DOMAIN-SUFFIX,ytimg.com,🚀 节点选择
  - IP-CIDR,74.125.0.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,173.194.0.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,120.232.181.162/32,🚀 节点选择,no-resolve
  - IP-CIDR,120.241.147.226/32,🚀 节点选择,no-resolve
  - IP-CIDR,120.253.253.226/32,🚀 节点选择,no-resolve
  - IP-CIDR,120.253.255.162/32,🚀 节点选择,no-resolve
  - IP-CIDR,120.253.255.34/32,🚀 节点选择,no-resolve
  - IP-CIDR,120.253.255.98/32,🚀 节点选择,no-resolve
  - IP-CIDR,180.163.150.162/32,🚀 节点选择,no-resolve
  - IP-CIDR,180.163.150.34/32,🚀 节点选择,no-resolve
  - IP-CIDR,180.163.151.162/32,🚀 节点选择,no-resolve
  - IP-CIDR,180.163.151.34/32,🚀 节点选择,no-resolve
  - IP-CIDR,203.208.39.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,203.208.40.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,203.208.41.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,203.208.43.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,203.208.50.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,220.181.174.162/32,🚀 节点选择,no-resolve
  - IP-CIDR,220.181.174.226/32,🚀 节点选择,no-resolve
  - IP-CIDR,220.181.174.34/32,🚀 节点选择,no-resolve
  - DOMAIN-SUFFIX,cdninstagram.com,🚀 节点选择
  - DOMAIN-SUFFIX,instagram.com,🚀 节点选择
  - DOMAIN-SUFFIX,instagr.am,🚀 节点选择
  - DOMAIN-SUFFIX,kakao.com,🚀 节点选择
  - DOMAIN-SUFFIX,kakao.co.kr,🚀 节点选择
  - DOMAIN-SUFFIX,kakaocdn.net,🚀 节点选择
  - IP-CIDR,1.201.0.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,27.0.236.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,103.27.148.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,103.246.56.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,110.76.140.0/22,🚀 节点选择,no-resolve
  - IP-CIDR,113.61.104.0/22,🚀 节点选择,no-resolve
  - DOMAIN-SUFFIX,lin.ee,🚀 节点选择
  - DOMAIN-SUFFIX,line-apps.com,🚀 节点选择
  - DOMAIN-SUFFIX,line-cdn.net,🚀 节点选择
  - DOMAIN-SUFFIX,line-scdn.net,🚀 节点选择
  - DOMAIN-SUFFIX,line.me,🚀 节点选择
  - DOMAIN-SUFFIX,line.naver.jp,🚀 节点选择
  - DOMAIN-SUFFIX,nhncorp.jp,🚀 节点选择
  - IP-CIDR,103.2.28.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,103.2.30.0/23,🚀 节点选择,no-resolve
  - IP-CIDR,119.235.224.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,119.235.232.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,119.235.235.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,119.235.236.0/23,🚀 节点选择,no-resolve
  - IP-CIDR,147.92.128.0/17,🚀 节点选择,no-resolve
  - IP-CIDR,203.104.128.0/19,🚀 节点选择,no-resolve
  - DOMAIN-KEYWORD,1drv,🚀 节点选择
  - DOMAIN-KEYWORD,onedrive,🚀 节点选择
  - DOMAIN-KEYWORD,skydrive,🚀 节点选择
  - DOMAIN-SUFFIX,livefilestore.com,🚀 节点选择
  - DOMAIN-SUFFIX,oneclient.sfx.ms,🚀 节点选择
  - DOMAIN-SUFFIX,onedrive.com,🚀 节点选择
  - DOMAIN-SUFFIX,onedrive.live.com,🚀 节点选择
  - DOMAIN-SUFFIX,photos.live.com,🚀 节点选择
  - DOMAIN-SUFFIX,skydrive.wns.windows.com,🚀 节点选择
  - DOMAIN-SUFFIX,spoprod-a.akamaihd.net,🚀 节点选择
  - DOMAIN-SUFFIX,storage.live.com,🚀 节点选择
  - DOMAIN-SUFFIX,storage.msn.com,🚀 节点选择
  - DOMAIN-KEYWORD,porn,🚀 节点选择
  - DOMAIN-SUFFIX,8teenxxx.com,🚀 节点选择
  - DOMAIN-SUFFIX,ahcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,bcvcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,bongacams.com,🚀 节点选择
  - DOMAIN-SUFFIX,chaturbate.com,🚀 节点选择
  - DOMAIN-SUFFIX,dditscdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,livejasmin.com,🚀 节点选择
  - DOMAIN-SUFFIX,phncdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,phprcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,pornhub.com,🚀 节点选择
  - DOMAIN-SUFFIX,pornhubpremium.com,🚀 节点选择
  - DOMAIN-SUFFIX,rdtcdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,redtube.com,🚀 节点选择
  - DOMAIN-SUFFIX,sb-cd.com,🚀 节点选择
  - DOMAIN-SUFFIX,spankbang.com,🚀 节点选择
  - DOMAIN-SUFFIX,t66y.com,🚀 节点选择
  - DOMAIN-SUFFIX,xhamster.com,🚀 节点选择
  - DOMAIN-SUFFIX,xnxx-cdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,xnxx.com,🚀 节点选择
  - DOMAIN-SUFFIX,xvideos-cdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,xvideos.com,🚀 节点选择
  - DOMAIN-SUFFIX,ypncdn.com,🚀 节点选择
  - DOMAIN-SUFFIX,pixiv.net,🚀 节点选择
  - DOMAIN-SUFFIX,pximg.net,🚀 节点选择
  - DOMAIN-SUFFIX,amplitude.com,🚀 节点选择
  - DOMAIN-SUFFIX,firebaseio.com,🚀 节点选择
  - DOMAIN-SUFFIX,hockeyapp.net,🚀 节点选择
  - DOMAIN-SUFFIX,readdle.com,🚀 节点选择
  - DOMAIN-SUFFIX,smartmailcloud.com,🚀 节点选择
  - DOMAIN-SUFFIX,fanatical.com,🚀 节点选择
  - DOMAIN-SUFFIX,humblebundle.com,🚀 节点选择
  - DOMAIN-SUFFIX,steamcommunity.com,🚀 节点选择
  - DOMAIN-SUFFIX,tap.io,🚀 节点选择
  - DOMAIN-SUFFIX,taptap.tw,🚀 节点选择
  - DOMAIN-SUFFIX,twitch.tv,🚀 节点选择
  - DOMAIN-SUFFIX,ttvnw.net,🚀 节点选择
  - DOMAIN-SUFFIX,jtvnw.net,🚀 节点选择
  - DOMAIN-KEYWORD,ttvnw,🚀 节点选择
  - DOMAIN-SUFFIX,t.co,🚀 节点选择
  - DOMAIN-SUFFIX,twimg.co,🚀 节点选择
  - DOMAIN-SUFFIX,twimg.com,🚀 节点选择
  - DOMAIN-SUFFIX,twimg.org,🚀 节点选择
  - DOMAIN-SUFFIX,t.me,🚀 节点选择
  - DOMAIN-SUFFIX,tdesktop.com,🚀 节点选择
  - DOMAIN-SUFFIX,telegra.ph,🚀 节点选择
  - DOMAIN-SUFFIX,telegram.me,🚀 节点选择
  - DOMAIN-SUFFIX,telegram.org,🚀 节点选择
  - DOMAIN-SUFFIX,telesco.pe,🚀 节点选择
  - IP-CIDR,91.108.0.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,109.239.140.0/24,🚀 节点选择,no-resolve
  - IP-CIDR,149.154.160.0/20,🚀 节点选择,no-resolve
  - IP-CIDR6,2001:67c:4e8::/48,🚀 节点选择,no-resolve
  - IP-CIDR6,2001:b28:f23d::/48,🚀 节点选择,no-resolve
  - IP-CIDR6,2001:b28:f23f::/48,🚀 节点选择,no-resolve
  - DOMAIN-SUFFIX,terabox.com,🚀 节点选择
  - DOMAIN-SUFFIX,teraboxcdn.com,🚀 节点选择
  - IP-CIDR,18.194.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,34.224.0.0/12,🚀 节点选择,no-resolve
  - IP-CIDR,54.242.0.0/15,🚀 节点选择,no-resolve
  - IP-CIDR,50.22.198.204/30,🚀 节点选择,no-resolve
  - IP-CIDR,208.43.122.128/27,🚀 节点选择,no-resolve
  - IP-CIDR,108.168.174.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,173.192.231.32/27,🚀 节点选择,no-resolve
  - IP-CIDR,158.85.5.192/27,🚀 节点选择,no-resolve
  - IP-CIDR,174.37.243.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,158.85.46.128/27,🚀 节点选择,no-resolve
  - IP-CIDR,173.192.222.160/27,🚀 节点选择,no-resolve
  - IP-CIDR,184.173.128.0/17,🚀 节点选择,no-resolve
  - IP-CIDR,158.85.224.160/27,🚀 节点选择,no-resolve
  - IP-CIDR,75.126.150.0/16,🚀 节点选择,no-resolve
  - IP-CIDR,69.171.235.0/16,🚀 节点选择,no-resolve
  - DOMAIN-SUFFIX,mediawiki.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikibooks.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikidata.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikileaks.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikimedia.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikinews.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikipedia.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikiquote.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikisource.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikiversity.org,🚀 节点选择
  - DOMAIN-SUFFIX,wikivoyage.org,🚀 节点选择
  - DOMAIN-SUFFIX,wiktionary.org,🚀 节点选择
  - DOMAIN-SUFFIX,neulion.com,🚀 节点选择
  - DOMAIN-SUFFIX,icntv.xyz,🚀 节点选择
  - DOMAIN-SUFFIX,flzbcdn.xyz,🚀 节点选择
  - DOMAIN-SUFFIX,ocnttv.com,🚀 节点选择
  - MATCH,🐟 漏网之鱼





```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/02.27:17:30:40.png" style="width:400px;"></p>

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/02.27:17:32:58.png" style="width:400px;"></p>