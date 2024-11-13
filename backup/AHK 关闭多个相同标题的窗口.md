
<p align='center'><img src="https://img.r08.us.kg/img/main/images/20241112085429.png" style='width:400px;'><br><br>

<p align='center'><img src="https://img.r08.us.kg/img/main/images/L11.12:09:15:55.png" style='width:400px;'><br><br>

#SingleInstance Force
SetTitleMatchMode 2

#n::
  run notepad
  Return
  
^!f4::
  WinGetTitle sTitle, A
  ; MsgBox %sTitle%
  ; InputBox, OutputVar [, Title, Prompt, HIDE, Width, Height, X, Y, Font, Timeout, Default]
  InputBox sTitle, 視窗標題, 請輸入視窗的標題文字, , 300, 150, , , , , %sTitle%
  if (sTitle = "nb") {
      sTitle := "記事本"  ;; 或用 sTitle = 記事本
  } else if (sTitle = "ie") {
      sTitle := "Internet Explorer"
  }
  while WinExist(sTitle)　　　　　　　　　　　　　while多少满足条件　　此处为数个记事本
                                                if WinExist(sTitle)          if　 单个满足条件　　单个记事本
    WinClose
  Return