
<details>
  <summary>dirsearch</summary>

    dirsearch -w /mnt/CyberSecurity/My-Cool-WordList-For-Fuzz-and-Bugs/wordlists/params.txt --full-url --random-agent -x 404,400 -e php,html,js,json,ini -u https://target.com/ |anew dirsearchURLs.txt
    dirsearch -e php,asp,aspx,jsp,py,txt,conf,config,bak,backup,swp,old,db,sql,asp,aspx,asp~,py~,rb,rb~,php~,bak,bkp,cache,cgi,conf,csv,html,inc,jar,js,json,jsp~,lock,log,rar,old,sql.gz,sql.zip,sql.tar.gz,sql~,swp~,tar,tar.bz2,tar.gz,txt,wadl,zip -i 200 --full-url --deep-recursive -w /mnt/CyberSecurity/My-Cool-WordList-For-Fuzz-and-Bugs/wordlists/params.txt --exclude-subdirs .well-known/,wp-includes/,wp-json/,faq/,Company/,Blog/,Careers/,Contact/,About/,IMAGE/,Images/,Logos/,Videos/,feed/,resources/,banner/,assets/,css/,fonts/,img/,images/,js/,media/,static/,templates/,uploads/,vendor/ --exclude-sizes 0B --skip-on-status 429 --random-agent -u https://target.com/ |anew dirsearchURLs2.txt
    dirsearch -u https://domain.com/ -e 'conf,config,bak,backup,smp,old,db,sql,asp,aspx,py,radl,zip,xml,swp,x~,asp~,py~,rb~,php~,bkp,jsp~,rar,gz,sql~,swp~,wdl,env,ini' --full-url -delay=10 --timeout=30 -p 127.0.0.1:8080 --random-agent -t 100 -w ~/SecLists/Discovery/Web-Content/combined_words.txt -o hiddenFiles.txt # turn on burpsuite to crawl  
</details>

---------------------------------------------------------------------------------------

<details>
  <summary>ffuf</summary>

    ffuf -w /usr/share/wordlists/custom.txt -t 75 -ac -mc 200,405,401,415,302,301 -u http://assets.engage.tesla.com/FUZZ |anew ffufURLs.txt
    ffuf -u https://www.example.com/FUZZ -w wordlist/Seclists/Discovery/Web-content/raft-medium-files.txt -mc 200,302,301 -t 1000 |anew ffufURLs2.txt
      
      to fuzz in two places with two files 
     ffuf -u https://mars.com/FUZZ/AGAIN  -w list1.txt:FUZZ  -w list2.txt:AGAIN
</details>

----------------------------------------------------------------------------------------

paramspider -d domain.com

gau target.com | anew gauURLs.txt

waybackurls target.com | anew waybackURLs.txt

katana -list allLiveSubdomains.txt -silent -o katanaCrawlURLs.txt

katana -passive -pss waybackarchive,commoncrawl,alienvault -f qurl -u target.com | anew katanaURLs.txt

gospider -s https://target.com -d 1 -o gospiderCrawlURLs.txt


##### Getting parameters from live urls :-
grep -E '\?.*=' allURLs.txt |anew allParamters.txt
##### cat allURLs.txt | grep "=" |anew allParamters.txt



