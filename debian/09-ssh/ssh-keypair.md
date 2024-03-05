## SSH Keypair

generate ssh keygen with RSA keys in client

    apt install openssh-server
    ssh-keygen -t rsa

copy from client to server

    ssh-copy-id -i ~/.ssh/id_rsa.pub -p 2222 rifan@192.168.1.254 (IP server)

remote server

    ssh rifan@192.168.1.254 -p 2222
