# usefuloneliners
Incredibly handy one-liner scripts for everyday life.
# Atenea CCN-Cert
Generate flag code.
    
    Encryread -p "Solución: " solucion; hash_md5=$(echo -n "$solucion" | md5sum | awk '{print $1}'); echo "flag{$hash_md5}"; ption: Securely encrypts the content of a specified input file using a user-provided password.
    Decryption: Decrypts an encrypted file to recover the original content using the same password.
