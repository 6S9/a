### 命令行hentai-cosplay.com下载器
https://www.jianshu.com/p/d88b40480054
```
@echo on
color 0a
set version=1.0.1
title=示例程序 %version%

if "%proxy%"=="" set proxy=127.0.0.1:1080
if "%downloads_folder%"=="" if exist F:\Downloads\ set downloads_folder=F:\Downloads\ else set downloads_folder=D:\Downloads\

:main
cls
if "%target%"=="" set /p target=请粘贴目标网址：
:get_lastpage
curl -k -L -# -o target_utf8.temp %target% -e "%target%" -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.167 Safari/537.36"
if exist target_utf8.temp (
iconv -c -f UTF-8 -t GBK  target_utf8.temp > target_gbk.temp
sed -i "s#\"#\n#g" target_gbk.temp
del *.
findstr "最後" target_gbk.temp >nul && egrep -B1 "最後" target_gbk.temp | egrep "/image/" | sed "s#^#https://ja.hentai-cosplay.com#g" > target_lastpageurl.temp || echo %target% > target_lastpageurl.temp
egrep "<title>" target_gbk.temp | sed "s#<title>##g;s# - エロコスプレ</title>##g;s#^[[:blank:]]*##g;s#[[:blank:]]#_#g" > target_title.temp
) else goto get_lastpage

:get_lastimage
for /f %%l in (target_lastpageurl.temp) do (
curl -k -L -# -o target_lastpageutf8.temp %%l -e "%target%" -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.167 Safari/537.36"
if exist target_lastpageutf8.temp (
iconv -c -f UTF-8 -t GBK  target_lastpageutf8.temp > target_lastpagegbk.temp
sed -i "s#\"#\n#g" target_lastpagegbk.temp
sed -i "s#=#\n#g" target_lastpagegbk.temp
del *.
egrep "hentai-cosplay.com/upload/" target_lastpagegbk.temp | egrep "[0-9]\.[[:alpha:]]*$" | sort | uniq |tail -1 | sed "s#/#/\n#7;s#\.#\n\.#3" > target_lastimageurl.temp
) else goto get_lastimage
)

:seq_imageurl
if exist target_lastimageurl.temp (
sed -n "1p" target_lastimageurl.temp > target_imageurl1.temp
sed -n "2p" target_lastimageurl.temp > target_imageurl2.temp
sed -n "3p" target_lastimageurl.temp > target_imageurl3.temp
)

for /f %%i in (target_imageurl1.temp) do (
for /f %%j in (target_imageurl2.temp) do (
for /f %%k in (target_imageurl3.temp) do (
seq -f "%%i%%01g%%k" 1 1 %%j > target_imageurl.temp
)
)
)

:aria2c
for /f %%t in (target_title.temp) do (
if exist target_imageurl.temp aria2c --file-allocation=none --max-concurrent-downloads=100 --max-connection-per-server=16 --dir=%%t -i target_imageurl.temp
)

:end
if exist *. del *.
if exist *.temp del *.temp


``
