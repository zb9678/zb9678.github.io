## #n前 #b后 explorer  chrome PDFXEdit

```
#If ( WinActive("ahk_exe explorer.exe"))
#SingleInstance Force
#n::
send, <!{right}
  return
#b::
send, <!{left}
return
#IfWinActive
;-----------------------------------------------------------------------------------
#If ( WinActive("ahk_exe chrome.exe") or  WinActive("ahk_exe PDFXEdit.exe"))
#SingleInstance Force
#n::
send, <^+{tab}
  return
#b::
send, <^{tab}
return
#IfWinActive
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  #n前 #b后 explorer  chrome PDFXEdit  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00015-1067

```