`@echo off
setlocal enabledelayedexpansion

echo 请选择文件资源管理器样式:
echo 1. Windows 10 文件资源管理器
echo 2. Windows 11 文件资源管理器
set /p choice="输入选项 (1或2): "

if "%choice%"=="1" (
    echo 正在应用 Windows 10 文件资源管理器样式...
    reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{2aa9162e-c906-4dd9-ad0b-3d24a8eef5a0}" /v "" /t REG_SZ /d "CLSID_ItemsViewAdapter" /f
    reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{2aa9162e-c906-4dd9-ad0b-3d24a8eef5a0}\InProcServer32" /v "" /t REG_SZ /d "C:\Windows\System32\Windows.UI.FileExplorer.dll_" /f
    reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{2aa9162e-c906-4dd9-ad0b-3d24a8eef5a0}\InProcServer32" /v "ThreadingModel" /t REG_SZ /d "Apartment" /f
    reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{6480100b-5a83-4d1e-9f69-8ae5a88e9a33}" /v "" /t REG_SZ /d "File Explorer Xaml Island View Adapter" /f
    reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{6480100b-5a83-4d1e-9f69-8ae5a88e9a33}\InProcServer32" /v "" /t REG_SZ /d "C:\Windows\System32\Windows.UI.FileExplorer.dll_" /f
    reg add "HKEY_CURRENT_USER\Software\Classes\CLSID\{6480100b-5a83-4d1e-9f69-8ae5a88e9a33}\InProcServer32" /v "ThreadingModel" /t REG_SZ /d "Apartment" /f
    echo Windows 10 文件资源管理器样式已应用.
) else if "%choice%"=="2" (
    echo 正在应用 Windows 11 文件资源管理器样式...
    reg delete "HKEY_CURRENT_USER\Software\Classes\CLSID\{2aa9162e-c906-4dd9-ad0b-3d24a8eef5a0}" /f
    reg delete "HKEY_CURRENT_USER\Software\Classes\CLSID\{6480100b-5a83-4d1e-9f69-8ae5a88e9a33}" /f
    echo Windows 11 文件资源管理器样式已复原.
) else (
    echo 无效的选项，请选择 1 或 2.
    exit /b
)

set /p restart="是否重启资源管理器以使更改生效？(y/n): "
if /i "%restart%"=="y" (
    echo 正在重启资源管理器...
    taskkill /f /im explorer.exe
    start explorer.exe
    echo 资源管理器已重启.
) else (
    echo 请手动重启资源管理器以使更改生效.
)

endlocal
pause
`