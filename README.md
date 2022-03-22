@echo off

if exist "C:\Users\%username%\Desktop\language.txt" (goto verifica) else (goto crealingua)

:crealingua

echo it >"C:\Users\%username%\Desktop\language.txt"

:verifica

set /p language=<"C:\Users\%username%\Desktop\language.txt"

if %language%==it goto it

if %language%==en goto en

pause>nul

:it

if exist "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" (goto inizzissimo) else (goto collegamanto)

:collegamanto
cd "C:\Users\%username%\Desktop"
mklink "test connessione" "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe"

goto inizzissimo

:inizzissimo

if exist "C:\Users\%username%\AppData\Local\test connessione\data_def.inf" (goto set_variablili) else (goto no)






:ver2
cd "C:\Users\%username%\AppData\Local\test connessione"
echo %data_vers%>"data_def.inf"

set /p vers=<"C:\Users\%username%\AppData\Local\test connessione\data_def.inf"
set /p data_vers=<"C:\Users\%username%\AppData\Local\test connessione\data_vers.inf"

if %vers%==%data_vers% (goto noagg) else (goto aggsi)

exit



:set_variablili
set /p data_vers=<"C:\Users\%username%\AppData\Local\test connessione\data_vers.inf"
set /p data_def=<"C:\Users\%username%\AppData\Local\test connessione\data_def.inf"
goto inizio





:a
cd "C:\Users\%username%\AppData\Local\test connessione"
curl http://lollo1344.altervista.org/data_vers.inf --output "data_vers.inf"
goto ver2



:noagg
cls
echo non ci sono aggirnamenti disponibili al momento 
echo.
echo riprova piu tardi o contatta lo sviluppatore per sapere quando verra rilasciato un aggiornamento
echo.
echo e-mail sviluppatore : loriciappo21@gmail.com
echo.
timeout /t 9 /nobreak > NUL
goto collegamanto

:aggsi
cls
echo nuovo aggirnamento disponibile !!!
echo.
echo.
echo  premi 1 per installarlo
echo.
echo.
echo  premi 2 per saltare la versione
echo.
choice /c 12 /n /m "1 o 2 ?: "
cls

if %errorlevel%==1 goto go
if %errorlevel%==2 goto inizio
pause>nul

:go
REM estrai
cd "C:\Users\%username%\AppData\Local\test connessione"
curl http://lollo1344.altervista.org/data_vers.inf --output "data_vers.inf"
timeout /t 1 /nobreak > NUL

md "C:\Users\%username%\AppData\Local\test connessione"


md "C:\Users\%username%\Desktop\temp"

cd C:\Users\%username%\Desktop\temp
curl https://codeload.github.com/lollodog/temsd/zip/refs/heads/main --output "test connessione agg.zip"
timeout /t 1 /nobreak > NUL

cd C:\Users\%username%\Desktop\temp

if exist "%ProgramFiles%\7-Zip\7z.exe" set APP="%ProgramFiles%\7-Zip\7z.exe"
if exist "%ProgramFiles(x86)%\7-Zip\7z.exe" set APP="%ProgramFiles(x86)%\7-Zip\7z.exe"
%APP% x -spe *.zip -oc:*

cd C:\Users\%username%\Desktop\temp

echo @ echo off>"GUP.bat"
echo del "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" /s /q /f>>"GUP.bat"
echo xcopy "C:\Users\%username%\Desktop\temp\test connessione agg\test-connessione-agg-main\testa connessione.exe"  "C:\Users\%username%\AppData\Local\test connessione" /s /q /y>>"GUP.bat"
echo explorer "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe">>"GUP.bat"
echo rmdir "C:\Users\%username%\Desktop\temp" /s /q>>"GUP.bat"

explorer "C:\Users\%username%\Desktop\temp\GUP.bat"
exit

goto inizio



:no
md "C:\Users\%username%\AppData\Local\test connessione"
cd "C:\Users\%username%\AppData\Local\test connessione"
echo 1.0.0>"data_def.inf"
echo 1.0.0>"data_vers.inf"
goto inizzissimo



mode 128,30
:inizio
if exist "C:\Users\%username%\AppData\Local\default.ini" (goto 1) else (goto crea)

:1


mode 138,30
title home  vers.%data_vers%
cls



set /p color=<"C:\Users\%username%\AppData\Local\defaultcolor.ini"
color %color%
cls
cd C:\Windows\System32
echo.
set /p predef=<"C:\Users\%username%\AppData\Local\default.ini"
set /p byte=<"C:\Users\%username%\AppData\Local\defaultbyte.ini"



if exist "C:\Users\%username%\Desktop\start.inf" (goto esiste) else (goto bypass)

:esiste

set /p start=<"C:\Users\%username%\Desktop\start.inf"

if %start%==1 goto autoavvio

if %start%==0 goto bypass




:bypass

echo                          premi invio senza digitare niente per testare %predef% con %byte% byte
echo.
echo.
echo questa e una versione e in test e si potrebbero rilevare alcuni bug
echo.
echo segnala eventuali errori a: loriciappo21@gmail.com
echo.
echo.
echo.
echo ip predefinito: "%predef%"
echo.
echo byte predefiniti: "%byte%"
echo.
echo versione del programma %data_vers%
echo.
echo.
echo  scrivi "imp" per cambiare le impostazioni 
echo.
echo  scrivi "avanz" per passare alla modalita di tracciamento 
echo.
echo  scrivi "ver" per verificare se ci sono aggiornamenti disponibili
echo.
echo  scrivi "loc" per localizzare un indirizzo ip
echo.
echo  scrivi "see" per visualizzare gli indirizzi ip attivi su questo pc
echo.
echo  scrivi "info" per vedere le informazioni del programma
echo.
echo.
set /p "ip=inserisci il tuo indizizzo ip manualmente o premi invio > "
if %errorlevel%==1 (goto err) else (goto predef)


:autoavvio
cls
echo per avviare normalmente elimina il file sul desktop che si chiama "start"
echo.
echo o al posto di 1 inserisci 0
echo.
set /p predef=<"C:\Users\%username%\AppData\Local\default.ini"



set ip=%predef%
set /p %byte%=<"C:\Users\%username%\AppData\Local\defaultbyte.ini"
ping %IP% -t100000 -l %byte%
goto 1



:err
set /p predef=<"C:\Users\%username%\AppData\Local\default.ini"

set ip=%predef%
goto predef


:predef
if %ip%==info goto info
if %ip%==see goto see
if %ip%==loc goto traccia
if %ip%==ver goto a
if %ip%==avanz goto avanz
if %ip%==imp goto cambia
set /p %byte%=<"C:\Users\%username%\AppData\Local\defaultbyte.ini"
ping %IP% -t100000 -l %byte%



timeout /t 1 /nobreak > NUL
goto predef

:cambia
mode 120,36
cls
echo.
echo               IMPOSTAZIONI
echo.
echo =============================================
echo.
echo premi "1" per cambiare il dns 
echo.
echo premi "2" per cambiare il numero di byte
echo.
echo premi "3" reimpostare i valori predefiniti
echo.
echo =============================================
echo.
echo premi "4" per cambiare il colore
echo.
echo =================================================
echo.
echo premi "5" per disinstallare il programma e i dati 
echo.
echo =================================================
echo.
echo premi "6" per esportare le preferenze
echo.
echo premi "7" per importare le preferenze
echo.
echo =======================================================
echo.
echo premi "8" per riavviare il programma
echo.
echo premi "9" autoavvia il test connessione all' apertura
echo.
echo =======================================================
echo.
echo premi "h" per tornare alla home
echo.
echo =============================================
echo.
echo.
choice /c 123456789h /n /m "1 2 3 4 5 6 7 8 9 h ? : "
cls

if %errorlevel%==1 goto dns
if %errorlevel%==2 goto byte
if %errorlevel%==3 goto default
if %errorlevel%==4 goto color
if %errorlevel%==5 goto disinst
if %errorlevel%==6 goto esport
if %errorlevel%==7 goto import
if %errorlevel%==8 goto riavvia
if %errorlevel%==9 goto open
if %errorlevel%==10 goto 1

:dns
echo.
echo scrivi \ e premi invio per tornare alle impostazioni
echo.
set /p dns=inserisci nuovo DNS predefinito  
if %dns%==\ (goto cambia) else (goto cont) 
pause>nul
:cont
echo %dns%>"C:\Users\%username%\AppData\Local\default.ini"
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
echo %byte%>"C:\Users\%username%\AppData\Local\defaultbyte.ini"
goto 1



:color
set /p color=<"C:\Users\%username%\AppData\Local\defaultcolor.ini"
color %color%
echo.
echo premi "1" per cambiare colore in bianco su nero
echo.
echo premi "2" per cambiare colore in bianco su viola
echo.
echo premi "3" per cambiare colore in verde su nero
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
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color
:bv
echo f5>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color
:nv
echo 02>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color
:rn
echo 0c>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color








:crea
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
echo 192.168.1.1>"C:\Users\%username%\AppData\Local\default.ini"
echo 32>"C:\Users\%username%\AppData\Local\defaultbyte.ini"
goto 1

:default
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
echo 192.168.1.1>"C:\Users\%username%\AppData\Local\default.ini"
echo 32>"C:\Users\%username%\AppData\Local\defaultbyte.ini"
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
del "C:\Users\%username%\AppData\Local\test connessione\data_def.inf" /s /q /f
del "C:\Users\%username%\AppData\Local\test connessione\data_vers.inf" /s /q /f
del "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" /s /q /f
rmdir "C:\Users\%username%\AppData\Local\test connessione" /s /q
timeout /t 1 /nobreak > NUL
rmdir "C:\Users\%username%\AppData\Local\test connessione" /s /q
del "C:\Users\%username%\Desktop\test connessione" /s /q /f
del "C:\Users\%username%\Desktop\test connessione agg.zip" /s /q /f
del "C:\Users\%username%\AppData\Local\test connessione\riavvia.bat" /s /q /f
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
echo directory del programma (dopo averlo aggiornato) : "C:\Users\%username%\AppData\Local\test connessione"
echo.
echo posizione file di memoria (.inf) in: "C:\Users\%username%\AppData\Local\test connessione"
echo.
echo codice sorgente open source in: https://github.com/lollodog/souce-code-test-connessione
echo.
echo sviluppatore: Lorenzo Pucci 
echo.
echo e-mail sviluppatore loriciappo21@gmail.com
echo.
echo grazie per aver utilizzato questo programma
echo.
echo premi un tasto per continuare
echo.
pause>nul
cls
color f
echo =======================================================================
echo.
echo                   novita della versione %data_vers%
echo.
echo aggiunta funzione di autoavvio del test connessione 
echo.
echo risoluzione di bug
echo.
echo aggiunte 2 lingue
echo.
echo =======================================================================
echo.
echo premi un tasto per continuare
echo.
pause>nul
goto inizio




:esport
cls
md "C:\Users\%username%\Desktop\export-preferences"
xcopy "C:\Users\%username%\AppData\Local\default.ini"  "C:\Users\%username%\Desktop\export-preferences" /Q /Y
xcopy "C:\Users\%username%\AppData\Local\defaultbyte.ini"  "C:\Users\%username%\Desktop\export-preferences" /Q /Y
xcopy "C:\Users\%username%\AppData\Local\defaultcolor.ini"  "C:\Users\%username%\Desktop\export-preferences" /Q /Y 
cls
echo preferenze esportate con successo
timeout /t 2 /nobreak > NUL
goto 1



:import
cls
echo premi invio senza digitare niente per selezionare il desktop
echo.
echo                                 nota bene !!!
echo.
echo se inserisci il percorso sbagliato l'importazione delle preferenze non funzionera
echo.
echo.
set /p "percorso=inserisci percorso della cartella delle preferenze o premi invio > "
if %errorlevel%==1 (goto predef2) else (goto import1)

echo.

:import1

xcopy %percorso%  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy %percorso%  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy %percorso%  "C:\Users\%username%\AppData\Local" /Q /Y >nul
cls
echo preferenze importate con successo
 
timeout /t 2 /nobreak > NUL
goto 1




:predef2

if not exist "C:\Users\%username%\Desktop\export-preferences" (goto preferenzerr)
xcopy "C:\Users\%username%\Desktop\export-preferences\default.ini"  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy "C:\Users\%username%\Desktop\export-preferences\defaultbyte.ini"  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy "C:\Users\%username%\Desktop\export-preferences\defaultcolor.ini"  "C:\Users\%username%\AppData\Local" /Q /Y >nul


timeout /t 1 /nobreak > NUL
rmdir "C:\Users\%username%\Desktop\export-preferences" /s /q 
cls
echo preferenze importate con successo
timeout /t 2 /nobreak > NUL
goto 1


:preferenzerr
cls
echo impossibile trovare la cartella export-preferences in: "C:\Users\%username%\Desktop\export-preferences"
timeout /t 5 /nobreak > NUL
goto 1


:see
cls
netstat
echo.
echo premi un tasto per continuare...
echo.
pause>nul
goto 1

:riavvia

if exist "C:\Users\%username%\AppData\Local\test connessione\riavvia.bat" (goto esegui) else (goto creaesegui)

:creaesegui

echo @echo off>"C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"
echo explorer "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" >>"C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"
echo exit >>"C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"

goto riavvia

:esegui

explorer "C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"
exit




:open
echo 1 >"C:\Users\%username%\Desktop\start.inf"
goto collegamanto




::========================inizio lingua inglese==================================================================================




:en

if exist "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" (goto inizzissimo) else (goto collegamanto)

:collegamanto
cd "C:\Users\%username%\Desktop"
mklink "test connection" "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe"

goto inizzissimo

:inizzissimo

if exist "C:\Users\%username%\AppData\Local\test connessione\data_def.inf" (goto set_variablili) else (goto no)






:ver2
cd "C:\Users\%username%\AppData\Local\test connessione"
echo %data_vers%>"data_def.inf"

set /p vers=<"C:\Users\%username%\AppData\Local\test connessione\data_def.inf"
set /p data_vers=<"C:\Users\%username%\AppData\Local\test connessione\data_vers.inf"

if %vers%==%data_vers% (goto noagg) else (goto aggsi)

exit



:set_variablili
set /p data_vers=<"C:\Users\%username%\AppData\Local\test connessione\data_vers.inf"
set /p data_def=<"C:\Users\%username%\AppData\Local\test connessione\data_def.inf"
goto inizio





:a
cd "C:\Users\%username%\AppData\Local\test connessione"
curl http://lollo1344.altervista.org/data_vers.inf --output "data_vers.inf"
goto ver2



:noagg
cls
echo there are no updates available at the moment 
echo.
echo try again later or contact the developer to find out when an update will be released
echo.
echo developer e-mail : loriciappo21@gmail.com
echo.
timeout /t 9 /nobreak > NUL
goto collegamanto

:aggsi
cls
echo new upgrade available !!!
echo.
echo.
echo  Press "1" to install it
echo.
echo.
echo  Press "2" to skip the version
echo.
choice /c 12 /n /m "1 o 2 ?: "
cls

if %errorlevel%==1 goto go
if %errorlevel%==2 goto inizio
pause>nul

:go
REM estrai
cd "C:\Users\%username%\AppData\Local\test connessione"
curl http://lollo1344.altervista.org/data_vers.inf --output "data_vers.inf"
timeout /t 1 /nobreak > NUL

md "C:\Users\%username%\AppData\Local\test connessione"


md "C:\Users\%username%\Desktop\temp"

cd C:\Users\%username%\Desktop\temp
curl https://codeload.github.com/lollodog/temsd/zip/refs/heads/main --output "test connessione agg.zip"
timeout /t 1 /nobreak > NUL

cd C:\Users\%username%\Desktop\temp

if exist "%ProgramFiles%\7-Zip\7z.exe" set APP="%ProgramFiles%\7-Zip\7z.exe"
if exist "%ProgramFiles(x86)%\7-Zip\7z.exe" set APP="%ProgramFiles(x86)%\7-Zip\7z.exe"
%APP% x -spe *.zip -oc:*

cd C:\Users\%username%\Desktop\temp

echo @ echo off>"GUP.bat"
echo del "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" /s /q /f>>"GUP.bat"
echo xcopy "C:\Users\%username%\Desktop\temp\test connessione agg\test-connessione-agg-main\testa connessione.exe"  "C:\Users\%username%\AppData\Local\test connessione" /s /q /y>>"GUP.bat"
echo explorer "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe">>"GUP.bat"
echo rmdir "C:\Users\%username%\Desktop\temp" /s /q>>"GUP.bat"

explorer "C:\Users\%username%\Desktop\temp\GUP.bat"
exit

goto inizio



:no
md "C:\Users\%username%\AppData\Local\test connessione"
cd "C:\Users\%username%\AppData\Local\test connessione"
echo 1.0.0>"data_def.inf"
echo 1.0.0>"data_vers.inf"
goto inizzissimo



mode 128,30
:inizio
if exist "C:\Users\%username%\AppData\Local\default.ini" (goto 1) else (goto crea)

:1


mode 138,30
title home  vers.%data_vers%
cls



set /p color=<"C:\Users\%username%\AppData\Local\defaultcolor.ini"
color %color%
cls
cd C:\Windows\System32
echo.
set /p predef=<"C:\Users\%username%\AppData\Local\default.ini"
set /p byte=<"C:\Users\%username%\AppData\Local\defaultbyte.ini"



if exist "C:\Users\%username%\Desktop\start.inf" (goto esiste) else (goto bypass)

:esiste

set /p start=<"C:\Users\%username%\Desktop\start.inf"

if %start%==1 goto autoavvio

if %start%==0 goto bypass




:bypass

echo                          press enter without typing anything to test %predef% with %byte% byte
echo.
echo.
echo this is a version and in test and you may detect some bugs
echo.
echo report any errors to: loriciappo21@gmail.com

echo.
echo.
echo.
echo default ip: "%predef%"
echo.
echo default bytes: "%byte%"
echo.
echo program version %data_vers%
echo.
echo.
echo  type "imp" to change the settings
echo.
echo  type "advance" to switch to tracking mode
echo.
echo  type "ver" to check for updates available
echo.
echo  type "loc" to locate an ip address
echo.
echo  type "see" to view the active IP addresses on this pc
echo.
echo  type "info" to see the program information
echo.
echo.
set /p "ip=enter your ip address manually or hit enter > "
if %errorlevel%==1 (goto err) else (goto predef)


:autoavvio
cls
echo to start normally delete the file on the desktop called "start"
echo.
echo or instead of 1 enter 0
echo.
set /p predef=<"C:\Users\%username%\AppData\Local\default.ini"



set ip=%predef%
set /p %byte%=<"C:\Users\%username%\AppData\Local\defaultbyte.ini"
ping %IP% -t100000 -l %byte%
goto 1



:err
set /p predef=<"C:\Users\%username%\AppData\Local\default.ini"

set ip=%predef%
goto predef


:predef
if %ip%==info goto info
if %ip%==see goto see
if %ip%==loc goto traccia
if %ip%==ver goto a
if %ip%==advance goto avanz
if %ip%==imp goto cambia
set /p %byte%=<"C:\Users\%username%\AppData\Local\defaultbyte.ini"
ping %IP% -t100000 -l %byte%



timeout /t 1 /nobreak > NUL
goto predef

:cambia
mode 120,36
cls
echo.
echo               SETTINGS
echo.
echo =============================================
echo.
echo press "1" to change the dns
echo.
echo press "2" to change the number of bytes
echo.
echo press "3" reset to default values
echo.
echo =============================================
echo.
echo press "4" to change the color
echo.
echo =================================================
echo.
echo press "5" to uninstall the program and data 
echo.
echo =================================================
echo.
echo press "6" to export preferences
echo.
echo press "7" to import preferences
echo.
echo =======================================================
echo.
echo press "8" to restart the program
echo.
echo press "9" auto-start connection test on opening
echo.
echo =======================================================
echo.
echo press "h" to return to home
echo.
echo =============================================
echo.
echo.
choice /c 123456789h /n /m "1 2 3 4 5 6 7 8 9 h ? : "
cls

if %errorlevel%==1 goto dns
if %errorlevel%==2 goto byte
if %errorlevel%==3 goto default
if %errorlevel%==4 goto color
if %errorlevel%==5 goto disinst
if %errorlevel%==6 goto esport
if %errorlevel%==7 goto import
if %errorlevel%==8 goto riavvia
if %errorlevel%==9 goto open
if %errorlevel%==10 goto 1

:dns
echo.
echo type \ and press enter to return to settings
echo.
set /p dns=enter new default DNS  
if %dns%==\ (goto cambia) else (goto cont) 
pause>nul
:cont
echo %dns%>"C:\Users\%username%\AppData\Local\default.ini"
goto 1


:byte
cls
echo.
echo type \ and press enter to return to settings
echo.
set /p byte=enter a number from 10 to 65500    
if %byte%==\ (goto cambia) else (goto cont1) 
pause>nul
:cont1
if %byte% gtr 65500 (goto byte)
if %byte% lss 10 (goto byte)
echo %byte%>"C:\Users\%username%\AppData\Local\defaultbyte.ini"
goto 1



:color
set /p color=<"C:\Users\%username%\AppData\Local\defaultcolor.ini"
color %color%
echo.
echo press "1" to change color to white on black
echo.
echo press "2" to change color to white to purple
echo.
echo press "3" to change color to green on black
echo.
echo press "4" to change color to red to black
echo.
echo press "5" to return to home
echo.
choice /c 12345 /n /m "1 2 3 4 5 ? : "
cls



if %errorlevel%==1 goto rb

if %errorlevel%==2 goto bv

if %errorlevel%==3 goto nv

if %errorlevel%==4 goto rn

if %errorlevel%==5 goto 1


:rb
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color
:bv
echo f5>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color
:nv
echo 02>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color
:rn
echo 0c>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
goto color








:crea
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
echo 192.168.1.1>"C:\Users\%username%\AppData\Local\default.ini"
echo 32>"C:\Users\%username%\AppData\Local\defaultbyte.ini"
goto 1

:default
echo f>"C:\Users\%username%\AppData\Local\defaultcolor.ini"
echo 192.168.1.1>"C:\Users\%username%\AppData\Local\default.ini"
echo 32>"C:\Users\%username%\AppData\Local\defaultbyte.ini"
goto 1




:avanz
cls
set /p "ip2=enter ip address to trace > "

pathping %ip2%
echo.
cls
echo press any key to continue ...
pause>nul
goto 1




:disinst
del "C:\Users\%username%\AppData\Local\test connessione\data_def.inf" /s /q /f
del "C:\Users\%username%\AppData\Local\test connessione\data_vers.inf" /s /q /f
del "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" /s /q /f
rmdir "C:\Users\%username%\AppData\Local\test connessione" /s /q
timeout /t 1 /nobreak > NUL
rmdir "C:\Users\%username%\AppData\Local\test connessione" /s /q
del "C:\Users\%username%\Desktop\test connessione" /s /q /f
del "C:\Users\%username%\Desktop\test connessione agg.zip" /s /q /f
del "C:\Users\%username%\AppData\Local\test connessione\riavvia.bat" /s /q /f
exit







:traccia
cls
echo.
echo type \ and press enter to return to the home screen
echo.
set /p "ins=enter ip address to locate > "
if %ins%==\ (goto inizio) else (goto cont2) 
:cont2
explorer "https://www.opentracker.net/feature/ip-tracker?ip=%ins%"
goto inizio



:info
cls
echo current program version: %data_vers% 
echo.
echo program directory (after updating it) : "C:\Users\%username%\AppData\Local\test connessione"
echo.
echo memory file location (.inf) in: "C:\Users\%username%\AppData\Local\test connessione"
echo.
echo open source source code in: https://github.com/lollodog/souce-code-test-connessione
echo.
echo developer: Lorenzo Pucci 
echo.
echo e-mail developer loriciappo21@gmail.com
echo.
echo thanks for using this program
echo.
echo press any key to continue ...
echo.
pause>nul
cls
color f
echo =======================================================================
echo.
echo                   new in version %data_vers%
echo.
echo added function of auto-start of the connection test 
echo.
echo bug fixes
echo.
echo added 2 languages
echo.
echo =======================================================================
echo.
echo press any key to continue...
echo.
pause>nul
goto inizio




:esport
cls
md "C:\Users\%username%\Desktop\export-preferences"
xcopy "C:\Users\%username%\AppData\Local\default.ini"  "C:\Users\%username%\Desktop\export-preferences" /Q /Y
xcopy "C:\Users\%username%\AppData\Local\defaultbyte.ini"  "C:\Users\%username%\Desktop\export-preferences" /Q /Y
xcopy "C:\Users\%username%\AppData\Local\defaultcolor.ini"  "C:\Users\%username%\Desktop\export-preferences" /Q /Y 
cls
echo preferenze esportate con successo
timeout /t 2 /nobreak > NUL
goto 1



:import
cls
echo hit enter without typing anything to select the desktop
echo.
echo                                 please note !!!
echo.
echo if you enter the wrong path, importing preferences will not work
echo.
echo.
set /p "percorso=enter path to the preferences folder or press enter > "
if %errorlevel%==1 (goto predef2) else (goto import1)

echo.

:import1

xcopy %percorso%  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy %percorso%  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy %percorso%  "C:\Users\%username%\AppData\Local" /Q /Y >nul
cls
echo preferences imported successfully
 
timeout /t 2 /nobreak > NUL
goto 1




:predef2

if not exist "C:\Users\%username%\Desktop\export-preferences" (goto preferenzerr)
xcopy "C:\Users\%username%\Desktop\export-preferences\default.ini"  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy "C:\Users\%username%\Desktop\export-preferences\defaultbyte.ini"  "C:\Users\%username%\AppData\Local" /Q /Y >nul
xcopy "C:\Users\%username%\Desktop\export-preferences\defaultcolor.ini"  "C:\Users\%username%\AppData\Local" /Q /Y >nul


timeout /t 1 /nobreak > NUL
rmdir "C:\Users\%username%\Desktop\export-preferences" /s /q 
cls
echo preferences imported successfully
timeout /t 2 /nobreak > NUL
goto 1


:preferenzerr
cls
echo unable to find export-preferences folder in: "C:\Users\%username%\Desktop\export-preferences"
timeout /t 5 /nobreak > NUL
goto 1


:see
cls
netstat
echo.
echo press any key to continue ...
echo.
pause>nul
goto 1

:riavvia

if exist "C:\Users\%username%\AppData\Local\test connessione\riavvia.bat" (goto esegui) else (goto creaesegui)

:creaesegui

echo @echo off>"C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"
echo explorer "C:\Users\%username%\AppData\Local\test connessione\testa connessione.exe" >>"C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"
echo exit >>"C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"

goto riavvia

:esegui

explorer "C:\Users\%username%\AppData\Local\test connessione\riavvia.bat"
exit




:open
echo 1 >"C:\Users\%username%\Desktop\start.inf"
goto collegamanto


