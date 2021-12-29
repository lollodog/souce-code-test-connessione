# souce-code-test-connessione

@echo off 



:verify
if exist "C:\Users\%username%\AppData\Local\Google\lollo" (goto set_variablili) else (goto no)

:ver2
cd "C:\Users\%username%\AppData\Local\Google\lollo"
echo %data_vers%>"data_def.inf"

set /p vers=<"C:\Users\%username%\AppData\Local\Google\lollo\data_def.inf"
set /p data_vers=<"C:\Users\%username%\AppData\Local\Google\lollo\data_vers.inf"

if %vers%==%data_vers% (goto noagg) else (goto aggsi)

exit



:set_variablili
set /p data_vers=<"C:\Users\%username%\AppData\Local\Google\lollo\data_vers.inf"
set /p data_def=<"C:\Users\%username%\AppData\Local\Google\lollo\data_def.inf"
goto inizio





:a
cd "C:\Users\%username%\AppData\Local\Google\lollo"
curl http://lollo1344.altervista.org/data_vers.inf --output "data_vers.inf"
goto ver2




:noagg
cls
echo non ci sono aggirnamenti disponibili
timeout /t 3 /nobreak > NUL
goto verify

:aggsi
cls
echo nuovo aggirnamento disponibile !!!
echo.
echo.
echo per installarlo premi 1 
echo.
echo.
echo per saltare la versione premi 2
echo.
choice /c 12 /n /m "1 o 2?: "
cls

if %errorlevel%==1 goto go
if %errorlevel%==2 goto inizio


:go
REM estrai
cd "C:\Users\%username%\AppData\Local\Google\lollo"
curl http://lollo1344.altervista.org/data_vers.inf --output "data_vers.inf"
timeout /t 1 /nobreak > NUL

md "C:\Users\%username%\AppData\Local\test connessione"


cd C:\Users\%username%\Desktop
md temp

cd C:\Users\%username%\Desktop\temp
curl https://codeload.github.com/lollodog/temsd/zip/refs/heads/main --output "test connessione agg.zip"
timeout /t 1 /nobreak > NUL

cd C:\Users\%username%\Desktop\temp

if exist "%ProgramFiles%\7-Zip\7z.exe" set APP="%ProgramFiles%\7-Zip\7z.exe"
if exist "%ProgramFiles(x86)%\7-Zip\7z.exe" set APP="%ProgramFiles(x86)%\7-Zip\7z.exe"
%APP% x -spe *.zip -oc:*

xcopy "C:\Users\%username%\Desktop\temp\test connessione agg\test-connessione-agg-main\testa connessione.exe"  "C:\Users\%username%\AppData\Local\test connessione" /d /s /y /i /j /Q

timeout /t 1 /nobreak > NUL


timeout /t 1 /nobreak > NUL

del "C:\Users\%username%\Desktop\test connessione" /s /q /f
timeout /t 1 /nobreak > NUL
cd C:\Users\%username%\Desktop
mklink "test connessione"  "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe"

rmdir "C:\Users\%username%\\Desktop\temp" /q /s

goto inizio



:no
mkdir "C:\Users\%username%\AppData\Local\Google\lollo"
cd "C:\Users\%username%\AppData\Local\Google\lollo"
echo 1.0.0>"data_def.inf"
echo 1.0.0>"data_vers.inf"
goto verify



mode 128,30
:inizio
if exist "C:\Users\%username%\AppData\Local\default.txt" (goto 1) else (goto crea)


:1
title home  vers.%data_vers%
cls



set /p color=<"C:\Users\%username%\AppData\Local\defaultcolor.txt"
color %color%
cls
cd C:\Windows\System32
echo.
set /p predef=<"C:\Users\%username%\AppData\Local\default.txt"
set /p byte=<"C:\Users\%username%\AppData\Local\defaultbyte.txt"

echo                     premi invio senza digitare niente per testare le impostazioni predefinite seguenti:
echo.
echo.
echo.
echo.
echo  %predef% (DNS predefinito)
echo.
echo  %byte% (byte predefiniti)
echo.
echo  colore attuale %color%
echo.
echo  scrivi "imp" per cambiare le impostazioni 
echo.
echo  scrivi "avanz" per passare alla modalita di tracciamento 
echo.
echo  scrivi "ver" per verificare se ci sono aggiornamenti disponibili
echo.
echo  scrivi "loc" per localizzare un indirizzo ip
echo.
echo  scrivi "info" per vedere le informazioni del programma
echo.
set /p "ip=inserisci il tuo indizizzo ip manualmente o premi invio > "
if %errorlevel%==1 (goto err) else (goto predef)





:err
set /p predef=<"C:\Users\%username%\AppData\Local\default.txt"

set ip=%predef%
goto predef


:predef
if %ip%==info goto info
if %ip%==loc goto traccia
if %ip%==disinst goto disinst
if %ip%==ver goto a
if %ip%==avanz goto avanz
if %ip%==imp goto cambia
set /p %byte%=<"C:\Users\%username%\AppData\Local\defaultbyte.txt"
ping %IP% -t100000 -l %byte%

timeout /t 1 /nobreak > NUL
goto predef

:cambia
cls
echo.
echo         impostazioni 
echo.
echo premi "1" per cambiare il dns 
echo.
echo premi "2" per cambiare il numero di byte
echo.
echo premi "3" reimpostare i valori predefiniti
echo.
echo premi "4" per cambiare il colore
echo.
echo premi "5" per tornare alla home
echo.
choice /c 12345 /n /m "1 2 3 4 5 ? : "
cls

if %errorlevel%==1 goto dns
if %errorlevel%==2 goto byte
if %errorlevel%==3 goto default
if %errorlevel%==4 goto color
if %errorlevel%==5 goto 1

:dns
echo.
echo scrivi \ e premi invio per tornare alle impostazioni
echo.
set /p dns=inserisci nuovo DNS predefinito  
if %dns%==\ (goto cambia) else (goto cont) 
pause>nul
:cont
echo %dns%>"C:\Users\%username%\AppData\Local\default.txt"
goto 1


:byte
cls
echo.
echo scrivi \ e premi invio per tornare alle impostazioni
echo.
set /p byte=inserisci un numero da 10 a 65500    
if %byte%==\ (goto cambia) else (goto cont1) 
pause>nul
:cont1
if %byte% gtr 65500 (goto byte)
if %byte% lss 10 (goto byte)
echo %byte%>"C:\Users\%username%\AppData\Local\defaultbyte.txt"
goto 1



:color
set /p color=<"C:\Users\%username%\AppData\Local\defaultcolor.txt"
color %color%
echo.
echo premi "1" per cambiare colore in nero su bianco
echo.
echo premi "2" per cambiare colore in bianco su viola
echo.
echo premi "3" per cambiare colore in nero su verde
echo.
echo premi "4" per cambiare colore in rosso su nero
echo.
echo premi "5" per tornare alla home
echo.
choice /c 12345 /n /m "1 2 3 4 5 ? : "
cls



if %errorlevel%==1 goto rb

if %errorlevel%==2 goto bv

if %errorlevel%==3 goto nv

if %errorlevel%==4 goto rn

if %errorlevel%==5 goto 1


:rb
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.txt"
goto color
:bv
echo f5>"C:\Users\%username%\AppData\Local\defaultcolor.txt"
goto color
:nv
echo 02>"C:\Users\%username%\AppData\Local\defaultcolor.txt"
goto color
:rn
echo 0c>"C:\Users\%username%\AppData\Local\defaultcolor.txt"
goto color








:crea
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.txt"
echo 192.168.1.1>"C:\Users\%username%\AppData\Local\default.txt"
echo 32>"C:\Users\%username%\AppData\Local\defaultbyte.txt"
goto 1

:default
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.txt"
echo 192.168.1.1>"C:\Users\%username%\AppData\Local\default.txt"
echo 32>"C:\Users\%username%\AppData\Local\defaultbyte.txt"
goto 1




:avanz
cls
set /p "ip2=inserisci indizizzo ip da tracciare > "

pathping %ip2%
echo.
cls
echo premi un tasto per continuare...
pause>nul
goto 1




:disinst
del "C:\Users\%username%\AppData\Local\Google\lollo\data_def.inf" /s /q /f
del "C:\Users\%username%\AppData\Local\Google\lollo\data_vers.inf" /s /q /f
rmdir "C:\Users\%username%\AppData\Local\Google\lollo" /s /q
timeout /t 1 /nobreak > NUL
rmdir "C:\Users\%username%\AppData\Local\test connessione" /s /q
del "C:\Users\%username%\Desktop\test connessione" /s /q /f
del "C:\Users\%username%\Desktop\test connessione agg.zip" /s /q /f
exit







:traccia
cls
echo.
echo scrivi \ e premi invio per tornare alla scheramata home
echo.
set /p "ins=inserisci indizizzo ip da localizzare > "
if %ins%==\ (goto inizio) else (goto cont2) 
:cont2
explorer "https://www.opentracker.net/feature/ip-tracker?ip=%ins%"
goto inizio



:info
cls
echo versione del programma attuale: %data_vers% 
echo.
echo directory del programma (dopo averlo aggiornato) 
echo.
echo "C:\Users\%username%\AppData\Local\test connessione"
echo.
echo posizione file di memoria (.inf) in:
echo.
echo "C:\Users\%username%\AppData\Local\Google\lollo"
echo.
echo codice sorgente open source in: https://github.com/lollodog/souce-code-test-connessione
echo.
echo sviluppatore: Lorenzo Pucci 
echo.
echo grazie per aver utilizzato questo programma
echo.
echo questo programma e in continua evoluzione
echo.
echo premi un tasto per continuare
echo.
pause>nul
goto inizio
