konfigurasi ssh keypair

- apt install openssh-server
- masuk ke client
  ssh-keygen -t rsa
- tekan enter atau kosongi passwordnya
- copy dari client ke server
  ssh-copy-id tkj@192.168.10.2 (ipnya server)
- remote client ke server
  ssh tkj@192.168.10.2

konfigurasi ssh keypair

- apt install openssh-server
- buka client
  ssh-keygen -t rsa
  kosongin passpharse
- ssh-copy-id tkj@192.168.10.2
