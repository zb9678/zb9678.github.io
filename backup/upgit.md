## AHK脚本

```
-  -o clipboard　上传后得到的网址输出到剪贴板　
-  -f ccc　           输出格式为 ccc  
- "ccc" = '<p align="center"><img src="{url}" style="width:400px;"></p>'

F1 & s::
    ; 显示上传中提示
    Text := "⭕ 上传图片中 ⭕"
    btt(Text, 600, 0, , "Style4")
    ; 运行 upgit 上传命令，将 URL 复制到剪贴板
    Run, D:\ahk1.0\Lib\0 tool\picgo-croe\upgit.exe :clipboard -o clipboard -f ccc
, , hide
    return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & s  上传截图到github/img   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 
```

====================================================

## config.toml

```
- D:\ahk1.0\Lib\0 tool\picgo-croe\config.toml
- D:\ahk1.0\Lib\0 tool\picgo-croe\upgit.exe
-----------------------------------------------------

`rename = "im/Ugit{month}.{day}:{hour}:{minute}:{second}{ext}"
default_uploader = "github"

[output_formats]
"bbcode" = "[img]{url}[/img]"
"html" = '<img src="{url}" />'
"markdown" = "![]({url})"
"ccc" = '<p align="center"><img src="{url}" style="width:400px;"></p>'


[uploaders.github]
# 保存文件的分支，例如 master 或 main
branch = "main"
pat = "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"
repo = "img"
username = "zcr07"
```

---------------------------------------------------------

- 注意： "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"  
- 有效期
- Expiration  选　No expiration
- 此处爱出问题。 不行就重新申请Token
- https://github.com/settings/tokens  

==================================================

## works.js   

```
- Zcr071225@gmail.com  Workers 和 Pages  imgpic
- https://dash.cloudflare.com/addfe9fc56c06acb158fd7b4883b478f/workers/services/edit/imgpic/production
- 
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url)
  const path = url.pathname
  
  // 定义环境变量 GITHUB_USERNAME 和 GITHUB_PAT
   const GITHUB_USERNAME = 'zcr07' // 替换为你的 GitHub 用户名
   const GITHUB_PAT = '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' // 替换为你的 GitHub PAT，只开放 repo 权限即可
  
  // 构建 GitHub raw 内容的 URL
  const githubUrl = `https://raw.githubusercontent.com/${path}`
  
  // 创建新的请求，添加必要的头部
  const modifiedRequest = new Request(githubUrl, {
    method: request.method,
    headers: {
      ...request.headers,
      'Authorization': `token ${GITHUB_PAT}`,
      'Accept': 'application/vnd.github.v3.raw'
    }
  })
  
  // 发送请求并返回响应
  try {
    const response = await fetch(modifiedRequest)
    
    // 如果响应不成功，抛出错误
    if (!response.ok) {
      throw new Error(`GitHub API responded with ${response.status}: ${response.statusText}`)
    }
    
    // 创建新的响应，保留原始内容但移除敏感头部
    const newResponse = new Response(response.body, response)
    newResponse.headers.delete('Authorization')
    
    return newResponse
  } catch (error) {
    return new Response(`Error: ${error.message}`, { status: 500 })
  }
}
```

===================================================

## gitlab　同步

- https://gitlab.com/zcr071225/img
- 教程
- https://www.youtube.com/watch?v=eRqIpeeo9SA


```
 config.toml  老版不用
- D:\ahk1.0\Lib\0 tool\picgo-croe\config.toml

`rename = "im/Ugit{month}.{day}:{hour}:{minute}:{second}{ext}"
default_uploader = "github"
[replacements]
"raw.githubusercontent.com" = "img.r08.us.kg"

[uploaders.github]
# 保存文件的分支，例如 master 或 main
branch = "main"
pat = "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"
repo = "img"
username = "zcr07"`
```
===============================================
