<details>
  <summary>smb share enum</summary>

    TOOLS
      - nmap , smbclient , enum4linux
      - nmap -p 139,445 --script smb-enum-shares,smb-enum-users 10.10.10.1
      - smbclient -L \\10.10.10.1 -N >> display the files shared between employees
      - mount.cifs //10.10.10.1/smbshare /home/kali user=,pass= >> downloading shared files
    
      - enum4linux  
      
      * if the file has $ then it's for the admin only 
      
</details>

----------------------------------------------------------------------------

#### Brute Force with hydra 
