## 选中后用 EmEditor 打开

```
	#IfWinActive ahk_class TTOTAL_CMD
	AppsKey & F2::
#IfWinActive ahk_class CabinetWClass
AppsKey & F2::
	#IfWinActive ahk_class ExploreWClass
	AppsKey & F2::
#IfWinActive ahk_class Progman
AppsKey & F2::
	#IfWinActive ahk_class WorkerW
	AppsKey & F2::
WinGet, hWnd, ID, A
WinGetClass, vWinClass, % "ahk_id " hWnd
vPath := "", vIsDir := 0

	if (vWinClass = "TTOTAL_CMD")
{
	MsgBox "Tc"
}
	if (vWinClass = "CabinetWClass") || (vWinClass = "ExploreWClass")
{
	for oWin in ComObjCreate("Shell.Application").Windows
{
	if (oWin.HWND = hWnd)
{
	vIsDir := oWin.Document.FocusedItem.IsFolder
	vPath := oWin.Document.FocusedItem.Path
	break
}
}
	oWin := ""
}
else if (vWinClass = "Progman") || (vWinClass = "WorkerW")
{
	VarSetCapacity(hWnd, 4, 0)
	;SWC_DESKTOP := 0x8 ;VT_BYREF := 0x4000 ;VT_I4 := 0x3 ;SWFO_NEEDDISPATCH := 0x1
	oWin := ComObjCreate("Shell.Application").Windows.FindWindowSW(0, "", 8, ComObject(0x4003, &hWnd), 1)
	vIsDir := oWin.Document.FocusedItem.IsFolder
	vPath := oWin.Document.FocusedItem.Path
	oWin := ""
}

if (vPath = "")
{
	MsgBox, % "error: file not found"
	return
}
else if !FileExist(vPath)
{
	MsgBox, % "error: file not found:`r`n" vPath
	return
}
else if vIsDir
{
	Run, % Chr(34) vPath Chr(34)
	return
}
	FileGetSize, vSizeMB, % vPath, M
	if (vSizeMB > 6)
{
	MsgBox, % "error: file too big: " vSizeMB " MB"
	return
}
	SplitPath, vPath, vName, vDir, vExt, vNameNoExt, vDrive
	FileGetSize, vSizeMB, % vPath, M
	if (vExt = "lnk")
	FileGetShortcut, % vPath, vPath
	if vExt in bat,ahk,reg,txt,htm,html,mht,cpp,h,m3u,mpcpl,url,clp,ini,cfg,csv,srt,log,js,xml,toml,json,css,vbs,md,dat,ah2,conf,yml,toml,pub,cmd
	Run, "D:\ahk1.0\Lib\0 tool\EmEditor\EmEditor.exe" "%vPath%"
else if vExt in bmp,gif,jpe,jpeg,jpg,png,ico
	Run, "c:\3\iview460_x64\i_view64.exe" "%vPath%"
else if vExt in md
	Run, "c:\3\Typora0.9.98\Typora.exe" "%vPath%"
	Return
;ΞΞΞΞΞΞΞΞΞΞΞΞ   AppsKey & F2  选中图标 用 EmEditor 打开   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13-448
```
