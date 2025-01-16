> [!TIP]
>  ? 的作用

- 可以有前缀 y   如可以打开 yā   
     - - 没有 ？的话，就打不出yā，只能打出 ā

```
::a8::ā     a8        需空格ā       ya8   只能单独使用，前面有y就不能变为 ā
:?:a0::ā   a0        需空格ā        yā     前面有y没关系。
```
-  以上这2个实例中，要注意 ā 的后面都有一个空格

> [!TIP]
>   * 的作用

- 自动输出   （区别于 o）
            - - 去除 ā 后的空格
            - 除非使用了 * 否则您必须在热字串的缩写后输入 终止符 才能触发它. 终止符最开始由以下内容组成:   -  (  )  [  ]  {  }   '  :  ;  "  /  \  ,  .  ?  !   `n   `t

```
:*:a9::ā    无需空格 ā          ya9      只能单独使用，前面有y就不能变为 ā
:*?:a7::ā   无需空格 ā          yā       前面有y没关系。
```
-  以上这2个实例中，要注意 ā 的后面没有空格

> [!TIP]
>   o 的作用

- 去除 ā 后的空格
- - 无法自动输出（* 号则可以，注意区别）

```
::a7::ā      ā 
:o:a6::ā    ā
```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/01.16:14:43:21.png" style="width:400px;"></p>

<p align='center'><img src="https://ing.w07.us.kg/images/20250116142301.png" style='width:400px;'><br><br>

> [!TIP]
>    c 的作用

- 输入时需要区分大小写

```
:c:Gu::xxx   只有输入的是是Gu才能输出xxx　　gu　GU　gU　　都无法输出xxx
```

### 例如

```
:C:BTW::  ; 输入所有大写字母.
:C:Btw::  ; 只有第一个字母输入大写字母.
: :btw::  ; 输入任何其他组合.
    case_conform_btw() {
        hs := A_ThisHotkey  ; 为了方便, 以防被打断.
        if (hs == ":C:BTW")
            Send BY THE WAY
        else if (hs == ":C:Btw")
            Send By the way
        else
            Send by the way
    }

3种输出结果
btw               by the way
BTW             BY THE WAY
Btw               By the way
```

> [!TIP]
>    r 的作用

-  原样输出，禁止转义

```
　:r:dc::{enter}　输入dc 原样输出 {enter} 　而不会转义成 回车
```

> [!TIP]
>    b0 的作用

- 在输入内容 <ll> 后添加 :: 后的内容 </ll>
  - - 注意，不是b，是 b0

```
:b0:<ll>::</ll>{left 5}           <ll>  </ll>
 :b:<li>::</li>{left 5}
 </li>
:ob0:<ll>::</ll>{left 5}           <ll></ll>
 :ob:<li>::</li>{left 5}             
</li>
```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/01.16:15:02:16.png" style="width:400px;"></p>
