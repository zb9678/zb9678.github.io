## \K 重置匹配起点

abxyzc123xyz789

- 目标：匹配 xyz，但只在它前面有数字的情况下。

```
\d+\Kxyz
```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/im7/03.04:18:23:08.png" style="width:400px;"></p><br>

\d+ 匹配字符串中的 123。
/K 重置匹配起点，从xyz开始。