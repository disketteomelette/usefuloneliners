# usefuloneliners
Incredibly handy one-liner scripts for everyday life.
# Atenea CCN-Cert
[Bash] Generate flag code.
    
    read -p "Solución: " s; echo "flag{$(md5sum <<< "$s" | cut -d' ' -f1)}";
    
# Windows

[PS] Dumps the DNS resolution cache to dnsdump.txt

    ipconfig /displaydns | Select-String "Nombre de registro" | ForEach-Object { $_.ToString().Split(":")[1].Trim() } | Out-File -FilePath dnsdump.txt
