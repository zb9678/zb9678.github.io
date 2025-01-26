## 任务栏透明度

WinSet, Transparent, 210, ahk_class Shell_TrayWnd			        ; 210  0-255 任务栏透明度


## 更新 github_hosts

Run, "C:\Program Files\Git\git-bash.exe" --hide "D:\ahk1.0\fetch_github_hosts", , Hide


### fetch_github_hosts 文件

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

### Git 下载

- https://git-scm.com/downloads


