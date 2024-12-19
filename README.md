# usefuloneliners
Incredibly handy one-liner scripts for everyday life.
# Atenea CCN-Cert
[Bash] General purpose. Generate flag code.
    
    read -p "Solución: " s; echo "flag{$(md5sum <<< "$s" | cut -d' ' -f1)}";

[Bash] "Batflag" challenge. Web directory enumeration. Downloads DirBuster dictionary (https://github.com/dustyfresh/) asks the user for a directory to test and try every word, saving the results.

    rm resultados.txt; echo "Ingrese la dirección URL en formato 'http://pagina.com/directorio/':" && read -r url_base && echo "Descargando archivo diccionario..." && curl -sSLO https://github.com/dustyfresh/dictionaries/raw/master/DirBuster-Lists/directory-list-2.3-big.txt -o diccionario.txt && while IFS= read -r linea; do if [[ $linea == \#* ]]; then continue; fi; linea2=$(echo "$linea" | xargs); url="$url_base$(echo -n "$linea2" | sed 's/ /%20/g')"; curl -I "$url" > temp; cat temp | grep "\< HTTP/1.1 "; echo "-- $linea2 --" >> resultados.txt; cat temp >> resultados.txt; rm temp; done < diccionario.txt

# Lexnet

[Bash] Script designed to run in a folder containing PDF files that lack OCR and do not comply with the PDF-A standard. This script applies OCR to all PDFs, then converts them to PDF-A format and saves them in the 'resultados' folder, ready for Lexnet submission. Remember install first dependencies: sudo apt install ocrmypdf ghostscript

    mkdir -p resultado && for pdf in *.pdf; do ocrmypdf "$pdf" "resultado/$pdf" && gs -dPDFA=1 -dBATCH -dNOPAUSE -dQUIET -sOutputFile="resultado/$(basename "$pdf" .pdf)-PDF-A.pdf" "resultado/$pdf" && rm -f "resultado/$pdf"; done

# Misc

[Python]  Tic-tac-toe game created in Python, minimized to its bare essentials using ternary operators and nested lambda functions, just for fun.

    import random, os; dc = dict.fromkeys('qweasdzxc', ''); l = lambda: os.system('cls' if os.name == 'nt' else 'clear'); m = lambda t: print(f"\n╔{'═' * (len(t:=f'  {t}  ')+2)}╗\n║{t}║\n╚{'═' * (len(t)+2)}╝"); i = lambda: print("\n".join(" ".join(f"{p}[{'█' if dc[p]=='X' else '▒' if dc[p]=='O' else ' '}]" for p in r) for r in [['q','w','e'],['a','s','d'],['z','x','c']])); v = lambda: next((dc[c[0]] for c in [['q','w','e'],['a','s','d'],['z','x','c'],['q','a','z'],['w','s','x'],['e','d','c'],['q','s','c'],['e','s','z']] if dc[c[0]]==dc[c[1]]==dc[c[2]] and dc[c[0]]), 'emp' if all(dc.values()) else None); mvma = lambda: next((cmb[[dc[p] for p in cmb].index('')] for s,r in [('O','X'),('X','O')] for cmb in [['q','w','e'],['a','s','d'],['z','x','c'],['q','a','z'],['w','s','x'],['e','d','c'],['q','s','c'],['e','s','z']] if [dc[p] for p in cmb].count(s)==2 and [dc[p] for p in cmb].count('')==1), random.choice([p for p in dc if dc[p]==''))); trnj = lambda: exec("while (jgda:=input('▬▬▬ Elige casilla ►►► ').lower()) not in dc or dc[jgda]!='': pass; dc[jgda]='X'"); jgar = lambda: exec("ja='jug' if random.choice(['jug','maq'])=='jug' else (dc.update(s='O'), 'maq'); fn='Fin del juego'; while True: l(); m(f'Turno de {\"JUGADOR\" if ja==\"jug\" else \"MAQUINA\"}'); i(); (trnj() if ja=='jug' else dc.update({mvma():'O'})); est=v(); (l(), m(fn), i(), m('¡El jugador gana!' if est=='X' else '¡La máquina gana!' if est=='O' else '¡Empate!'), exit()) if est in ['X','O','emp'] else exec('ja=\"maq\"' if ja=='jug' else 'ja=\"jug\"')"); jgar() if __name__ == "__main__" else None

    
# Windows

[PS] Dumps the DNS resolution cache to dnsdump.txt (SPANISH).

    ipconfig /displaydns | Select-String "Nombre de registro" | ForEach-Object { $_.ToString().Split(":")[1].Trim() } | Out-File -FilePath dnsdump.txt

[Batch] System info snapshot and dump to infodump.txt. Generates an information file that includes running processes with detailed information, username (in three different forms), details of the current user (privileges and groups), the registration status of the device in Azure, and the Kerberos ticket cache.

    (tasklist /V & whoami & whoami /all & set & echo %username% & dsregcmd /status & klist & wmic.exe computersystem get username) >> infodump.txt
