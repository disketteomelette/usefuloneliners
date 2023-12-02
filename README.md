# usefuloneliners
Incredibly handy one-liner scripts for everyday life.
# Atenea CCN-Cert
Generate flag code.
    
    read -p "Solución: " solucion; hash_md5=$(echo -n "$solucion" | md5sum | awk '{print $1}'); echo "flag{$hash_md5}";
    
