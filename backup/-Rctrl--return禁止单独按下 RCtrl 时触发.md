## 如何使 Rctrl & a 快捷键组合按下时，不会激活 Send, #{Space}

- 给脚本添加   

`#HotkeyModifierTimeout 0`

` *Rctrl::return  ; 禁止单独按下 RCtrl 时触发`

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/12.13:23:19:25.png" style="width:400px;"></p>


```
Rctrl::  
Send, #{Space}
        SoundBeep, 300, 5
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  切换中英输入法   Rctrl  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 4-75
```

以下为SnoMouse.ahk脚本中的一部分

```
#HotkeyModifierTimeout 0
;*Rctrl::return  ; 禁止单独按下 RCtrl 时触发
; 鼠标运动处理
*>^a:: 鼠标模拟.左按("a")
*>^d:: 鼠标模拟.右按("d")
*>^w:: 鼠标模拟.上按("w")               ; * 号可以避免和系统自带的Alt+w冲突，造成上移时关闭文档。
*>^s:: 鼠标模拟.下按("s")
```

## 完整的 SnoMouse.ahk

```
;#notrayicon
#Persistent
#SingleInstance force
#NoEnv 
#HotkeyModifierTimeout  0  ;影响热键修饰符的行为：CTRL、ALT、WIN 和 SHIFT。设为 0 时则总是超时 (修饰键总是不会被推回到按下的状态).
SetWorkingDir, %A_ScriptDir%
Process,priority, , high ;脚本进程优先级为高
#Include, D:\ahk1.0\Lib\AccModel.ahk            ;-------------------------------------------
Menu, Tray, Icon, D:\ahk1.0\Lib\0\Symbol purpel.ico 
global CapsLockXMode := 1
global TMouse_Disabled := 0
global TMouse_SendInput := 1
global TMouse_SendInputAPI := 1
global TMouse_SendInputScroll := 0
global TMouse_StickyCursor := 1
global TMouse_StopAtScreenEdge := 1
; 根据屏幕 DPI 比率，自动计算，得出，如果数值不对，才需要纠正
global TMouse_UseDPIRatio           := 1
global TMouse_MouseSpeedRatio       := 1   ;可调小
global TMouse_WheelSpeedRatio       := 1  ;可调小
global TMouse_DPIRatio              := TMouse_UseDPIRatio ? A_ScreenDPI / 96 : 1
global CapsLockX_WASD_MouseOrScroll := 1
; global debug_fps := new FPS_Debugger()
global 鼠标模拟 := new AccModel2D(Func("鼠标模拟"), 0.1, TMouse_DPIRatio * 120 * 2 * TMouse_MouseSpeedRatio)
global 滚轮模拟 := new AccModel2D(Func("滚轮模拟"), 0.1, TMouse_DPIRatio * 120 * 4 * TMouse_WheelSpeedRatio)
global 滚轮自动控制 := new AccModel2D(Func("滚轮自动控制"), 0.1, 10)
global 滚轮自动 := new AccModel2D(Func("滚轮自动"), 0, 1)

if (TMouse_SendInput) {
    SendMode Input   ;切换模式
}
; 解决多屏 DPI 问题
DllCall("Shcore.dll\SetProcessDpiAwareness", "UInt", 2)

; gestures supports
; [[AHK_H+Hv2] - WinApi() - Page 2 - Scripts and Functions - AutoHotkey Community]( https://www.autohotkey.com/board/topic/51243-ahk-hhv2-winapi/page-2 )
global WM_GESTURE:=281
global WM_GESTURENOTIFY:=282
global GID_BEGIN:=1
global GID_END:=2
global GID_ZOOM:=3
global GID_PAN:=4
global GID_ROTATE:=5
global GID_TWOFINGERTAP:=6
global GID_PRESSANDTAP:=7

CursorHandleGet()
{
    VarSetCapacity(PCURSORINFO, 20, 0) ;为鼠标信息 结构 设置出20字节空间
    NumPut(20, PCURSORINFO, 0, "UInt") ;*声明出 结构 的大小cbSize = 20字节
    DllCall("GetCursorInfo", "Ptr", &PCURSORINFO) ;获取 结构-光标信息
    if (NumGet(PCURSORINFO, 4, "UInt") == 0 ) ;当光标隐藏时，直接输出特征码为0
    Return 0
    Return NumGet(PCURSORINFO, 8)
}

CursorShapeChangedQ()
{
    static lA_Cursor := CursorHandleGet()
    if (lA_Cursor == CursorHandleGet()) {
        Return 0
    }
    lA_Cursor := CursorHandleGet()
    Return 1
}

sign(v)
{
    Return v == 0 ? 0 : (v > 0 ? 1 : -1)
}

Pos2Long(x, y)
{
    Return x | (y << 16)
}

SendInput_MouseMsg32(dwFlag, mouseData := 0)
{
    VarSetCapacity(sendData, 28, 0)
    NumPut(0, sendData, 0, "UInt")
    NumPut(0, sendData, 4, "Int")
    NumPut(0, sendData, 8, "Int")
    NumPut(mouseData, sendData, 12, "UInt")
    NumPut(dwFlag, sendData, 16, "UInt")
    DllCall("SendInput", "UInt", 1, "Str", sendData, "UInt", 28)
}
PostMessage_ScrollMouse(dx, dy)
{
    WM_MOUSEWHEEL := 0x020A
    WM_MOUSEWHEELH := 0x020E
    _:= dy && PostMessageForScroll(WM_MOUSEWHEEL, -dy)
    _:= dx && PostMessageForScroll(WM_MOUSEWHEELH, dx)
}
ScrollMouse(dx, dy)
{
    global TMouse_SendInputScroll
    if (TMouse_SendInputScroll) {
        SendInput_ScrollMouse(dx, dy)
    } else {
        PostMessage_ScrollMouse(dx, dy)
    }
}
SendInput_ScrollMouse(dx, dy)
{
    ; get cursor pos
    VarSetCapacity(POINT, 8, 0)
    DllCall("GetCursorPos", "Ptr", &POINT)
    x := NumGet(POINT, 0, "Int")
    y := NumGet(POINT, 4, "Int")
    ; scroll by system input message
    MOUSEEVENTF_WHEEL := 0x0800
    MOUSEEVENTF_HWHEEL := 0x1000
    if (dy) {
        size := A_PtrSize+4*4+A_PtrSize*2
        VarSetCapacity(mi, size, 0)
        NumPut(x, mi, A_PtrSize, "Int")   ; LONG dx
        NumPut(y, mi, A_PtrSize+4, "Int")  ; LONG dy
        NumPut(-dy, mi, A_PtrSize+4+4, "Int")  ; DWORD mouseData
        NumPut(MOUSEEVENTF_WHEEL, mi, A_PtrSize+4+4+4, "UInt")   ; DWORD dwFlags
        DllCall("SendInput", "UInt", 1, "Ptr", &mi, "Int", size )
        ; perf_timing()
    }
    if (dx) {
        ; todo fix sendinput
        PostMessage_ScrollMouse(dx, 0)

    }
}

SendInput_MouseMove(x, y)
{

    size := A_PtrSize+4*4+A_PtrSize*2
    VarSetCapacity(mi, size, 0)
    NumPut(x, mi, A_PtrSize, "Int")   ; int dx
    NumPut(y, mi, A_PtrSize+4, "Int")  ; int dy
    NumPut(0x0001, mi, A_PtrSize+4+4+4, "UInt")   ; DWORD dwFlags MOUSEEVENTF_MOVE
    DllCall("SendInput", "UInt", 1, "Ptr", &mi, "Int", size )
}
鼠标模拟2(dx, dy){
    SendInput_MouseMove(dx, dy)
    
}
ScrollModeToggle()
{
    global CapsLockX_WASD_MouseOrScroll
    if (CapsLockX_WASD_MouseOrScroll != 0) {
        CapsLockX_WASD_MouseOrScroll := 0
        ToolTip 鼠标模拟 已切换到 WASD 滚轮模式，再次按 CapsLockX+AD 可取消
        SetTimer 鼠标模拟_ToolTipRemove, -3000
    } else {
        CapsLockX_WASD_MouseOrScroll := 1
        ToolTip 鼠标模拟 已切换到 WASD 鼠标模式
        SetTimer 鼠标模拟_ToolTipRemove, -3000
    }
}
ScrollModeEnter()
{
    global CapsLockX_WASD_MouseOrScroll
    if (CapsLockX_WASD_MouseOrScroll != 0) {
        CapsLockX_WASD_MouseOrScroll := 0
        ToolTip 鼠标模拟 已切换到 WASD 滚轮模式，再次按 CapsLockX+AD 可取消
        SetTimer 鼠标模拟_ToolTipRemove, -3000
    }
}
ScrollModeExit()
{
    global CapsLockX_WASD_MouseOrScroll
    if (CapsLockX_WASD_MouseOrScroll != 1) {
        CapsLockX_WASD_MouseOrScroll := 1
        ToolTip 鼠标模拟 已切换到 WASD 鼠标模式
        SetTimer 鼠标模拟_ToolTipRemove, -3000
    }
}

; void 鼠标模拟
鼠标模拟(dx, dy, 状态){
    if (!CapsLockXMode) {
        鼠标模拟.止动()
        return
    }
    if (状态 == "横中键") {
        ScrollModeToggle()
        鼠标模拟.止动()
        return
    }
    if (状态 == "纵中键") {
        ScrollModeToggle()
        鼠标模拟.止动()
        return
    }
    if (状态 != "移动") {
        return
    }
    ; Shift 减速 =1
    if (GetKeyState("Shift", "P")) {
        sleep 100
        dx := dx == 0 ?  0 : (dx > 0 ? 1 : -1 )
        dy := dy == 0 ?  0 : (dy > 0 ? 1 : -1 )
    }
    if (TMouse_SendInputAPI) {
        ; 支持64位AHK！
        SendInput_MouseMove(dx, dy)
    } else {
        MouseMove, %dx%, %dy%, 0, R
    }
    
    ; TODO: 撞到屏幕边角就停下来
    ; if(TMouse_StopAtScreenEdge )
    ; MouseGetPos, xb, yb
    ; 鼠标模拟.横速 *= dx && xa == xb ? 0 : 1
    ; 鼠标模拟.纵速 *= dy && ya == yb ? 0 : 1
    
    
    ; 在各种按钮上减速，进出按钮时减速80%
    if (TMouse_StickyCursor && CursorShapeChangedQ()) {
        鼠标模拟.横速 *= 0.2
        鼠标模拟.纵速 *= 0.2
    }
}

滚轮自动(dx, dy, 状态){
    if (状态 != "移动") {
        return
    }
    ScrollMouse(dx, dy)
}
滚轮自动控制(dx, dy, 状态){
    if (状态 != "移动") {
        return
    }
    滚轮自动.横速 += dx, 滚轮自动.纵速 += dy, 滚轮自动.始动()
    msg := "【雪星滚轮自动v2】`n"
    msg .= "横：" (滚轮自动.横速|0) "px/s`n纵：" (滚轮自动.纵速|0)  "px/s`n"
    msg .= "CapsLockX + Ctrl + Alt + RF 调整纵向自动滚轮`n"
    msg .= "CapsLockX + Ctrl + Alt + Shift + RF 调整横向自动滚轮`n"
    鼠标模拟_ToolTip(msg)
}
滚轮模拟(dx, dy, 状态){
    if (!CapsLockXMode) {
        return 滚轮模拟.止动()
    }
    if ( 状态 == "横中键" || 状态 == "纵中键") {
        ScrollModeExit()
        
        SendEvent {Blind}{MButton Down}
        KeyWait r
        KeyWait f
        SendEvent {Blind}{MButton Up}
        ; 关闭滚轮自动
        if (滚轮自动.横速 || 滚轮自动.纵速) {
            滚轮自动.止动()
            滚轮自动控制(0, 0, "止动")
        }
        return
    }
    if (状态 != "移动") {
        return
    }
    ScrollMouse(dx, dy)
}
PostMessageForScroll(msg, zDelta)
{
    ; 目前还不支持 UWP which should use WM_TOUCH
    CoordMode, Mouse, Screen
    MouseGetPos, x, y, wid, fcontrol
    wParam := zDelta << 16 ;zDelta
    lParam := x | (y << 16) ; pos2long
    MouseGetPos, , , , ControlClass2, 2
    MouseGetPos, , , , , ControlClass3, 3
    if (A_Is64bitOS) {
        ControlClass1 := DllCall("WindowFromPoint", "int64", x | (y << 32), "Ptr") | 0x0
    } else {
        ControlClass1 := DllCall("WindowFromPoint", "int", x, "int", y) | 0x0
    }
    ;Detect modifer keys held down (only Shift and Control work)
    wParam |= GetKeyState("Shift", "p") ? 0x4 : 0
    wParam |= GetKeyState("Ctrl", "p")  ? 0x8 : 0
    if (ControlClass2 == "") {
        ; PostMessage, %msg%, %wParam%, %lParam%, %fcontrol%, ahk_id %ControlClass1%
        DllCall("PostMessage", "UInt", ControlClass1, "UInt", msg, "UInt", wParam, "UInt", lParam, "UInt")
    } else {
        ; PostMessage, %msg%, %wParam%, %lParam%, %fcontrol%, ahk_id %ControlClass2%
        DllCall("PostMessage", "UInt", ControlClass2, "UInt", msg, "UInt", wParam, "UInt", lParam, "UInt")
        if (ControlClass2 != ControlClass3) {
            ; PostMessage, %msg%, %wParam%, %lParam%, %fcontrol%, ahk_id %ControlClass3%
            DllCall("PostMessage", "UInt", ControlClass3, "UInt", msg, "UInt", wParam, "UInt", lParam, "UInt")
        }
    }
    if (wid) {
        DllCall("PostMessage", "UInt", wid, "UInt", msg, "UInt", wParam, "UInt", lParam, "UInt")
    }
    ; tooltip % x " " y "`n" ControlClass1  "`n"  ControlClass2 "`n" ControlClass3 "`n" wid
}

CapsLockX_鼠标左键按下(wait){
    ScrollModeExit()
    global CapsLockX_鼠标左键等待
    if (CapsLockX_鼠标左键等待) {
        return
    }
    CapsLockX_鼠标左键等待 := wait
    SendEvent {Blind}{LButton Down}
    KeyWait %wait%
    ; Hotkey, %wait% Up, CapsLockX_鼠标左键弹起
}
CapsLockX_鼠标左键弹起(){
    global CapsLockX_鼠标左键等待
    SendEvent {Blind}{LButton Up}
    CapsLockX_鼠标左键等待 := ""
    
}
CapsLockX_鼠标右键按下(wait){
    ScrollModeExit()
    global CapsLockX_鼠标右键等待
    if (CapsLockX_鼠标右键等待) {
        return
    }
    CapsLockX_鼠标右键等待 := wait
    SendEvent {Blind}{RButton Down}
    KeyWait %wait%
    ; Hotkey, %wait% Up, CapsLockX_鼠标右键弹起
}
CapsLockX_鼠标右键弹起(){
    global CapsLockX_鼠标右键等待
    SendEvent {Blind}{RButton Up}
    CapsLockX_鼠标右键等待 := ""
}
鼠标模拟_ToolTip(tips){
    ToolTip %tips%
    SetTimer 鼠标模拟_ToolTipRemove, -3000
}
鼠标模拟_ToolTipRemove(){
    ToolTip
}



#if CapsLockXMode && CapsLockX_MouseButtonSwitched
/*
; 鼠标按键处理
>^e:: CapsLockX_鼠标右键按下("e")
>^q:: CapsLockX_鼠标左键按下("q")
>^e Up::CapsLockX_鼠标右键弹起()
>^q Up:: CapsLockX_鼠标左键弹起()
*/
#if CapsLockXMode
*Rctrl::return  ; 禁止单独按下 RCtrl 时触发
; 鼠标运动处理
*>^a:: 鼠标模拟.左按("a")
*>^d:: 鼠标模拟.右按("d")
*>^w:: 鼠标模拟.上按("w")               ; * 号可以避免和系统自带的Alt+w冲突，造成上移时关闭文档。
*>^s:: 鼠标模拟.下按("s")

#if CapsLockXMode
*>^q::
    ScrollModeExit()
    滚轮模拟.上按("q")
return
*>^e::
    ScrollModeExit()
    滚轮模拟.下按("e")
return
;-----------------------------------------------模拟鼠标操作 WASD 鼠标移动，Q E 滚轮
#if CapsLockXMode

*>^g::                         ; 需连接2次g   
	SendEvent {click}{LButton down} 
	KeyWait, LButton                                                            
	return

; 🛏🛏🛏🛏🛏🛏🛏🛏🛏🛏  >^g 需连接2次g   左键按住   松开左键   🛏🛏🛏🛏🛏🛏🛏🛏🛏🛏🛏

z::
SendEvent {Blind}{RButton down}        
KeyWait Lwin
global SendEvent {Blind}{RButton up}
return

x::
SendEvent {Blind}{LButton down}          ;注意此处为LButton（鼠标左右换了）
KeyWait Rwin
global SendEvent {Blind}{LButton up}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  >^z 左键  >^x  右键   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 3

c::
Send {RButton down}
return
v::
SendEvent {click}
return
	KeyWait, RButton
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   c 左键按住   v 松开左键     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 4
#if CapsLockXMode
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ
;⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇠⇢⇢ 
#Persistent
SetTimer, Alert9, 500
WindowList:=[]
return
 
Alert9:
	Value := WindowList.Pop()
	if (Value=WinExist("A"))
	{
		WindowList.push(WinExist("A"))
	}
	else
	{
		if (value!="")
			WindowList.push(Value)
		WindowList.push(WinExist("A"))
	}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ

```