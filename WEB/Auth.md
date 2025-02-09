<details> 
## <summary>signup vulnerabilities</summary>
    
    0- check in login page or register page http or https 
    (insecure data transfer ) 
    	-------------------------------------------------------------
    1- if there is no verification code or confirmation then 
    signup with admin@~~site.com~~ and report pre-account takeover vulnerability 
	-------------------------------------------------------------
    2- a- create account with hacker@gmail.com for example 
    	 b- confirmation will reach you 
    	 c- don't click on it 
    	 d- login to your account and change the email to victim@gmail.com 
    	 e- go back the link in step b and click on it 
    	 f- if the victim@gmail.com was verified successfully then 
    	 (misconfiguration lead to verification bypass  vulnerability) 
    	-------------------------------------------------------------
    3- while registertion put xss payloads inside username , name ....
        -------------------------------------------------------------
    4- create account with victim@gmail.com 
    	- don't verify the account and don't click on verification link 
    	- login to the site if you can 
    	- go to settings and see if there is 2 factor authentication 
    	- enable 2 factor authentication without confirming account 
    	- report vulenrability (enable 2fa without confirmaiton lead to pre-account tkaeover)
        -------------------------------------------------------------
    5- create account with victim@gmail.com ,  don't click on the link
    	- login to victim@gmail.com 
    	- change the email address to hacker@gmail.com 
    	- click on confimation link send to your email hacker@gmail.com 
    	- go back and change email to victim@gmail.com and observe it was verified succcessfully
    	(verification bypass )
       -------------------------------------------------------------
    6- Create account1 but don't verify
    	- Then create acount2 wiht the same email but different method like google login
     	-  See if can access any data
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
 	-Weak Password Policy	
	     - check if program accept 
		- weak passwords like 123456
		- username same as email address
		- password same as email address
		- improper implemented password reset and change features
	-------------------------------------------------------------
 	- 








  
  

 
      
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
     brute force otp 
    --------------------------------------
     reset password does not end live sessions 
    --------------------------------------
     	1- Open up Firefox and Burp Suite
	2- Visit the forgot password page 
	3- Enter the victim's email address and click Reset and Email Password
	4- Intercept the HTTP request in Burp Suite & change the Host Header to your malicious site / server.
    --------------------------------------
	- check if the password reset endpoint is vulnerable to IDOR
	-  check if the password reset endpoint is vulnerable to Host Header injection
 	- test for HTTP parameter Pollution (HPP)
    --------------------------------------
	- Test for SQLI in the reset pass send function
    
    --------------------------------------
		     
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
	<summary>2FA</summary>

	- Request a 2FA code from Attacker Account.
	- Use this valid 2FA code in the victim 2FA  Request and see if it bypass the 2FA Protection.
	 ----------------------------------------------------
	- After sumbit the verfiy code 
 	- Change the attacker cookie to victim-user cookie
	----------------------------------------------------
 	- Try Response & Status code manipulation 
  	- if "Success":"false" Change it to true
   	- if the response 4xx change it to 200 OK
	----------------------------------------------------
 	1. Request a 2FA code and use it
	2. Now, Re-use the 2FA code and if it is used successfully that's an issue.
	- Also, try requesting multiple 2FA codes and see if previously requested Codes expire or not when a new code is requested
	- Also, try to re-use the previously used code after long time duration say 1 day or more.
	----------------------------------------------------
 	- CSRF on 2FA disable feature
  	----------------------------------------------------
   	1. Directly Navigate to the page which comes after 2FA or any other authenticated page of the application.
	2. If there is no success, change the refer header to the 2FA page URL. This may fool  
	application to pretend as if the request came after satisfying 2FA Condition
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
	- Lack of rate limit re-sending the code via SMS
	----------------------------------------------------
 	- Try Play with session expire
	----------------------------------------------------
	- Create account without verify it and enable 2FA (Valid Bug)
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
