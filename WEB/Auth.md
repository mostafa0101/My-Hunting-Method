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

