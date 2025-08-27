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

```
python CVE-2024-6387.py scan -T 10.6.1.67 -p 22 
                                                     
   .aMMMb  dMMMMb  dMMMMMP dMMMMb  .dMMMb  .dMMMb  dMP dMP 
  dMP"dMP dMP.dMP dMP     dMP dMP dMP" VP dMP" VP dMP dMP  
 dMP dMP dMMMMP" dMMMP   dMP dMP  VMMMb   VMMMb  dMMMMMP   
dMP.aMP dMP     dMP     dMP dMP dP .dMP dP .dMP dMP dMP    
VMMMP" dMP     dMMMMMP dMP dMP  VMMMP"  VMMMP" dMP dMP 

   ReggreSSHion CVE-2024-6387 Vulnerability Checker / Exploiter
   2.0 - Optimized by @Kz
    

🚨Servers likely vulnerable: 1
   [+] Server at 10.6.1.67 (N/A):22 (running SSH-2.0-OpenSSH_8.7)

🛡 Servers not vulnerable: 0

🛡 Servers likely not vulnerable (possible LoginGraceTime remediation): 0

⚠ Servers with unknown SSH version: 0

Summary:

📊 Total scanned hosts: 1

🚨 Total vulnerable hosts: 1

🛡  Total not vulnerable hosts: 0

🛡  Total likely not vulnerable hosts: 0

⚠  Total unknown hosts: 0

🔒 Servers with port 22 closed: 0

```


## xrdp open 
![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/74853138/482578961-2f8fce38-d3d0-4a51-872e-48a9c63fe121.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250827%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250827T091118Z&X-Amz-Expires=300&X-Amz-Signature=535817948c8093d80d88df1407f659cf36bdd3bfde50c3dadbe757cb273dd061&X-Amz-SignedHeaders=host)


## Web Exploitation

### Web enumerarion 

```
Target: http://sam.condor.dz/

[09:47:08] Starting: 
[09:47:19] 200 -    4KB - /api/
[09:47:20] 200 -  881B  - /assets/
[09:47:21] 200 -    1KB - /build/
[09:47:23] 200 -   70B  - /composer.json
[09:47:23] 200 -   23KB - /composer.lock
[09:47:24] 200 -    3KB - /cron/
[09:47:24] 200 -  925B  - /data/
[09:47:25] 200 -    1KB - /dist/
[09:47:29] 200 -   36KB - /header
[09:47:29] 200 -   36KB - /header.php
[09:47:30] 200 -   15KB - /images/
[09:47:30] 200 -    6KB - /includes/
[09:47:33] 200 -    5KB - /logs/
[09:47:40] 200 -   13KB - /plugins/
[09:47:44] 200 -    9KB - /scripts/
[09:47:45] 200 -  907B  - /setup/
[09:47:49] 200 -   80KB - /test
[09:47:49] 200 -   80KB - /test.php
[09:47:49] 200 -   80KB - /test/
[09:47:49] 200 -   80KB - /test/reports
[09:47:49] 200 -   80KB - /test/tmp/
[09:47:49] 200 -   80KB - /test/version_tmp/
[09:47:52] 200 -    2KB - /vendor/
[09:47:52] 200 -    0B  - /vendor/autoload.php
[09:47:52] 200 -    0B  - /vendor/composer/autoload_psr4.php
[09:47:52] 200 -    0B  - /vendor/composer/autoload_namespaces.php
[09:47:52] 200 -    0B  - /vendor/composer/autoload_real.php
[09:47:52] 200 -    0B  - /vendor/composer/autoload_static.php
[09:47:52] 200 -    0B  - /vendor/composer/autoload_classmap.php
[09:47:52] 200 -   24KB - /vendor/composer/installed.json
[09:47:52] 200 -    0B  - /vendor/composer/ClassLoader.p

```

### I focused only on the API and scripts paths. 
After downloading the files from these paths, I discovered interesting files such as id_rsa and some bash scripts. 


![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/74853138/482579020-ffc949a6-02c0-4348-8afb-5adf5dc30929.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250827%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250827T091205Z&X-Amz-Expires=300&X-Amz-Signature=f4e2e07b5b0f63462a7b08f02df10b5bcee0e0982dee236764082a46075a4e5a&X-Amz-SignedHeaders=host)

## Script path


![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/74853138/482579031-c6ad3b35-2dc9-4eb8-8dbe-50ea0cb1c355.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250827%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250827T091240Z&X-Amz-Expires=300&X-Amz-Signature=03c435a96e772cad053596c29b8f331514ddefd7b2f0a61fda18d53d8e84bd43&X-Amz-SignedHeaders=host)

after reading some file
there is leaking of information username email address ip ....

![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/74853138/482579052-f3f95b2e-ae5c-43ba-8384-83fe2441a20b.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250827%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250827T091306Z&X-Amz-Expires=300&X-Amz-Signature=00f60cd2d12a926bc3cf8132d915052d8891b9e4068cf965c37ae935eb486c3d&X-Amz-SignedHeaders=host)


## Exploitation 


since i have a id_rsa and some ip address from files i tested id_rsa and i got access to the server as root

![alt text](https://github-production-user-asset-6210df.s3.amazonaws.com/74853138/482579064-a90c4d29-db09-4245-9723-c912a607d5d4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250827%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250827T091413Z&X-Amz-Expires=300&X-Amz-Signature=cb4df3d92b4a8a7c415dfb100c9644188b58fd5e3b01a363ab1aa83d94e3fba4&X-Amz-SignedHeaders=host)


## Results

since i got access to one server i stop the test, 
please you can proceed to close all of this paths and remove id_rsa from the path and we can move to test with credentials.

