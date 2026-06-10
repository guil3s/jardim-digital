---
{"dg-publish":true,"permalink":"/desenvolvimento/backupator-uma-brincadeira-para-praticar-dos/","dg-note-properties":{}}
---

Há alguns anos atrás atrás comecei a escrever um script para automatizar o Backup de alguns arquivos do meu notebook para meu hd externo.

Fiz todo o desenvolvimento em DOS, para praticar os códigos de script. Infelizmente não consegui me furtar de usar powershell em alguns momentos do código, como você poderá perceber.

O script está funcional. Para mais praticidade, realizei o agendamento de tarefas, ferramenta nativa do windows, para que sempre que meu hd externo for conectado o script seja executado e faça o backup automaticamente, isso é bem interessante.

Ainda não subi o projeto para o github, quem sabe eu faça isso futuramente. Por enquanto, segue o código pra quem se interessar:

[Backupator.bat](https://drive.google.com/file/d/1ec1abEE-LtK8Ru2wXOPPlfJbWUFzqKdu/view?usp=drive_link)
[fazerbackup.bat](https://drive.google.com/file/d/1LHJhddvU-Nf_34oxZgAvHtCbLvG_7eNL/view?usp=drive_link)
[initscript.bat](https://drive.google.com/file/d/1F06lb5WBGvvR2CEImK--oeT45zYGodcY/view?usp=drive_link)
[logo.bat](https://drive.google.com/file/d/1bvK-4eSc0qXE3w84iUydCcQvhQkmz4Us/view?usp=drive_link)
[log.txt](https://drive.google.com/file/d/1h7f9-UHrgfQywbuAE2XAN3Vm9lY9xJO4/view?usp=drive_link)
[programados.txt](https://drive.google.com/file/d/1EyMRB84QYTYFNzOdp0eLcFnBDdSFNeDq/view?usp=drive_link)
[tarefa.xml](https://drive.google.com/file/d/1AyywtPgLi8RjeAfc8Pf91vNhARMca5OR/view?usp=drive_link)

Captura de tela do script em funcionamento:
![Pasted image 20260607211703.png](/img/user/Desenvolvimento/Pasted%20image%2020260607211703.png)

### Backupator.bat

```powershell

@echo off
color 0A
title <nul & title BACKUPATOR~~~ 0.0.1 >nul 2>&1
::mode con:cols=70 lines=1000
chcp 65001 >nul 2>&1

setlocal enabledelayedexpansion
set /a "off = 0"

cls
call logo.bat

::::::::::::::: ROTINA PRINCIPAL :::::::::::::::
 
:principal
	echo.
	::ping 127.0.0.1 -n 1 >nul 2>&1
	::echo    ██▒▒░░
	::ping 127.0.0.1 -n 1 >nul 2>&1
	::echo    █
	::ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ O que você deseja?
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ 
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ 1 - Ir para o início
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ 2 - Exibir backups programados
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ 3 - Programar novo backup
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ 4 - Fazer backups programados agora
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ 5 - Ajuda
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ 6 - Sair
	echo.
	color 74
	::set /p menu= ^> Digite a opção desejada: 
	choice /c:1234567 /n /t 30 /d 7 /m "█▒░  Selecione a opção desejada:"
	IF [%ERRORLEVEL%] == [1] (
		cls
		call logo.bat )
	IF [%ERRORLEVEL%] == [2] call :lertxt
	IF [%ERRORLEVEL%] == [3] call :novo
	IF [%ERRORLEVEL%] == [4] (
		cls
		call fazerbackup.bat )
	IF [%ERRORLEVEL%] == [5] call :ajuda
	IF [%ERRORLEVEL%] == [6] goto :sair
	IF [%ERRORLEVEL%] == [7] (
		set /a "off+=1"
		IF [!off!] GTR [10] ( goto :sair ) else (
			cls
			call logo.bat ))
	goto :principal >nul 2>&1
	


:: LÊ O TXT :: GRAVA NO ARRAY :: EXIBE NA TELA ::

:lertxt
	cls
	for /f "eol=# tokens=1-9 delims=? usebackq" %%I in (programados.txt) do (
		::call :array %%~I %%~J %%~fK %%~fL %%~M %%~N %%~O %%~P %%~Q
		set arq[%%~I].ID=%%~I
		set arq[%%~I].Ativo=%%~J
		set arq[%%~I].PastaOrigem=%%~fK
		set arq[%%~I].PastaDestino=%%~fL
		set arq[%%~I].Serial=%%~M
		set arq[%%~I].DataRegistro=%%~N
		set arq[%%~I].HoraRegistro=%%~O
		set arq[%%~I].DataUltimoBackup=%%~P
		set arq[%%~I].HoraUltimoBackup=%%~Q
	)
	set /a "y = 1" >nul 2>&1
	cls
	:exibe
	if defined arq[%y%].ID (
		if [%y%] == [1] (
			call echo.
			call echo    █ SÃO OS BACKUPS PROGRAMADOS: )
		call echo.
		call echo    █ ID:            %%arq[%y%].ID%%
		call echo    ▒ Ativo:         %%arq[%y%].Ativo%%
		call echo    ▒ ORIGEM:        %%arq[%y%].PastaOrigem%%
		call echo    ▒ DESTINO:       %%arq[%y%].PastaDestino%%
		call echo    ░ SERIAL:        %%arq[%y%].Serial%%
		call echo    ░ ATIVO DESDE:   %%arq[%y%].DataRegistro%% %%arq[%y%].HoraRegistro%%
		call echo    ░ ÚLTIMO BACKUP: %%arq[%y%].DataUltimoBackup%% %%arq[%y%].HoraUltimoBackup%%
		set /a "y+=1"
		goto :exibe >nul 2>&1 ) else (
		if [%y%] == [1] (
			call echo.
			call echo    █ NÃO HÁ BACKUPS PROGRAMADOS. ) )
	exit /b
	::goto :principal >nul 2>&1

::::::::::::: PROGRAMAR NOVO :::::::::::::

:novo
	cls
	echo.
	echo    █ Escolha a pasta origem.
	set "psCommand="(new-object -COM 'Shell.Application')^.BrowseForFolder(0,'Escolha a pasta que deseja guardar.',0,0).self.path""
	set "psCommand="(new-object -COM 'Shell.Application')^.BrowseForFolder(0,'Escolha a pasta da origem.',0,0).self.path""
	for /f "usebackq delims=" %%I in (`powershell %psCommand%`) do set "pastaorigem="%%I""
	echo.
	echo    █ Escolha a pasta destino.
	set "psCommand="(new-object -COM 'Shell.Application')^.BrowseForFolder(0,'Escolha a pasta do destino.',0,0).self.path""
	for /f "usebackq delims=" %%I in (`powershell %psCommand%`) do set "pastadestino="%%I""
	setlocal enabledelayedexpansion
	IF [%pastaorigem%] == [] (
		echo.
		echo    █ ERRO: Você não selecionou a origem!
		echo.
			IF [%pastadestino%] == [] (
			echo    █ ERRO: Você não selecionou o destino!
			echo. )
		exit /b
	) else (
		echo.
		echo    ▒ Pasta Origem: %pastaorigem% )
	IF [%pastadestino%] == [] (
		echo.
		echo    █ ERRO: Você não selecionou o destino!
		echo.
		exit /b
	) else (
		echo.
		echo    ▒ Pasta Destino: %pastadestino% )
	IF [%pastadestino%] == [%pastaorigem%] (
		echo.
		echo    █ ERRO: A origem e o destino devem ser diferentes!
		echo.
		exit /b
	)

	::::: CONTA OS JÁ GRAVADOS NO TXT :::::
	set /a z=1 >nul 2>&1
	for /f "eol=# tokens=1-9 delims=? usebackq" %%I in (programados.txt) do (
		set /a z+=1
	)

	::::: ESTIPULA VARIAVEIS :::::
	set ativo=Sim
	set dataregistro=%date:~0,2%/%date:~3,2%/%date:~6,2%
	set horaregistro=%time:~0,2%h%time:~3,2%min%time:~6,2%seg
	set disco=%pastadestino:~1,2%
	set capturadisco="wmic logicaldisk get Caption,VolumeSerialNumber | find "%disco%""
	for /f "tokens=1,2" %%P in ( '%capturadisco%' ) do set "caption=%%~P" && set serial=%%~Q >nul 2>&1

	::::: GRAVA NO ARRAY :::::

	set arq[%z%].ID=%z%
	set arq[%z%].Ativo=%ativo%
	set arq[%z%].PastaOrigem=%pastaorigem%
	set arq[%z%].PastaDestino=%pastadestino%
	set arq[%z%].Serial=%serial%
	set arq[%z%].DataRegistro=%dataregistro%
	set arq[%z%].HoraRegistro=%horaregistro%
	set arq[%z%].DataUltimoBackup=00/00/0000
	set arq[%z%].HoraUltimoBackup=00h00min00seg

	::::: SALVA NO ARQUIVO :::::

	:::::call echo %%arq[%z%].ID%%?%%arq[%z%].Ativo%%?%%arq[%z%].PastaOrigem%%?%%arq[%z%].PastaDestino%%?%%arq[%z%].Serial%%?%%arq[%z%].DataRegistro%%?%%arq[%z%].HoraRegistro%%?%%arq[%z%].DataUltimoBackup%%?%%arq[%z%].HoraUltimoBackup%%>>programados.txt:::::
	:::::call echo. >>programados.txt
	(call echo %%arq[%z%].ID%%?%%arq[%z%].Ativo%%?%%arq[%z%].PastaOrigem%%?%%arq[%z%].PastaDestino%%?%%arq[%z%].Serial%%?%%arq[%z%].DataRegistro%%?%%arq[%z%].HoraRegistro%%?%%arq[%z%].DataUltimoBackup%%?%%arq[%z%].HoraUltimoBackup%%)>>programados.txt
	echo.
	echo    █ Instruções gravadas com sucesso!
	echo.
	exit /b

:ajuda
	cls
	echo.
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ Ajuda.
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    █ BACKUPATOR é um programa que automatiza seus backups.
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    ▒ Programe um novo backup, escolha o diretório de origem e de destino.
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    ▒ Faça a importação do arquivo "tarefa.xml"
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    ▒ no Agendador de Tarefas do Windows.
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    ░ Assim, toda vez que conetar sua mídia externa
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    ░ o backup será realizado automaticamente.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo.
	echo    ░ Deixe a preocupação de lado e nunca mais perca seus arquivos.
	echo.
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	set /p voltar=    █▒░  Aperte a tecla [ENTER] para voltar.
	cls
	call logo.bat
	exit /b	

:sair
	cls
	echo.
	echo             ▄▄▄▄    ▄▄▄       ▄████▄   ██ ▄█▀                    
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo            ▓█████▄ ▒████▄    ▒██▀ ▀█   ██▄█▒                     
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo            ▒██▒ ▄██▒██  ▀█▄  ▒▓█    ▄ ▓███▄░     
	ping 127.0.0.1 -n 1 >nul 2>&1                
	echo            ▒██░█▀  ░██▄▄▄▄██ ▒▓▓▄ ▄██▒▓██ █▄                     
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo            ░▓█  ▀█▓ ▓█   ▓██▒▒ ▓███▀ ░▒██▒ █▄                    
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo            ░▒▓███▀▒ ▒▒   ▓▒█░░ ░▒ ▒  ░▒ ▒▒ ▓▒                    
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo            ▒░▒   ░   ▒   ▒▒ ░  ░  ▒   ░ ░▒ ▒░                    
	echo             ░    ░   ░   ▒   ░        ░ ░░ ░                     
	::echo             ░            ░  ░░ ░      ░  ░                       
	::echo                  ░           ░                                   
	echo   █    ██  ██▓███   ▄▄▄     ▄▄▄█████▓ ▒█████   ██▀███  
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo   ██  ▓██▒▓██░  ██▒▒████▄   ▓  ██▒ ▓▒▒██▒  ██▒▓██ ▒ ██▒
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo  ▓██  ▒██░▓██░ ██▓▒▒██  ▀█▄ ▒ ▓██░ ▒░▒██░  ██▒▓██ ░▄█ ▒
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo  ▓▓█  ░██░▒██▄█▓▒ ▒░██▄▄▄▄██░ ▓██▓ ░ ▒██   ██░▒██▀▀█▄  
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo  ▒▒█████▓ ▒██▒ ░  ░ ▓█   ▓██▒ ▒██▒ ░ ░ ████▓▒░░██▓ ▒██▒
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo  ░▒▓▒ ▒ ▒ ▒▓▒░ ░  ░ ▒▒   ▓▒█░ ▒ ░░   ░ ▒░▒░▒░ ░ ▒▓ ░▒▓░
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo  ░░▒░ ░ ░ ░▒ ░       ▒   ▒▒ ░   ░      ░ ▒ ▒░   ░▒ ░ ▒░
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo   ░░░ ░ ░ ░░         ░   ▒    ░      ░ ░ ░ ▒    ░░   ░ 
	echo     ░                    ░  ░            ░ ░     ░     
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo.
	echo    POR GUILHERME MIGLIORINI
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    V. 0.0.1
	echo.
	ping 127.0.0.1 -n 1 >nul 2>&1
	echo    Copyleft 2022
	echo.
	color 0A
	echo.
	ping 127.0.0.1 -n 3 >nul 2>&1
	goto :eof

goto :eof

```
### fazerbackup.bat

```powershell

@echo off
chcp 65001 >nul 2>&1
setlocal enabledelayedexpansion
set /a "z = 1" >nul 2>&1
set /a "confirma = 0" 2>&1
for /f "eol=# tokens=1-9 delims=? usebackq" %%I in (programados.txt) do (
	::call :array %%~I %%~J %%~fK %%~fL %%~M %%~N %%~O %%~P %%~Q
	set arq[%%~I].ID=%%~I
	set arq[%%~I].Ativo=%%~J
	set arq[%%~I].PastaOrigem=%%~fK
	set arq[%%~I].PastaDestino=%%~fL
	set arq[%%~I].Serial=%%~M
	set arq[%%~I].DataRegistro=%%~N
	set arq[%%~I].HoraRegistro=%%~O
	set arq[%%~I].DataUltimoBackup=%%~P
	set arq[%%~I].HoraUltimoBackup=%%~Q )
:backupator
setlocal enabledelayedexpansion
if defined arq[%z%].ID (
	if [!arq[%z%].Ativo!] == [Sim] (
	
		set serial=!arq[%z%].Serial!
		set origem=!arq[%z%].PastaOrigem!
		set destino=!arq[%z%].PastaDestino!

		set variavel="wmic logicaldisk get Caption,VolumeSerialNumber | find "!serial!""
		for /f "tokens=1,2" %%1 in ( '!variavel!' ) do (
			set disco=%%~1
			ping 127.0.0.1 -n 1 >nul 2>&1
			robocopy.exe "!origem!" "!destino!" /E /LOG+:log.txt >nul 2>&1
			set /a "confirma+=1"

			if [%z%] == [1] (
				call echo.
				call echo    █ SERÃO REALIZADOS OS SEGUINTES BACKUPS: )
			call echo.
			call echo    █ ID:            !arq[%z%].ID!
			call echo    ▒ Ativo:         !arq[%z%].Ativo!
			call echo    ▒ ORIGEM:        !arq[%z%].PastaOrigem!
			call echo    ▒ DESTINO:       !arq[%z%].PastaDestino!
			call echo    ░ SERIAL:        !arq[%z%].Serial!
			call echo    ░ ATIVO DESDE:   !arq[%z%].DataRegistro! !arq[%w%].HoraRegistro!
			call echo    ░ ÚLTIMO BACKUP: !arq[%z%].DataUltimoBackup! !arq[%w%].HoraUltimoBackup!

		)
)
		set /a "z+=1" >nul 2>&1
		goto :backupator >nul 2>&1 )

if [%z%] == [1] (
	echo.
	echo    █ ERRO: Não há backups programados.
	exit /b )

if [%confirma%] == [0] (
	echo.
	echo    █ ERRO: O dispotivo precisa estar conectado.
	powershell -Command "& {Add-Type -AssemblyName System.Windows.Forms; Add-Type -AssemblyName System.Drawing; $notify = New-Object System.Windows.Forms.NotifyIcon; $notify.Icon = [System.Drawing.SystemIcons]::Information; $notify.Visible = $true; $notify.ShowBalloonTip(0, 'Script de Backup', 'O dispositivo não está conectado.', [System.Windows.Forms.ToolTipIcon]::None)}"
	exit /b ) else ( 
	powershell -Command "& {Add-Type -AssemblyName System.Windows.Forms; Add-Type -AssemblyName System.Drawing; $notify = New-Object System.Windows.Forms.NotifyIcon; $notify.Icon = [System.Drawing.SystemIcons]::Information; $notify.Visible = $true; $notify.ShowBalloonTip(0, 'Script de Backup', 'Conteúdo salvo no HD Externo. Verifique o log para mais informações.', [System.Windows.Forms.ToolTipIcon]::None)}"
	exit /b )

goto :eof

```
### initscript.bat

```powershell

@echo off
START /MIN CMD.EXE /C C:\Users\...\BACKUPATOR\fazerbackup.bat >nul 2>&1
exit >nul 2>&1

```
### logo.bat

```powershell

cls
echo.
echo            ▄▄▄▄    ▄▄▄       ▄████▄   ██ ▄█▀                    
ping 127.0.0.1 -n 1 >nul 2>&1
echo           ▓█████▄ ▒████▄    ▒██▀ ▀█   ██▄█▒                     
ping 127.0.0.1 -n 1 >nul 2>&1
echo           ▒██▒ ▄██▒██  ▀█▄  ▒▓█    ▄ ▓███▄░     
ping 127.0.0.1 -n 1 >nul 2>&1                
echo           ▒██░█▀  ░██▄▄▄▄██ ▒▓▓▄ ▄██▒▓██ █▄                     
ping 127.0.0.1 -n 1 >nul 2>&1
echo           ░▓█  ▀█▓ ▓█   ▓██▒▒ ▓███▀ ░▒██▒ █▄                    
ping 127.0.0.1 -n 1 >nul 2>&1
echo           ░▒▓███▀▒ ▒▒   ▓▒█░░ ░▒ ▒  ░▒ ▒▒ ▓▒                    
ping 127.0.0.1 -n 1 >nul 2>&1
echo           ▒░▒   ░   ▒   ▒▒ ░  ░  ▒   ░ ░▒ ▒░                    
::ping 127.0.0.1 -n 1 >nul 2>&1
::echo            ░    ░   ░   ▒   ░        ░ ░░ ░                     
::echo            ░            ░  ░░ ░      ░  ░                       
::echo                 ░           ░                                   
ping 127.0.0.1 -n 1 >nul 2>&1
echo   █    ██  ██▓███   ▄▄▄     ▄▄██████▓ ▒█████   ██▀███  
ping 127.0.0.1 -n 1 >nul 2>&1
echo   ██  ▓██▒▓██░  ██▒▒████▄   ▓  ██▒ ▓▒▒██▒  ██▒▓██ ▒ ██▒
ping 127.0.0.1 -n 1 >nul 2>&1
echo  ▓██  ▒██░▓██░ ██▓▒▒██  ▀█▄ ▒ ▓██░ ▒░▒██░  ██▒▓██ ░▄█ ▒
ping 127.0.0.1 -n 1 >nul 2>&1
echo  ▓▓█  ░██░▒██▄█▓▒ ▒░██▄▄▄▄██░ ▓██▓ ░ ▒██   ██░▒██▀▀█▄  
ping 127.0.0.1 -n 1 >nul 2>&1
echo  ▒▒█████▓ ▒██▒ ░  ░ ▓█   ▓██▒ ▒██▒ ░ ░ ████▓▒░░██▓ ▒██▒
ping 127.0.0.1 -n 1 >nul 2>&1
echo  ░▒▓▒ ▒ ▒ ▒▓▒░ ░  ░ ▒▒   ▓▒█░ ▒ ░░   ░ ▒░▒░▒░ ░ ▒▓ ░▒▓░
ping 127.0.0.1 -n 1 >nul 2>&1
echo  ░░▒░ ░ ░ ░▒ ░       ▒   ▒▒ ░   ░      ░ ▒ ▒░   ░▒ ░ ▒░
ping 127.0.0.1 -n 1 >nul 2>&1
::echo   ░░░ ░ ░ ░░         ░   ▒    ░      ░ ░ ░ ▒    ░░   ░ 
::ping 127.0.0.1 -n 1 >nul 2>&1
echo     ░                    ░  ░            ░ ░     ░    
exit /b

```

