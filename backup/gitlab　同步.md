##  gitlab 登录

- https://gitlab.com/users/sign_in

## 新建空白项目

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:07:26.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:11:58.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:14:03.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:15:13.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:21:23.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:21:51.png" style="width:400px;"></p>

## 得到 GITLAB_PAT    glpat-sWZjDWp5ruPVYXL_RTPo

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:23:06.png" style="width:400px;"></p>

=============================================

## Github 设置

- https://github.com/zb9678/zb9678.github.io/settings/secrets/actions

- 设置3个 secrets

GITLAB_USERNAME	zb9678
GITLAB_REPO	Gitlab      zb9678.github.io1
GITLAB_PAT	                glpat-sWZjDWp5ruPVYXL_RTPo

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:26:56.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:28:24.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:29:30.png" style="width:400px;"></p>


## Github 设置同步 sync-to-gitlab.yml

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:33:20.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:32:05.png" style="width:400px;"></p>

---------------------------------------------------------------------------------------------------

##   sync-to-gitlab.yml 　内容



```
name: Sync to GitLab

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  sync:
    runs-on: ubuntu-latest

    env:
      GITLAB_USERNAME: ${{ secrets.GITLAB_USERNAME }}
      GITLAB_REPO: ${{ secrets.GITLAB_REPO }}
      GITLAB_PAT: ${{ secrets.GITLAB_PAT }}

    steps:
    - name: Checkout repository
      uses: actions/checkout@v4.1.1
      with:
        fetch-depth: 0

    - name: Set up Git
      run: |
        git config --global user.name 'github-actions'
        git config --global user.email 'github-actions@github.com'

    - name: Add GitLab remote
      run: git remote add gitlab https://${{ env.GITLAB_USERNAME }}:${{ env.GITLAB_PAT }}@gitlab.com/${{ env.GITLAB_USERNAME }}/${{ env.GITLAB_REPO }}.git

    - name: Force push to GitLab
      run: git push gitlab main --force
```

## gitlab 删库

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:41:41.png" style="width:400px;"></p>

<p align="center"><img src="https://raw.githubusercontent.com/zb9678/img/main/im2/z11.19:17:43:32.png" style="width:400px;"></p>