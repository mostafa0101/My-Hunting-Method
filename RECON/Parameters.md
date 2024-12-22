<details>
  <summary>Arjun</summary>

    arjun -u "https://target.com" -m get --stable |anew arjunParam.txt
    
    arjun -i hiddenFiles.txt -t 10 -c 300 -T 30 -d 10 -oB 127.0.0.1:8080 -m POST -oT hiddenParam1.txt
    
    arjun -i allURLs.txt -t 10 -c 300 -T 30 -d 10 -oB 127.0.0.1:8080 -m POST -oT hiddenParam2.txt

</details>

--------------------------------------------------------------------------------------

ffuf -u https://target.com/page.php?FUZZ=test -w /mnt/CyberSecurity/SecLists/Discovery/Web-Content/url-params_from-top-55-most-popular-apps.txt |anew ffufParam.txt

cat ffufParam.txt arjunParam.txt |anew allHidenParam.txt


