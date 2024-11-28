- 检查运行的应用有几种方法，例如 #IfWinActive, ahk_exe, wt 或 if WinActive("wt") 等。
- 要检查运行的服务则要用到 sc.exe
- 
## sc.exe

- sc用法
- 功能： SC 是一個用來和服務控制管理員及服務溝通的命令列程式
- 語法： sc <server> [command] [service name] <option1> <option2>...
- command: query - 查詢服務的狀態，或列舉服務類型的狀態

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/11.28:20:02:17.png" style="width:400px;"></p>

## 启动服务

- 可以用 net.exe 或 sc start 命令。

net start ADEsvc

## ahk

`;; chk-is-running  服務名稱 系統目錄  啟動批次檔名
;; chk-is-running gitea z:\test\gitea start_service.bat
#SingleInstance Force

ServiceName = %1%    ;; "gitea"
ServiceDir = %2%  ;;"z:\test\gitea"   ;; 系統目錄
StartBat = %3%  ;;"start_service.bat"  ;; 啟動服務的批次檔

ServiceChk = sc query "%ServiceName%" > %ServiceDir%\chk-is-running.txt
runwait, %COMSPEC% /C %ServiceChk%, ,Hide  

FileRead, FileContent, %ServiceDir%\chk-is-running.txt
Loop, Parse, FileContent, `n,`r
{
FileLine = %A_LoopField%
Lookfor = STATE
  IfInString, FileLine, %LookFor%
  {
    StringGetPos, pointer, FileLine, :
    StringRight, ServerStatus, FileLine, StrLen(FileLine) - pointer - 5
    if (ServerStatus == "RUNNING") {
      FileAppend, % PID . " " . A_YYYY . "-" . A_MM . "-" . A_DD . " " . A_Hour . ":" . A_Min . ":" . A_Sec . " " . ServiceName . " is running " . " `n", %ServiceDir%\chk-is-running.log
    } else {
      Run, %ServiceDir%\%StartBat% , %ServiceDir%, Hide|UseErrorLevel, PID
      ;;MsgBox %ErrorLevel%
      FileAppend, % PID . " " . A_YYYY . "-" . A_MM . "-" . A_DD . " " . A_Hour . ":" . A_Min . ":" . A_Sec . " After net start " . ErrorLevel . " `n", %ServiceDir%\chk-is-running.log
    }
  }
}
Return`
