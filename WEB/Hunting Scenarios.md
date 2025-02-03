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

-----------------------------------------------------------------------------

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

-----------------------------------------------------------------------------


<details>
## <summary>login vulnerabilities </summary>

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

-----------------------------------------------------------------------------



  <details>
## <summary>reset password vulnerabilities</summary>
    
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
</details>

-----------------------------------------------------------------------------


<details>
## <summary>session vulnerabilities</summary>
  	
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
	
</details>

-----------------------------------------------------------------------------


<details>
	<summary>IDOR</summary>
	
    1- Look for id everywhere
    
    2- Play with hash/encoded values
    
    3- Change The ID's in the request 
    
    4- Upload the profile photo for another user
    
    5- Try change/View data of another user
    
    6- Do something with your email then change it in Burp

    7- Add parameter IDs to requests that don’t have them 

    8- Try replacing parameter names

    9- Try changing the requested file type 
    	GET /user_data/2341 --> 401 Unauthorized
	GET /user_data/2341.json --> 200 OK
    
    10- Try using an array {“id”:19} → {“id”:[19]}

    11- Wildcard ID /api/users/*

    12- check for session cookies if has httponly flag

    13- use the inspector of Burp Repeater to play with id's

    14- use https://jwt.io

    15- create two accounts and save both jwt data and try change between them

    16- detect each cookie and see where it being used

    17- Gather POST & GET and test every CRUD

    18- 

 
  
</details>

-----------------------------------------------------------------------------

<details>
	<summary>Broken Access Control</summary>

	1- Test some Graphql operations with different user roles and see what this operation do
 	2- Check the role of every user and try upgrade your role by urself
  	3- try any unauth behavior like :
   		- member delete admin
     		- member send invites using the invite request
       		- member outside the comapny try any action 
	 	- 
 
</details>

-----------------------------------------------------------------------------

<details>
	<summary>RCE</summary>

	1- Injection in json file 
 		{
   		   "username":" `touch ayfile.txt` ",
		   "password":"test"
		}
  	We establish a connection using ntcat then inject command in the json to get this connection
     --------------------------------------------------------------------------------------------------
     2- 

     
</details>

-----------------------------------------------------------------------------


<details>
	<summary>Logic Bugs</summary>
	
    1- Try change the price or quantity of item
    
    2- Multiple booking for one room
    
    3- Place order without verify stock level
    
    4- Use coupons or bounus more than one time
    
    5- Check the difference bettween Front-end & Burp request
    
    6- Try creating more than one from the same block 

    7- Check for all posible IF statements and try to bypass it

    8- A user gains access to restricted features they shouldn't have access to.

    9- Try access files after deletion using the link of this file 

    10- Make changes in the source code disabled -> enabled / hidden -> flex

    11- Delete comment with report https://shahjerry33.medium.com/business-logic-errors-a-new-look-3b18d9c2a12f

    12- 
      
		
</details>

-----------------------------------------------------------------------------


<details>
	<summary>Race Condition</summary>

    1- 
 
</details>

-----------------------------------------------------------------------------


<details>
	<summary>Rate Limit</summary>

 	rate limit 
	1- no rate limit on login page 
	2- no rate limit on internal password
	3- no rate limit on sending reset password link 
	4- no rate limit on OTP or 2FA => account takeover
	5- no rate limit on contact us page 
	6- no rate limit on comments 
	7- no rate limit on reports of comments
	8- no rate limit on port 22
 	9- no rate limit on create users account lead to massive accounts created
	
	------------
	bypass rate limit by adding headers 
	X-Forwarded-For: 127.0.0.1
	X-Forwarded-Host: 127.0.0.1
	X-Origination-IP: 127.0.0.1 or 0.0.0.0
	X-Fowarded-For: 127.0.0.1
	X-Remote-IP: 127.0.0.1
	X-Remote-Addr: 127.0.0.1
	------------------------------------------
	POST /login.php HTTP/1.1
	Host: target.com
	X-Forwarded-For: 127.0.0.1
	X-Forwarded-Host: 127.0.0.1
	X-Origination-IP: 127.0.0.1 or 0.0.0.0
	X-Fowarded-For: 127.0.0.1
	X-Remote-IP: 127.0.0.1
	X-Remote-Addr: 127.0.0.1
	
	username=admin&password=$fuzz$
	-------------------------------------------
	429 => 403 
	bypass rate limit 
	
	ffuf -u https://example.com -w wordlist.txt --data "username=admin&password=FUZZ"  -H "X-Forwarded-For: 127.0.0.1" -H "X-Forwarded-For: 127.0.0.1"`
	
	403 


</details>

-----------------------------------------------------------------------------


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

-----------------------------------------------------------------------------


<details>
## <summary>Javascript Analysis</summary>
    
    1- use mantra to get api , passwords , keys ...
     cat js.txt | mantra  | tee -a mantra.txt
    2- use nuclei to search for secrets 
     nuclei -l js.txt -t nuclei-templates/http/exposures/ -o nucleijs.txt
    
    if found google api key then use tool google.sh  and see if api valid or not
    google.sh AIz.............

	
 	- wayback
	- gospider
	- katana
	=> allurls.txt
	
	1- Use Mantra => for api keys
	
	2- Use jsluice => for secrets and urls =>  jsluice urls player.js
						     jsluice secrets player.js
	 for i in $(ls);do jsluice secrets $i;done
	
	3- Use nuclei  => nuclei-tempates/http/exposures/
	 nuclei -l js.txt -t /root/nuclei-templates/http/exposures/ -mhe 4
	4- analyze the code with js beaty in visual studio code 


</details>

-----------------------------------------------------------------------------


<details>
	<summary>PHP</summary>
</details>

-----------------------------------------------------------------------------


<details>
	<summary>2FA</summary>
			
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



<details>
## <summary>check sql injection in php</summary>
    
    1- first let's gather parameters 
    # arjun -i php.txt | tee -a parameters.txt
    2- after knowing parameters like id then full url would be 
    https://example.com/file.php?id=*
    3- use sqlmap 
    # sqlmap -u "~~https://example.com/file.php?id=*~~" --dbs --banner --batch --random-agent
    
 </details>   


-----------------------------------------------------------------------------


    
<details>
## <summary>SQLI</summary>

    id = 1'XOR(if(now()=sysdate(),sleep(2*2),0))OR'

</details>


-----------------------------------------------------------------------------

<details>
	<summary>XSS</summary>

 
	
	dalfox url "https://target.com/?q=search" -o dalfox_xss.txt
	dalfox file allParam.txt --waf-evasion --user-agent 'Mozilla/5.0 (x11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 			Safari/537.36' --proxy 'http://127.0.0.1:8080' --timeout 30 -b 'payload from xss.report' -o xssProbability.txt --deep-domxss 
	
	
	
	
	paramspider --domain domain.com
	paramspider --domain https://www.domain.com --exclude woff,css,png,svg,jpg --output t.txt
	
	echo "sub.domain.com" | waybackurls | httpx -silent | Gxss -c 100 -p Xss | sort -u | dalfox pipe
	
	
	cat domain.txt | kxss | grep "\" ' < >" | tee kxss.txt
	
	cat domain.txt | kxss
</details>

-----------------------------------------------------------------------------

<details>
	<summary>CSRF</summary>

	Generate POC using LazyCSRF in BurpSuite
	=================================================
	FIRST SCENARIO: 
  	1- Login as Attacker and intercept any function like change email, pass, logout...etc
   	2- Genereate CSRF poc with that reqeust
    	3- login as Victim in another browser
     	4- open the CSRF poc in victim browser if did the function then it's a bug
  	
   	=================================================
	SECOND SCENARIO: The Token is tied to non-session cookie
 		if the token tied to an attribute in the request 
 	1- intercept the request of user1 change email,username..etc
  	2- Genrate POC 
   	3- get the CSRF key and attribute value of user2
    	4- 

    	=================================================
   	- Remove the token and leave the parameter empty
  	- Try use another user CSRF token
   	- Change the request method to get and remove the token
    	- Add Ayhaga to the real CSRF token 
     	- Dynamic chars in CSRF token manipulate
	- try delete referrer
 	- Referrer: https://target.com/https://evil.com
  	

 
</details>



