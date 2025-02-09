## 给任意网址如 ser07.rr.nu  在CF上添加自定义域

- 在cloudflare中新建Workers 并修改worker.js代码如下

- 注意修改此行  url.host = 'ser07.rr.nu';

- https://dash.cloudflare.com/addfe9fc56c06acb158fd7b4883b478f/workers/services/edit/rruu/production

```
/**
 * Welcome to Cloudflare Workers! This is your first worker.
 *
 * - Run "npm run dev" in your terminal to start a development server
 * - Open a browser tab at http://localhost:8787/ to see your worker in action
 * - Run "npm run deploy" to publish your worker
 *
 * Learn more at https://developers.cloudflare.com/workers/
 */


export default {

  async fetch(request, env) {

    const url = new URL(request.url);

    url.host = 'ser07.rr.nu';

    return fetch(new Request(url, request))

  }


}

```


