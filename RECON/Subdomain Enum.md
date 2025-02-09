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

<details>
<summary>  Subdomain takeover </summary>
    
    # subzy run --targets subs.txt --hide_fails --vuln  | grep -v -E "Akamai|xyz|available|\-"
    if you found any vulnerability then search on how to takeover subdomain 
</details>
    
-----------------------------------------------------------------------------


  <details>       
## <summary>httpx</summary>
    
    to see the working sites 
    # cat allsubs.txt | httpx -o httpx.txt
    # cat httpx.txt | httpx -mc 200 -o httpx200.txt    
    1- use smuggler to check request smuggling vulnerablitiy 
    # cat httpx.txt | smuggler.py | tee -a smuggler.txt
</details>

-----------------------------------------------------------------------------


<details>
## <summary>dirsearch and ffuf</summary>
    
    1- if you need to fuzz all the file of urls httpx.txt
    # dirsearch -l $(pwd)/httpx.txt -i 200  -e conf,config,bak,backup,swp,old,db,sql,asp,aspx,aspx~,asp~,py,py~,rb,rb~,php,php~,bak,bkp,cache,cgi,conf,csv,html,inc,jar,js,json,jsp,jsp~,lock,log,rar,old,sql,sql.gz,http://sql.zip,sql.tar.gz,sql~,swp,swp~,tar,tar.bz2,tar.gz,txt,wadl,zip,.log,.xml,.js.,.json
    2- if you need to fuzz specific site 
    # dirsearch -u ~~https://mars.com~~  -i 200  -e conf,config,bak,backup,swp,old,db,sql,asp,aspx,aspx~,asp~,py,py~,rb,rb~,php,php~,bak,bkp,cache,cgi,conf,csv,html,inc,jar,js,json,jsp,jsp~,lock,log,rar,old,sql,sql.gz,http://sql.zip,sql.tar.gz,sql~,swp,swp~,tar,tar.bz2,tar.gz,txt,wadl,zip,.log,.xml,.js.,.json
    3- you can use ffuf and wordlist of file names from google 
    # ffuf -u ~~https://mars.com~~/FUZZ -w ~~wordlist.txt~~  -mc 200 
    
    advanced mode of ffuf to bypass rate limit and firewall
    # ffuf -u ~~https://mars.com~~/FUZZ -w wordlist.txt -H "X-Forwarded-For: 127.0.0.1"
    -H "X-Forwarded-Host: 127.0.0.1" 
    
    to fuzz in two places with two files 
    # ffuf -u https://mars.com/FUZZ/AGAIN  -w list1.txt:FUZZ  -w list2.txt:AGAIN
</details>

-----------------------------------------------------------------------------


<details>
## <summary>Gather urls</summary>
    
    1- gather urls with katana
    # katana -list httpx.txt -o katana.txt
    2- gather urls with waybackurls
    # cat httpx.txt | waybackurls >> wayback.txt
    3-  use gospider 
    # gospider -S httpx.txt | sed -n 's/.*\(https:\/\/[^ ]*\)]*.*/\1/p' >> gospider.txt
    4- gather all files in one file and remove duplicate 
    # cat katana.txt wayback.txt gospider.txt >> urls.txt
    5- remove duplicate with anew 
    # cat urls.txt | anew >> allurls.txt 
    # rm urls.txt
    6- get javascript files in js.txt
    # cat allurls.txt | grep -E "\.js" >> js.txt
    7- get php files in php.txt
    # cat allurls.txt | grep -E "\.php$" >> php.txt
 </details>   
    	
-----------------------------------------------------------------------------
-----------------------------------------------------------------------------
-----------------------------------------------------------------------------


##### ASN number
    - https://bgp.he.net/
    -  whois -h whois.radb.net  -- '-i origin AS8983' | grep -Eo "([0-9.]+){4}/[0-9]+" | uniq -u > ip_ranges.txt
##### PTR (revrse DNS)
    - cat ip_anges.txt | mapcidr -silent | dnsx -ptr -resp-only -o ptr_recrds.txt
    - this step provide the host/domain name of ip's in the ip_range.txt 
