## Passive Enum
    - subfinder -d target.com -o subs.txt -all
<details>
  <summary>Helpful Sites</summary>

    censys       bevigil
    
    binaryedge   cerspotter
    
    whoisxmlapi  fofa
    
    shodan       github
    
    virustotal   zoomeye
</details>      

<details>
 <summary> Subdomain enumeration </summary>

	Tool for automative recon
	https://github.com/blacklanternsecurity/bbot

    
     https://securitytrails.com/
    
    https://subdomainfinder.c99.nl/
    
    https://shrewdeye.app/ 
    
    
    # subfinder -d ~~mars.com~~ -all --recursive  -o subs.txt
  
    
   
    # echo ~~mars.com~~ | assetfinder --subs-only >> subs.txt
    
    
    after collecting all subdomains in subs.txt then let's remove duplicate 
    # cat subs.txt | anew >> allsubs.txt
    # rm subs.txt
</details>

-----------------------------------------------------------------------------



## ASN number
    - https://bgp.he.net/
    -  whois -h whois.radb.net  -- '-i origin AS8983' | grep -Eo "([0-9.]+){4}/[0-9]+" | uniq -u > ip_ranges.txt
## PTR (revrse DNS)
    - cat ip_anges.txt | mapcidr -silent | dnsx -ptr -resp-only -o ptr_recrds.txt
    - this step provide the host/domain name of ip's in the ip_range.txt 
