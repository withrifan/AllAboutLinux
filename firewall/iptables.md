# Iptables
Perintah Iptables untuk mengizinkan port/service yang diperlukan dan memblokir semua port yang tidak diperlukan.
## Input Rules
Rules untuk mengelola trafik yang masuk ke Linux Server 

Mengizinkan input dari interface Loopback

    iptables -A INPUT -i lo -j ACCEPT

Mengizinkan input dari trafik yang sudah ada & terkait

    iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT

Mengizinkan input untuk protokol ICMP (ping)
    
    -A INPUT -p icmp -j ACCEPT

Mengizinkan input untuk service DNS dengan port udp
    
    -A INPUT -p udp -m udp --dport 53 -j ACCEPT
    -A INPUT -p tcp -m multiport --dports 49152:65534 -j ACCEPT
    -A INPUT -p tcp -m multiport --dports 80,443 -j ACCEPT
    -A INPUT -p tcp -m tcp --dport 2222 -j ACCEPT
    -A INPUT -p tcp -m tcp --dport 21211 -j ACCEPT
    -A INPUT -p tcp -m tcp --dport 445 -j ACCEPT
    -A INPUT -p tcp -m tcp --dport 139 -j ACCEPT
    -A INPUT -p tcp -m tcp --dport 25 -j ACCEPT
    -A INPUT -p tcp -m tcp --dport 143 -j ACCEPT
    -A INPUT -p tcp -m tcp --dport 110 -j ACCEPT
    -A INPUT -j DROP

Output Rules

    -A OUTPUT -o lo -j ACCEPT
    -A OUTPUT -m conntrack --ctstate ESTABLISHED -j ACCEPT
    -A OUTPUT -p icmp -j ACCEPT
    -A OUTPUT -p udp -m udp --sport 53 -j ACCEPT
    -A OUTPUT -p tcp -m multiport --sports 49152:65534 -j ACCEPT
    -A OUTPUT -p tcp -m multiport --sports 80,443 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --sport 2222 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --sport 21211 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --sport 445 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --sport 139 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --sport 25 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --sport 143 -j ACCEPT
    -A OUTPUT -p tcp -m tcp --sport 110 -j ACCEPT
    -A OUTPUT -j DROP
