# usefuloneliners
Incredibly handy one-liner scripts for everyday life.
# Atenea CCN-Cert
Generate flag code.
    
    read -p "Solución: " s; echo "flag{$(md5sum <<< "$s" | cut -d' ' -f1)}";
    
