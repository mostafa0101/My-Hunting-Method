
gau https://example.com --threads 5 --o gau.txt 
cat gau.txt | grep ".js" > trgtJS.txt

python3 ~/JSFinder/JSFinder.py -f trgtJS.txt

python3 ~/SecretFinder/SecretFinder.py -i trgtJS.txt





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


