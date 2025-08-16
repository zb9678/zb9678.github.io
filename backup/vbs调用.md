## vbs调用   修改hosts AHK脚本

```
SetWorkingDir, D:\ahk1.0\Lib\                             ; 必须这样设置，要不运行会报错
Run, "run_hidden.vbs", , Hide                               ; 完整路径 D:\ahk1.0\Lib\run_hidden.vbs
```

## vbs文件内容   D:\ahk1.0\Lib\run_hidden.vbs

```
Set UAC = CreateObject("Shell.Application")
UAC.ShellExecute "powershell.exe", "-WindowStyle Hidden -NoProfile -Command & 'C:\Program Files\Git\git-bash.exe' -c '/d/ahk1.0/fetch_github_hosts'", , "runas", 0
```

## D:\ahk1.0\fetch_github_hosts

```
_hosts=$(mktemp /tmp/hostsXXX)
hosts=/c/Windows/System32/drivers/etc/hosts
remote=https://raw.hellogithub.com/hosts
reg='/# GitHub520 Host Start/,/# Github520 Host End/d'

sed "$reg" $hosts > "$_hosts"
curl "$remote" >> "$_hosts"
cat "$_hosts" > "$hosts"

rm "$_hosts"

```
## hosts

```
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host
# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
# 
104.17.110.184 dash.cloudflare.com


127.0.0.1 http://tonec.com
127.0.0.1 http://www.tonec.com
#127.0.0.1 http://registeridm.com
#127.0.0.1 http://www.registeridm.com
#127.0.0.1 http://secure.registeridm.com
127.0.0.1 http://internetdownloadmanager.com
#127.0.0.1 http://www.internetdownloadmanager.com
#127.0.0.1 http://secure.internetdownloadmanager.com
#127.0.0.1 http://mirror.internetdownloadmanager.com
#127.0.0.1 http://mirror2.internetdownloadmanager.com
#127.0.0.1 http://mirror3.internetdownloadmanager.com


0.0.0.0 apps.corel.com
0.0.0.0 mc.corel.com
0.0.0.0 origin-mc.corel.com
0.0.0.0 iws.corel.com
127.0.0.1 mc.corel.co
127.0.0.1 apps.corel.com
127.0.0.1 origin-mc.corel.com
127.0.0.1 iws.corel.com
127.0.0.1 ipp.corel.com
127.0.0.1 secure.ipp.corel.com
127.0.0.1 content.corel.com
127.0.0.1 65.200.22.154
127.0.0.1 65.200.22.99
127.0.0.1 hub5btmain.sandai.net
127.0.0.1 mc.corel.com
127.0.0.1 ipm.corel.com
127.0.0.1 sws.corel.com
127.0.0.1 dam.corel.com
127.0.0.1 compute-1.amazonaws.com
127.0.0.1 www.corel.com
127.0.0.1 lm.licenses.adobe.com
127.0.0.1 na2m-pr.licenses.adobe.com
127.0.0.1 practivate.adobe.com
127.0.0.1 activate.adobe.com
127.0.0.1 ereg.adobe.com
127.0.0.1 wip.adobe.com
127.0.0.1 lmlicenses.wip4.adobe.com
127.0.0.1 cloud.coreldraw.app


# --- SWITCHHOSTS_CONTENT_START ---

# GitHub520 Host Start
140.82.114.25                 alive.github.com
20.205.243.168                api.github.com
140.82.112.21                 api.individual.githubcopilot.com
185.199.110.133               avatars.githubusercontent.com
185.199.110.133               avatars0.githubusercontent.com
185.199.110.133               avatars1.githubusercontent.com
185.199.110.133               avatars2.githubusercontent.com
185.199.110.133               avatars3.githubusercontent.com
185.199.110.133               avatars4.githubusercontent.com
185.199.110.133               avatars5.githubusercontent.com
185.199.110.133               camo.githubusercontent.com
140.82.112.21                 central.github.com
185.199.110.133               cloud.githubusercontent.com
20.205.243.165                codeload.github.com
140.82.114.22                 collector.github.com
185.199.110.133               desktop.githubusercontent.com
185.199.110.133               favicons.githubusercontent.com
20.205.243.166                gist.github.com
52.217.123.249                github-cloud.s3.amazonaws.com
3.5.30.104                    github-com.s3.amazonaws.com
52.217.207.121                github-production-release-asset-2e65be.s3.amazonaws.com
52.217.107.220                github-production-repository-file-5c1aeb.s3.amazonaws.com
16.15.217.211                 github-production-user-asset-6210df.s3.amazonaws.com
192.0.66.2                    github.blog
20.205.243.166                github.com
140.82.114.18                 github.community
185.199.108.154               github.githubassets.com
151.101.193.194               github.global.ssl.fastly.net
185.199.108.153               github.io
185.199.110.133               github.map.fastly.net
185.199.108.153               githubstatus.com
140.82.113.25                 live.github.com
185.199.110.133               media.githubusercontent.com
185.199.110.133               objects.githubusercontent.com
13.107.42.16                  pipelines.actions.githubusercontent.com
185.199.110.133               raw.githubusercontent.com
185.199.110.133               user-images.githubusercontent.com
13.107.246.73                 vscode.dev  # Timeout
140.82.112.21                 education.github.com
185.199.110.133               private-user-images.githubusercontent.com


# Update time: 2025-05-02T11:53:32+08:00
# Update url: https://raw.hellogithub.com/hosts
# Star me: https://github.com/521xueweihan/GitHub520
# GitHub520 Host End

```

