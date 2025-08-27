# Rapport de test website sam.condor.dz



### NMAP SCAN 



```

nmap -sV -Pn 10.6.1.67 -p- -vvv

Starting Nmap 7.95 ( https://nmap.org ) at 2025-08-27 09:42 CET

NSE: Loaded 47 scripts for scanning.

Initiating Parallel DNS resolution of 1 host. at 09:42

Completed Parallel DNS resolution of 1 host. at 09:42, 0.00s elapsed

DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 2, OK: 1, NX: 0, DR: 0, SF: 0, TR: 1, CN: 0]

Initiating SYN Stealth Scan at 09:42

Scanning dzcesvab03002.condor.com (10.6.1.67) [65535 ports]

Discovered open port 3389/tcp on 10.6.1.67

Discovered open port 22/tcp on 10.6.1.67

Discovered open port 80/tcp on 10.6.1.67

Discovered open port 443/tcp on 10.6.1.67

SYN Stealth Scan Timing: About 20.01% done; ETC: 09:44 (0:02:04 remaining)

Discovered open port 13980/tcp on 10.6.1.67

SYN Stealth Scan Timing: About 48.42% done; ETC: 09:44 (0:01:05 remaining)



```

### Discovered open port 

22 ssh

80 http

443 https

3389 XRDP < linux


## version ssh vulnerable


<img width="870" height="683" alt="image" src="https://github.com/user-attachments/assets/200d9a96-ac84-4eed-8892-a597b81d6a0a" />


## xrdp open 

<img width="1032" height="799" alt="image" src="https://github.com/user-attachments/assets/98b4089c-6cc7-4ac1-b72f-2a6ef2eba9f6" />



## Web Exploitation

### Web enumerarion 

<img width="899" height="901" alt="image" src="https://github.com/user-attachments/assets/a8088084-e96c-45ec-894d-78a8b319f16d" />

### I focused only on the API and scripts paths. 

After downloading the files from these paths, I discovered interesting files such as id_rsa and some bash scripts. 


## Script path
<img width="1006" height="905" alt="image" src="https://github.com/user-attachments/assets/8a16485c-1262-46ac-acbc-66f23fb101fe" />



<img width="971" height="689" alt="image" src="https://github.com/user-attachments/assets/482a2031-0a3e-4930-92b6-a9254456e91c" />


after reading some file

there is leaking of information username email address ip ....




<img width="1178" height="721" alt="image" src="https://github.com/user-attachments/assets/baf1bece-1b89-4e33-9d15-37ead3981e8e" />




## Exploitation 





since i have a id_rsa and some ip address from files i tested id_rsa and i got access to the server as root



<img width="804" height="297" alt="image" src="https://github.com/user-attachments/assets/844f3867-616b-4ad0-a5a7-e798448cd5e3" />





## Results



since i got access to one server i stop the test, 

please you can proceed to close all of this paths and remove id_rsa from the path and we can move to test with credentials.

