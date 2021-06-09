> #### window10 去掉桌面图标快捷方式箭头


1. 桌面任意位置>右键>新建>文本文档>将以下内容复制粘贴进去后保存。
2. 将文本文档的后缀修改.bat。 
3. 再右键以管理员身份运行，重启电脑。 搞定啦！

```
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Icons" /v 29 /d "%systemroot%\system32\imageres.dll,197" /t reg_sz /f
taskkill /f /im explorer.exe
attrib -s -r -h "%userprofile%\AppData\Local\iconcache.db"
del "%userprofile%\AppData\Local\iconcache.db" /f /q
start explorer
pause

```