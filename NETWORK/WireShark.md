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
