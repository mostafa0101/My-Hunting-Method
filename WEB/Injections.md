<details>
  <summary>XSS</summary>

    - Check for X-XSS-Protection header in the requset
    - 
    
    
    
    
    
    dalfox url "https://target.com/?q=search" -o dalfox_xss.txt
    dalfox file allParam.txt --waf-evasion --user-agent 'Mozilla/5.0 (x11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36' --proxy 'http://127.0.0.1:8080' --timeout 30 -b 'payload from xss.report' -o xssProbability.txt --deep-domxss 
    
    
    
    
    paramspider --domain domain.com
    paramspider --domain https://www.domain.com --exclude woff,css,png,svg,jpg --output t.txt
    
    echo "sub.domain.com" | waybackurls | httpx -silent | Gxss -c 100 -p Xss | sort -u | dalfox pipe
    
    
    cat domain.txt | kxss | grep "\" ' < >" | tee kxss.txt
    
    cat domain.txt | kxss
    
</details>

---------------------------------------------------------------------------------
<details>
  <summary>SQLi</summary>

</details>

---------------------------------------------------------------------------------
<details>
  <summary>SSTI</summary>

    inject {{2*2}} in username or email
    
</details>

