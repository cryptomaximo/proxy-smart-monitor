@echo off
setlocal

:: Variabili di configurazione
set "REPO_NAME=proxy-smart-monitor"
set "SCRIPT_NAME=monitorProxies.js"
set "DESCRIPTION=Repository per il monitoraggio dei proxy"
set "USERNAME=cryptomaximo"

:: Creazione di una nuova directory per il progetto
mkdir %REPO_NAME%
cd %REPO_NAME%

:: Creazione del file di script
echo const proxies = [ > %SCRIPT_NAME%
echo   { ip: "ip-proxy1", port: 6540, username: "user", password: "pass" }, >> %SCRIPT_NAME%
echo   { ip: "ip-proxy2", port: 6712, username: "user", password: "pass" }, >> %SCRIPT_NAME%
echo   { ip: "ip-proxy3", port: yourport, username: "user", password: "pass" }, >> %SCRIPT_NAME%
echo ]; >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo const testUrl = "https://google.com"; // Endpoint pubblico per il test >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo function monitorProxiesAndLogToSheet() { >> %SCRIPT_NAME%
echo   const spreadsheet = SpreadsheetApp.getActiveSpreadsheet(); >> %SCRIPT_NAME%
echo   let detailSheet = spreadsheet.getSheetByName("Proxy Details"); >> %SCRIPT_NAME%
echo   let summarySheet = spreadsheet.getSheetByName("Proxy Summary"); >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   // Creazione o Pulizia dei Fogli >> %SCRIPT_NAME%
echo   if (!detailSheet) { >> %SCRIPT_NAME%
echo     detailSheet = spreadsheet.insertSheet("Proxy Details"); >> %SCRIPT_NAME%
echo   } else { >> %SCRIPT_NAME%
echo     detailSheet.clear(); >> %SCRIPT_NAME%
echo   } >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   if (!summarySheet) { >> %SCRIPT_NAME%
echo     summarySheet = spreadsheet.insertSheet("Proxy Summary"); >> %SCRIPT_NAME%
echo   } else { >> %SCRIPT_NAME%
echo     summarySheet.clear(); >> %SCRIPT_NAME%
echo   } >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   // Intestazioni per i dettagli >> %SCRIPT_NAME%
echo   const detailHeaders = ["Timestamp", "IP", "Port", "Status", "Response Time (ms)", "Error"]; >> %SCRIPT_NAME%
echo   detailSheet.getRange(1, 1, 1, detailHeaders.length).setValues([detailHeaders]); >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   // Risultati >> %SCRIPT_NAME%
echo   const results = proxies.map(proxy => { >> %SCRIPT_NAME%
echo     const startTime = new Date().getTime(); >> %SCRIPT_NAME%
echo     let isWorking = false; >> %SCRIPT_NAME%
echo     let responseTime = null; >> %SCRIPT_NAME%
echo     let errorMessage = null; >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo     try { >> %SCRIPT_NAME%
echo       UrlFetchApp.fetch(testUrl, { >> %SCRIPT_NAME%
echo         method: "get", >> %SCRIPT_NAME%
echo         muteHttpExceptions: true, >> %SCRIPT_NAME%
echo         proxy: { >> %SCRIPT_NAME%
echo           host: proxy.ip, >> %SCRIPT_NAME%
echo           port: proxy.port, >> %SCRIPT_NAME%
echo           auth: { >> %SCRIPT_NAME%
echo             username: proxy.username, >> %SCRIPT_NAME%
echo             password: proxy.password, >> %SCRIPT_NAME%
echo           }, >> %SCRIPT_NAME%
echo         }, >> %SCRIPT_NAME%
echo       }); >> %SCRIPT_NAME%
echo       isWorking = true; >> %SCRIPT_NAME%
echo       responseTime = new Date().getTime() - startTime; >> %SCRIPT_NAME%
echo     } catch (error) { >> %SCRIPT_NAME%
echo       errorMessage = error.toString(); >> %SCRIPT_NAME%
echo     } >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo     return { >> %SCRIPT_NAME%
echo       timestamp: new Date().toLocaleString(), >> %SCRIPT_NAME%
echo       ip: proxy.ip, >> %SCRIPT_NAME%
echo       port: proxy.port, >> %SCRIPT_NAME%
echo       status: isWorking ? "WORKING" : "FAILED", >> %SCRIPT_NAME%
echo       responseTime: responseTime || "N/A", >> %SCRIPT_NAME%
echo       error: errorMessage, >> %SCRIPT_NAME%
echo     }; >> %SCRIPT_NAME%
echo   }); >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   // Scrittura dei dettagli >> %SCRIPT_NAME%
echo   results.forEach((result, index) => { >> %SCRIPT_NAME%
echo     detailSheet.getRange(index + 2, 1, 1, detailHeaders.length).setValues([ >> %SCRIPT_NAME%
echo       [result.timestamp, result.ip, result.port, result.status, result.responseTime, result.error], >> %SCRIPT_NAME%
echo     ]); >> %SCRIPT_NAME%
echo   }); >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   // Calcolo delle statistiche >> %SCRIPT_NAME%
echo   const workingProxies = results.filter(result => result.status === "WORKING"); >> %SCRIPT_NAME%
echo   const failedProxies = results.filter(result => result.status === "FAILED"); >> %SCRIPT_NAME%
echo   const averageLatency = workingProxies.reduce((sum, proxy) => sum + (proxy.responseTime || 0), 0) / workingProxies.length || "N/A"; >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   // Scrittura del riepilogo >> %SCRIPT_NAME%
echo   const summaryHeaders = ["Total Proxies", "Working Proxies", "Failed Proxies", "Average Latency (ms)", "Failure Rate (%)"]; >> %SCRIPT_NAME%
echo   const summaryData = [ >> %SCRIPT_NAME%
echo     proxies.length, >> %SCRIPT_NAME%
echo     workingProxies.length, >> %SCRIPT_NAME%
echo     failedProxies.length, >> %SCRIPT_NAME%
echo     averageLatency, >> %SCRIPT_NAME%
echo     ((failedProxies.length / proxies.length) * 100).toFixed(2), >> %SCRIPT_NAME%
echo   ]; >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo   summarySheet.getRange(1, 1, 1, summaryHeaders.length).setValues([summaryHeaders]); >> %SCRIPT_NAME%
echo   summarySheet.getRange(2, 1, 1, summaryData.length).setValues([summaryData]); >> %SCRIPT_NAME%
echo } >> %SCRIPT_NAME%
echo. >> %SCRIPT_NAME%
echo function scheduleMonitoring() { >> %SCRIPT_NAME%
echo   ScriptApp.newTrigger("monitorProxiesAndLogToSheet") >> %SCRIPT_NAME%
echo     .timeBased() >> %SCRIPT_NAME%
echo     .everyMinutes(15) // Modifica la frequenza qui (es. ogni 15 minuti) >> %SCRIPT_NAME%
echo     .create(); >> %SCRIPT_NAME%
echo } >> %SCRIPT_NAME%
