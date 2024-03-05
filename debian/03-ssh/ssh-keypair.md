## SSH Keypair

Generate ssh keygen menggunakan RSA keys pada Linux client

    apt install openssh-server
    ssh-keygen -t rsa

Menyalin file id_rsa.pub dari client ke SSH server

    ssh-copy-id -i ~/.ssh/id_rsa.pub -p 2222 rifan@10.10.10.254

## Pada Windows Client

Mengaktifkan AuthorizedKeys pada server, menghapus tanda # di depan AuthorizedKeysFile 

    nano /etc/ssh/sshd_config
    AuthorizedKeysFile  .ssh/authorized_keys

Restart SSH server

    systemctl restart ssh

Generate ssh keygen menggunakan PuTTY Key Generator pada Windows client

1. Buka aplikasi PuTTYGen
2. Pada Generate a public/private key pair, klik Generate
3. Gerakan mouse pada bagian Key
4. Pada Save generated key, klik Save private key lalu beri nama
5. Pada Key, salin ssh-rsa ke file ~/.ssh/authorized_keys pada SSH server
6. Buka aplikasi PuTTY --> Connection --> SSH --> Auth --> Credentials
7. Pada bagian Private key file for authentication --> pilih file private key yang sudah disimpan tadi
8. Selanjutnya tes koneksi ke server