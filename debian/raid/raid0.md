# Install Debian with RAID 0
Menggunakan beberapa HDD yang digabung menjadi 1, agar menambah kapasitas penyimpanan dan backup data.

## RAID 0
Misal 2 HDD dengan kapasitas masing-masing 100GB, maka totalnya 200GB. Kelebihan performa read & write lebih cepat, namun kekurangannya jika data di HDD 1 rusak maka data yang disimpan tidak bisa terbaca.

## Langkah-langkah 
- Partitioning method = Manual
- Pilih HDD ke 1 lalu klik Yes pada "Create new empty partition table on this device"
- Lakukan hal yang sama untuk HDD ke 2
- Misal 2 HDD dengan kapasitas masing-masing 20GB, akan kita bagi menjadi 2 partisi yaitu 1GB swap dan sisanya partisi Root (/)
- Pilih Free Space pada HDD ke 1
- Create a new partition
- Ubah menjadi 0.5 GB lalu Continue
- Pilih Primary
- Pilih Beginning
- Pada bagian Use as pilih "physical volume for RAID"
- lalu "Done setting up the partition"
- lakukan hal yang sama untuk HDD ke 2
- Selanjutnya kita buat partisi yang nantinya akan digunakan oleh Root (/)
- Pilih Free Space pada HDD ke 1
- Create a new partition lalu enter
- New partition size lalu enter
- Pilih Primary
- Pilih Beginning
- Pada bagian Use as pilih "physical volume for RAID"
- lalu "Done setting up the partition"
- lakukan hal yang sama untuk HDD ke 2

Jika pada HDD 1 dan 2 sudah terpartisi raid, selanjutnya kita gabungkan menjadi 1 partisi tersebut

- Pilih Configure software RAID
- Pilih Yes
- Pada "Software RAID configuration actions" pilih Create MD device
- Pada "Software RAID device type" pilih RAID0
- Pada "Active devices for the RAID0 array" pilih partisi yang kita buat untuk swap, dengan tekan spasi pada partisi HDD ke 1 dan partisi HDD ke 2
- tekan Enter
- Pada "Software RAID configuration actions" pilih Create MD device
- Pada "Software RAID device type" pilih RAID0
- Pada "Active devices for the RAID0 array" pilih partisi yang kita buat untuk Root (/), dengan tekan spasi pada partisi HDD ke 1 dan partisi HDD ke 2
- tekan Enter
- Pada "Software RAID configuration actions" pilih Finish

Hasilnya ada 2 RAID0 dengan ukuran 
