`@echo off
:menu
cls
echo ===========================================
echo        Recall 功能管理脚本
echo ===========================================
echo.
echo 1. 查看 Recall 功能状态
echo 2. 禁用 Recall 功能
echo 3. 启用 Recall 功能
echo 4. 退出
echo.
set /p choice="请选择一个选项 (1-4): "
:menu
cls
echo ===========================================
echo        Recall 功能管理脚本
echo ===========================================
echo.
echo 1. 查看 Recall 功能状态
echo 2. 禁用 Recall 功能
echo 3. 启用 Recall 功能
echo 4. 退出
echo.
set /p choice="请选择一个选项 (1-4): "

if "%choice%"=="1" goto check
if "%choice%"=="2" goto disable
if "%choice%"=="3" goto enable
if "%choice%"=="4" goto exit

echo 无效的选择。请选择一个有效的选项。
pause
goto menu

:check
cls
echo 正在检查 Recall 功能状态...
Dism /Online /Get-FeatureInfo /FeatureName:Recall
pause
goto menu

:disable
cls
echo 正在禁用 Recall 功能...
Dism /Online /Disable-Feature /FeatureName:Recall
pause
goto menu

:enable
cls
echo 正在启用 Recall 功能...
Dism /Online /Enable-Feature /FeatureName:Recall
pause
goto menu

:exit
exit
 (1-4): "

if "%choice%"=="1" goto check
if "%choice%"=="2" goto disable
if "%choice%"=="3" goto enable
if "%choice%"=="4" goto exit

echo 无效的选择。请选择一个有效的选项。
pause
goto menu

:check
cls
echo 正在检查 Recall 功能状态...
Dism /Online /Get-FeatureInfo /FeatureName:Recall
pause
goto menu

:disable
cls
echo 正在禁用 Recall 功能...
Dism /Online /Disable-Feature /FeatureName:Recall
pause
goto menu

:enable
cls
echo 正在启用 Recall 功能...
Dism /Online /Enable-Feature /FeatureName:Recall
pause
goto menu

:exit
exit
`