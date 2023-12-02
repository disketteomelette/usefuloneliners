# usefuloneliners
Incredibly handy one-liner scripts for everyday life.
# Atenea CCN-Cert
[Bash] Generate flag code.
    
    read -p "Solución: " s; echo "flag{$(md5sum <<< "$s" | cut -d' ' -f1)}";
    
# Windows

[PS] Dumps the DNS resolution cache to dnsdump.txt (SPANISH).

    ipconfig /displaydns | Select-String "Nombre de registro" | ForEach-Object { $_.ToString().Split(":")[1].Trim() } | Out-File -FilePath dnsdump.txt

[Batch] System info snapshot and dump to infodump.txt. Generates an information file that includes running processes with detailed information, username (in three different forms), details of the current user (privileges and groups), the registration status of the device in Azure, and the Kerberos ticket cache.

    (tasklist /V & whoami & whoami /all & set & echo %username% & dsregcmd /status & klist & wmic.exe computersystem get username) >> infodump.txt
