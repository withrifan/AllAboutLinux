## Install tmux (terminal multiplexer)
https://github.com/tmux/tmux

Install dependencies

    sudo apt install libevent-2.1-7 libevent-dev ncurses-base gcc make pkg-config bison   

Debian/Ubuntu based
    
    apt install tmux
    
    or
    
    git clone https://github.com/tmux/tmux
    cd tmux
    sh autogen.sh
    ./configure
    make && sudo make install
    
## Penggunaan tmux
start tmux dengan nama sesi

    tmux new -s satu
    
cek sesi tmux
    
    tmux ls

hapus sesi tmux

    tmux kill-session -t satu

Split horizontal
  
    Ctrl + b, lalu  Shift + %
    
Split vertical

    Ctrl + b, lalu Shift + "
    
Detach sesi

    Ctrl + a + d
