<details>
  <summary>nmap</summary>

    nmap -Pn -sS -n <ip> -f 

     * -il <file name>
     * -sV > get service version
     * -p 22 > for port 22
     * -p22,21,443
     * -Pn > bypass firewall
     * -f > fragment mode to bypass firewall
     * -D RND:5 > get 5 random IPs
     * --source-port 67 > the firewall maybe allow this port 
     * -O > get operating system
     * -n > skip DNS servers
     * -S > to set you Source ip

    SCRIPTS
      - nmap ayhaga.com -p22 --script=ssh*
      -  --script=brute
     
</details>


<details>
  <summary>masscan</summary>

    - masscan 192.168.1.20 -p0-65535 --rate=1000
    - faster than nmap
    - accept only ip 

</details>
