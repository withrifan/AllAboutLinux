# Install Debian with RAID 1
Sama seperti Mirroring, misal 2 HDD dengan kapasitas masing-masing 100GB maka data disimpan di kedua HDD tersebut dan kapasitas HDD tidak bertambah menjadi 200GB melainkan tetap 100GB. Kekurangannya juga, proses menulis lebih lama karena perlu sinkronisasi dengan kedua HDD.
Namun jika data yang data di HDD pertama rusak maka data yang di HDD kedua masih aman.

Misal kita akan membuat RAID 1 di 2 HDD yang berkapasitas masing-masing 20GB, nantinya akan dibuat partisi 1GB untuk swap dan sisanya untuk Root (/).

## Langkah-langkah
- Partitioning method = Manual
- Pilih HDD ke 1 lalu klik Yes pada "Create new empty partition table on this device"
- Lakukan hal yang sama untuk HDD ke 2
- Pilih Free Space pada HDD ke 1
- Create a new partition
- Ubah menjadi 1 GB lalu Continue
- Pilih Primary
- Pilih Beginning
- Pada bagian Use as pilih "physical volume for RAID"
- lalu "Done setting up the partition"
- lakukan hal yang sama untuk HDD ke 2

Selanjutnya kita buat partisi yang nantinya akan digunakan oleh Root (/)

- Pilih Free Space pada HDD ke 1
- Create a new partition lalu enter
- New partition size lalu enter
- Pilih Primary
- Pilih Beginning
- Pada bagian Use as pilih "physical volume for RAID"
- lalu "Done setting up the partition"
- lakukan hal yang sama untuk HDD ke 2

Jika pada HDD 1 dan 2 sudah terpartisi raid, selanjutnya kita konfigurasi software RAID

- Pilih Configure software RAID
- Pilih Yes
- Pada "Software RAID configuration actions" pilih Create MD device
- Pada "Software RAID device type" pilih RAID1
- Pada "Number of active devices for the RAID1 array" masukkan jumlah HDD yang kita gunakan
- Pada "Number of spare devices for the RAID1 array" lalu Continue
- Pada "Active devices for the RAID1 array" pilih partisi yang kita buat untuk swap, dengan tekan spasi pada partisi HDD ke 1 dan partisi HDD ke 2 lalu Continue
- Pada "Software RAID configuration actions" pilih Create MD device
- Pada "Software RAID device type" pilih RAID1
- Pada "Number of active devices for the RAID1 array" masukkan jumlah HDD yang kita gunakan
- Pada "Number of spare devices for the RAID1 array" lalu Continue
- Pada "Active devices for the RAID1 array" pilih partisi yang kita buat untuk Root (/), dengan tekan spasi pada partisi HDD ke 1 dan partisi HDD ke 2 lalu Continue
- Pada "Software RAID configuration actions" pilih Finish

Hasilnya ada 2 RAID1 dengan ukuran sekitar 1GB dan 20GB, yang 1 GB kita buat Swap dan 20GB untuk Root (/)

- Pilih partisi 1GB pada bagian RAID1
- Pada Use as pilih swap area
- lalu Done setting up a partition
- Pilih partisi 20GB pada bagian RAID1
- Pada Use as pilih Ext4 journaling file system lalu Enter
- Pada Mount point pilih "/ the root file system"
- lalu Done setting up a partition
- lalu Finish partitioning and write changes to disk
- lalu pilih Yes pada Write the changes to disks
