# usefuloneliners
Incredibly handy one-liner scripts for everyday life.
# Atenea CCN-Cert
[Bash] General purpose. Generate flag code.
    
    read -p "Solución: " s; echo "flag{$(md5sum <<< "$s" | cut -d' ' -f1)}";

[Bash] "Batflag" challenge. Web directory enumeration. Downloads DirBuster dictionary (https://github.com/dustyfresh/) asks the user for a directory to test and try every word, saving the results.

    rm resultados.txt; echo "Ingrese la dirección URL en formato 'http://pagina.com/directorio/':" && read -r url_base && echo "Descargando archivo diccionario..." && curl -sSLO https://github.com/dustyfresh/dictionaries/raw/master/DirBuster-Lists/directory-list-2.3-big.txt -o diccionario.txt && while IFS= read -r linea; do if [[ $linea == \#* ]]; then continue; fi; linea2=$(echo "$linea" | xargs); url="$url_base$(echo -n "$linea2" | sed 's/ /%20/g')"; curl -I "$url" > temp; cat temp | grep "\< HTTP/1.1 "; echo "-- $linea2 --" >> resultados.txt; cat temp >> resultados.txt; rm temp; done < diccionario.txt

    
# Windows

[PS] Dumps the DNS resolution cache to dnsdump.txt (SPANISH).

    ipconfig /displaydns | Select-String "Nombre de registro" | ForEach-Object { $_.ToString().Split(":")[1].Trim() } | Out-File -FilePath dnsdump.txt

[Batch] System info snapshot and dump to infodump.txt. Generates an information file that includes running processes with detailed information, username (in three different forms), details of the current user (privileges and groups), the registration status of the device in Azure, and the Kerberos ticket cache.

    (tasklist /V & whoami & whoami /all & set & echo %username% & dsregcmd /status & klist & wmic.exe computersystem get username) >> infodump.txt
