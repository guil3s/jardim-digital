---
{"dg-publish":true,"permalink":"/backupator-uma-brincadeira-para-praticar-dos/","dg-note-properties":{}}
---

Há alguns anos atrás atrás comecei a escrever um script para automatizar o Backup de alguns arquivos do meu notebook para meu hd externo.

Fiz todo o desenvolvimento em DOS, para praticar os códigos de script. Infelizmente não consegui me furtar de usar powershell em alguns momentos do código, como você poderá perceber.

Atualmente o script está funcional. Também, realizei o agenda de tarefa, nativo do windows, para que, sempre que meu hd externo é conectado o script roda e faz o backup automaticamente, isso é bem interessante.

Ainda não subi o projeto para o github, quem sabe eu faça isso futuramente. Por enquanto, segue o código pra quem se interessar.

`@echo off
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
	for /f "eol=# tokens=1-9 delims=? usebackq" ~I ~fK ~M ~O ~Q
		set arq[~I
		set arq[~J
		set arq[~fK
		set arq[~fL
		set arq[~M
		set arq[~N
		set arq[~O
		set arq[~P
		set arq[~Q
	)
	set /a "y = 1" >nul 2>&1
	cls
	:exibe
	if defined arq[%y%].ID (
		if [%y%] == [1] (
			call echo.
			call echo    █ SÃO OS BACKUPS PROGRAMADOS: )
		call echo.
		call echo    █ ID:            
		call echo    ▒ Ativo:         
		call echo    ▒ ORIGEM:        
		call echo    ▒ DESTINO:       
		call echo    ░ SERIAL:        
		call echo    ░ ATIVO DESDE:    
		call echo    ░ ÚLTIMO BACKUP:  
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
	for /f "usebackq delims=" I""
	echo.
	echo    █ Escolha a pasta destino.
	set "psCommand="(new-object -COM 'Shell.Application')^.BrowseForFolder(0,'Escolha a pasta do destino.',0,0).self.path""
	for /f "usebackq delims=" I""
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
	for /f "eol=# tokens=1-9 delims=? usebackq" P in ( '%capturadisco%' ) do set "caption=~Q >nul 2>&1
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
	:::::call echo ????????>>programados.txt:::::
	:::::call echo. >>programados.txt
	(call echo ????????)>>programados.txt
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
goto :eof`