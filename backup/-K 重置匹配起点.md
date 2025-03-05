## \K 重置匹配起点

abxyzc123xyz789

- 目标：匹配 xyz，但只在它前面有数字的情况下。

```
\d+\Kxyz
```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.04:18:23:08.png" style="width:400px;"></p><br>

\d+ 匹配字符串中的 123。
/K 重置匹配起点，从xyz开始。

## 式\K中|(?:\G(?!^))主要

```
先匹配到了`式`，
通过 `/K` 重置匹配起始位置，匹配到其后的`中`，
 |
(?:\G(?!^))主要  这段代码则将中做为起始，匹配连续的`主要`。
```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.05:14:13:25.png" style="width:400px;"></p><br>