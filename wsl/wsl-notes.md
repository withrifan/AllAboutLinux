## Export Import to another drive
Export Ubuntu-22.04 WSL to another drive

     wsl --export Ubuntu-22.04 Z:\Ubuntu-22.04.tar

Unregister Ubuntu-22.04 WSL

    wsl --unregister Ubuntu-22.04

Import Ubuntu-22.04 file tar

    wsl --import Ubuntu-22.04 z:\wsl\Ubuntu-22.04 z:\Ubuntu-22.04.tar

Change default user Ubuntu-22.04

    ubuntu2204.exe config --default-user rifan

## Debian/Ubuntu
run 32bit C program in 64bit device

    sudo dpkg --add-architecture i386
    sudo apt update
    sudo apt install gcc-multilib
