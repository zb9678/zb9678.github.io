## >! 2345sdf复制  wertxcv 粘贴

```
#Persistent
	Copy(clipboardID) 
{
	global ; All variables are global by default
	local oldClipboard := ClipboardAll ; Save the (real) clipboard

	Clipboard := "" ; Erase the clipboard first, or else ClipWait does nothing
	SendInput {Ctrl Down}c{Ctrl Up}
	ClipWait, 2, 1 ; Wait 1s until the clipboard contains any kind of data
if ErrorLevel 
{
	Clipboard := oldClipboard ; Restore old (real) clipboard
	return
}
	ClipboardData%clipboardID% := Clipboard
	Clipboard := oldClipboard ; Restore old (real) clipboard
}
Cut(clipboardID) 
{
	global ; All variables are global by default
	local oldClipboard := ClipboardAll ; Save the (real) clipboard
	Clipboard := "" ; Erase the clipboard first, or else ClipWait does nothing
	SendInput {Ctrl Down}x{Ctrl Up}
	ClipWait, 2, 1 ; Wait 1s until the clipboard contains any kind of data
if ErrorLevel 
{
	Clipboard := oldClipboard ; Restore old (real) clipboard
	return
}
	ClipboardData%clipboardID% := Clipboard
	Clipboard := oldClipboard ; Restore old (real) clipboard
}
Paste(clipboardID) 
{
	global
	local oldClipboard := ClipboardAll ; Save the (real) clipboard
	Clipboard := "" ; Erase the clipboard first, or else ClipWait does nothing
	Clipboard := ClipboardData%clipboardID%
	ClipWait, 2, 1 ; Wait 1s until the clipboard contains any kind of data
	SendRaw, % Clipboard ; Was having an issue with ^v
	Clipboard := oldClipboard ; Restore old (real) clipboard
}
	return
;---------------------------------------------------------------------------   copy
 >!2::Copy(1)
 >!3::Copy(2)
 >!4::Copy(3)
 >!5::Copy(4)
 >!s::Copy(5)
 >!d::Copy(6)
 >!f::Copy(7)
 ;---------------------------------------------------------------------------   paste
 >!w::Paste(1)
 >!e::Paste(2)
 >!r::Paste(3)
 >!t::Paste(4)
 >!x::Paste(5)
 >!c::Paste(6)
 >!v::Paste(7)
;-----------------------------------------------------------------------------   cut
 >!g::Cut(1)
 >!h::Cut(2)
 >!j::Cut(3)
 >!k::Cut(4)
;---------------------------------------------------------------------------   paste
 >!b::Paste(1)                                 ;-------------->! g 剪切    >! b 粘贴
 >!n::Paste(2)
 >!m::Paste(3)
 >!,::Paste(4)
;-----------------------------------------------------------------------------------
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ >! 2345sdf复制  wertxcv 粘贴  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 05-322
```