# Simple CTF - TryHackMe Writeup 🚩
**Platform:** [TryHackMe](https://tryhackme.com/room/easyctf)
**Difficulty:** Easy

## Answer the questions below
  **How many services are running under port 1000?** *[2]*
  
      ``` sudo nmap -sV -p 1-1001 10.112.129.59
          PORT   STATE SERVICE VERSION
          21/tcp open  ftp     vsftpd 3.0.3
          80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
          Service Info: OS: Unix ```


  **What is running on the higher port?** *[SSH]*
  
    ``` sudo nmap -sV -p- 10.112.129.59
        PORT     STATE SERVICE VERSION
        21/tcp   open  ftp     vsftpd 3.0.3
        80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
        2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
        Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel ```

  **What's the CVE you're using against the application?** *[CVE-2019–9053]*
  
     ``` Start Fuzz Dir , Found Dir name = Simple , after found the dir open site http://10.112.129.59/simple  , and see last page found version [by Made Simple Version 2.2.8]
         copy the version and search in google , what CVE "CMS 2.2.8"   
     
      ``` 

 **To what kind of vulnerability is the application vulnerable?** *[SQLI]*

 ###Now We Try Login About Way FTP :
            
