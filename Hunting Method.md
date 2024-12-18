<details>
 <summary> Subdomain enumeration </summary>
    
     https://securitytrails.com/
    
    https://subdomainfinder.c99.nl/
    
    https://shrewdeye.app/ 
    
    
    # subfinder -d ~~mars.com~~ -all --recursive  -o subs.txt
  
    
   
    # echo ~~mars.com~~ | assetfinder --subs-only >> subs.txt
    
    
    after collecting all subdomains in subs.txt then let's remove duplicate 
    # cat subs.txt | anew >> allsubs.txt
    # rm subs.txt
</details>

<details> 
## <summary>signup vulnerabilities</summary>
    
    0- check in login page or register page http or https 
    (insecure data transfer ) 
    
    1- if there is no verification code or confirmation then 
    signup with admin@~~site.com~~ and report pre-account takeover vulnerability 
    
    2- a- create account with hacker@gmail.com for example 
    	 b- confirmation will reach you 
    	 c- don't click on it 
    	 d- login to your account and change the email to victim@gmail.com 
    	 e- go back the link in step b and click on it 
    	 f- if the victim@gmail.com was verified successfully then 
    	 (misconfiguration lead to verification bypass  vulnerability) 
    
    3- while registertion put xss payloads inside username , name ....
    
    4- create account with victim@gmail.com 
    	- don't verify the account and don't click on verification link 
    	- login to the site if you can 
    	- go to settings and see if there is 2 factor authentication 
    	- enable 2 factor authentication without confirming account 
    	- report vulenrability (enable 2fa without confirmaiton lead to pre-account tkaeover)
    
    5- create account with victim@gmail.com ,  don't click on the link
    	- login to victim@gmail.com 
    	- change the email address to hacker@gmail.com 
    	- click on confimation link send to your email hacker@gmail.com 
    	- go back and change email to victim@gmail.com and observe it was verified succcessfully
    	(verification bypass )
    	 
</details>

<details>
## <summary>login vulnerabilities </summary>

    ```
	 1- login over http not https 	( insecure data transfer )
	
	 3- try default credentials (test:test) (admin:admin) (admin:password) (kali:kali) (admin:123)
	  (admin:default) (root:root) (root:toor) (admin:kali) (kali:root) (admin:123456789)
	
	 4- try to inject sql injection in username as admin' or 1=1; -- -
	
	 5- try to make response manipulation  to bypass login page
	
	 6- use the request and send it to sqlmap to test if there is sql injection or not
	
	 7- try to inject xss payloads in username as <svg/onload=confirm()>
	
	 8- try to inject template injection inside username as {{9*9}} and if printed 81 then vulnerable to template injection
	
	 9- view source code of the page from CTRL+U to see if leaked credentials

 </details>


  <details>
## <summary>reset password vulnerabilities</summary>
    
    ```
    check link of reset password in email if http not https
    check reset request code can be leaked in request or response
    no rate limit (Email bombing)
    ------------------------------------
    1- ask reset password (from out) don’t press on it ⇒ 
    2- login to account ⇒ change the email and verify ⇒ click on reset link
    3- if password changed through reset password link (bug)
     -----------------------------------
    1- ask reset password (from out) don’t press on it ⇒
    2- login to account ⇒ change the password ⇒
    3- click on reset link ⇒ if password changed through reset password link (bug)
    --------------------------------------
    1- reset the password or ask for reset code  
    2- don't click or reload the page but go to /profile or /account
     directly and see if you can access
     -------------------------------------
     brute force otp 
     --------------------------------------
     reset password does not end live sessions 
     
     
    ```
</details>

<details>
## <summary>session vulnerabilities</summary>
  	```
	
	1- login to your account with firefox and chrome
		- change the password in firefox 
		- observe the account in chrome is still logged in and didn't logout
		- Broken session Management 
	
	2- login to your account with firefox and chrome 
		- enable 2FA in firefox 
		- reload the page in chrome and observe session is still valid 
	
	3- login to your account and update anything 
		-  intercept the request with burpsuite 
		- send the request to repeater
		- logout from your account 
		- use the request in repater to update and if still valid  (vulnerability)
	
	4- ask for reset password 
		- don't click on the link reached you 
		- login with your username and password 
		- change the password of the email 
		- logout from your account and then use the link in step 1 
		- if still valid then (Vulnerability)
	
	5-logout from your account 
		- click on (Alt+Left-arrow) button or <--
		- observe the session and profile data is still found 
		- broken cache vulnerability
	
	6- when updating email address 
		- check if OTP is sent to existing email not the new email 
		- broken function lead to verification bypass
	
	7- create account with email A => victim 
		- update the email to B => hacker then verify it -> vierfy your account 
		- update email back to A => victim 
		- if shown as verified then vulnerability 
	
	8- verifiaction bypass 
		- account with victim@gmail.com => don't verify it 
		- update account email to hacker@gmail.com
		- once you clicked the link , if verified victim@gmail.com then vuln  
	```
</details>

<details>
	<summary>RCE</summary>
</details>


<details>
	<summary>Broken Access Control</summary>
</details>


<details>
	<summary>Logic Bugs</summary>
	
    1- Try change the price or quantity of item
    
    2- Multiple booking for one room
    
    3- Place order without verify stock level
    
    4- Use coupons or bounus more than one time
    
    5- Check the difference bettween Front-end & Burp request
    
    6- 
      
		
</details>


<details>
## <summary>hacking WordPress</summary>
    
    
    wpscan --url [https://target.com](https://target.com/) --disable-tls-checks --api-token zBsi404GGCMKGzTraiEsSsQsFXCsUVWmaDUsn3EPuKc -e at -e ap -e u --enumerate ap --plugins-detection aggressive --force
    wordpress usernames exposure :
    /wp-json/wp/v2/users
    /author-sitemap.xml
    /wp-content/debug.log
    /wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd
    	
    /wp-login.php?action=register
    /wp-json/?rest_route=/wp/v2/users/
    /wp-json/?rest_route=/wp/v2/users/n

</details>

<details>
## <summary>Javascript Analysis</summary>
    
    1- use mantra to get api , passwords , keys ...
    # cat js.txt | mantra  | tee -a mantra.txt
    2- use nuclei to search for secrets 
    # nuclei -l js.txt -t nuclei-templates/http/exposures/ -o nucleijs.txt
    
    if found google api key then use tool google.sh  and see if api valid or not
    # google.sh AIz.............
</details>

<details>
	<summary>PHP</summary>
</details>

<details>
	<summary>2FA</summary>
		```
			
		1- check 000000 - 123456
		2- check null 
		3- reuse previous OTP	(used one )
		4- reuse code of another account (valid)
		5- No rate limit on 2FA	=>> 
		6- check if exposed code in response
		7- bypass it by reset password link
			- enable 2fa 
			-  logout 
			- reset password => then click on the link 
			- if you got into directly then vulnerability 
		
		8- bypass it by 0-auth google 	=> 2fa 
			1- login 
			2- enable 2fa 
			3- login with google => if you got into directly then (vulnerability) 
		
		9- No rate limit on sending 2FA 
		10- response manipulation => 403 Forbidden => 200 OK 
						false 	=> true
						0	=> 1
						failed 	=> successful 
		11- bypass 2fa by the next step 
		
		12- enable 2fa without email verification lead to pre-account takeover
		13- enabling 2fa does not end another sessions 
		change password 
		```
</details>


<details>
<summary>  Subdomain takeover </summary>
    
    # subzy run --targets subs.txt --hide_fails --vuln  | grep -v -E "Akamai|xyz|available|\-"
    if you found any vulnerability then search on how to takeover subdomain 
</details>
    
  <details>       
## <summary>httpx</summary>
    
    to see the working sites 
    # cat allsubs.txt | httpx -o httpx.txt
    # cat httpx.txt | httpx -mc 200 -o httpx200.txt    
    1- use smuggler to check request smuggling vulnerablitiy 
    # cat httpx.txt | smuggler.py | tee -a smuggler.txt
</details>

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
    	


<details>
## <summary>check sql injection in php</summary>
    
    1- first let's gather parameters 
    # arjun -i php.txt | tee -a parameters.txt
    2- after knowing parameters like id then full url would be 
    https://example.com/file.php?id=*
    3- use sqlmap 
    # sqlmap -u "~~https://example.com/file.php?id=*~~" --dbs --banner --batch --random-agent
    
 </details>   


    
<details>
## <summary>sqlinjection</summary>

    id = 1'XOR(if(now()=sysdate(),sleep(2*2),0))OR'

</details>

