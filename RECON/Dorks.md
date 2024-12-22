# Main Google dorks helper
### https://dorks.faisalahmed.me/
--------------------------------------------------------------

 <details>
  <summary>Google Dorks</summary>

          site:blob.core.windows.net "example.com"

          site:googleapis.com "example.com"
          
          site:drive.google.com "example.com"
          
          site:dev.azure.com "example[.]com"
          
          site:onedrive.live.com "example[.]com"
          
          site:digitaloceanspaces.com "example[.]com"
          
          site:sharepoint.com "example[.]com"
          
          site:dropbox.com/s "example[.]com"
          
          site:box.com/s "example[.]com"
          
          site:docs.google.com inurl:"/d/" "example[.]com"
          
          site:firebaseio.com "example[.]com"

          site:*.gapinc.com inurl:”*admin | *login” | inurl:.php | .asp

          intext:"index of /.git"

          site:domain.com ext:xls

          site:domain.com ext:xlsx

  
</details>

---------------------------------------------------------------------------------------

### Config files
site:target.com ext:xml | ext:conf | ext:cnf | ext:reg | ext:inf | ext:rdp | ext:cfg | ext:txt | ext:ora | ext:env | ext:ini
### GitLab/GitHub/Bitbucket
site:github.com | site:gitlab.com | site:bitbucket.org "company"
### Database files
site:target.com ext:sql | ext:dbf | ext:mdb
### Backup files
site:target.com ext:bkf | ext:bkp | ext:bak | ext:old | ext:backup
### .git folder
inurl:"/.git" target.com -github
### Exposed documents
site:target.com ext:doc | ext:docx | ext:odt | ext:pdf | ext:rtf | ext:sxw | ext:psw | ext:ppt | ext:pptx | ext:pps | ext:csv
### Other files
site:target.com intitle:index.of | ext:log | ext:php intitle:phpinfo "published by the PHP Group" | inurl:shell | inurl:backdoor | inurl:wso | inurl:cmd | shadow | passwd | boot.ini | inurl:backdoor | inurl:readme | inurl:license | inurl:install | inurl:setup | inurl:config | inurl:"/phpinfo.php" | inurl:".htaccess" | ext:swf
### Login pages
site:target.com inurl:signup | inurl:register | intitle:Signup
### Wordpress files
site:target.com inurl:wp-content | inurl:wp-includes
### Linkedin employees
site:linkedin.com employees target.com

-----------------------------------------------------------------------------------

#### SQL errors
site:target.com intext:"sql syntax near" | intext:"syntax error has occurred" | intext:"incorrect syntax near" | intext:"unexpected end of SQL command" | intext:"Warning: mysql_connect()" | intext:"Warning: mysql_query()" | intext:"Warning: pg_connect()"
#### PHP errors
site:target.com "PHP Parse error" | "PHP Warning" | "PHP Error"
#### Open redirects
site:target.com inurl:redir | inurl:url | inurl:redirect | inurl:return | inurl:src=http | inurl:r=http
#### Sub-subdomains
site:*.*.target.com


<details>
  <summary>EXTRA</summary>

      inurl:example.com intitle:"index of"
      inurl:example.com intitle:"index of /" "*key.pem"
      inurl:example.com ext:log
      inurl:example.com intitle:"index of" ext:sql|xls|xml|json|csv
      inurl:example.com "MYSQL_ROOT_PASSWORD:" ext:env OR ext:yml -git
      inurl:example.com intitle:"index of" "config.db"
      inurl:example.com allintext:"API_SECRET*" ext:env | ext:yml
      inurl:example.com intext:admin ext:sql inurl:admin
      inurl:example.com allintext:username,password filetype:log
      site:example.com "-----BEGIN RSA PRIVATE KEY-----" inurl:id_rsa

</details>
