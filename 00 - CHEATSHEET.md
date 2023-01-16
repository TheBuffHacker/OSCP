# **OSCP Cheatsheet**
#### High Level Methodology
*create a folder for that box: ie THM > GameZone*
*save your scans and captured information*
1. Active Recon
	1. [[nmap]]: quick and full 
		1. `nmap -vvv <IP> | tee -a nmap.quick`
		 2. `nmap -A -T4 -p- 10.10.175.200 | tee -a nmap.full`
	1. if webserver, gobuster scan, then investigate website
		1. `gobuster dir -u http://10.10.175.200/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt | tee -a gobuster`
		2. Visit website and click around (wappalyzer):
			1. Find login forms, comments, upload, view page source
			2. Burp

*Note: As you discover additional web URLs, re-enumerate that new directory to potentially web directories off that*

*If you have a payload that doesn't work, try the other type of payload so maybe a staged and non-staged payload*


- [SQLi](/SQLi.md)
- [[nmap]]
- [[Passwords and Hashes]]
- [[Shells and Payloads]]
