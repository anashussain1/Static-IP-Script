# Static-IP-Script
@echo off
:: Static IP configuration for Knut Hedtfeld laptop

set "IFACE=Ethernet"
:: Example of IP adress assign
set "IP=10.00.00.09"
set "MASK=255.255.0.0"
set "GW=10.0.00.1"
set "DNS1=10.00.00.1"
set "DNS2=10.00.00.2"

echo Configuring static IP for %IFACE%...

netsh interface ip set address name="%IFACE%" static %IP% %MASK% %GW% 1
if errorlevel 1 (
    echo Failed to set IP address.
    pause
    exit /b 1
)

echo Setting primary DNS to %DNS1%...
netsh interface ip set dns name="%IFACE%" static %DNS1%

echo Adding secondary DNS %DNS2%...
netsh interface ip add dns name="%IFACE%" %DNS2% index=2

echo ----------------------------------------
echo Static IP configuration completed.
echo IP: %IP%
echo Gateway: %GW%
echo DNS: %DNS1%, %DNS2%
echo ----------------------------------------

pause
