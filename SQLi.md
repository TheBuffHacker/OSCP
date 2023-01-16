==sqlmap==
- save a request from burp to use in sqlmap such as request.txt
- `sqlmap -r request.txt --dbms=mysql --dump`
	- dump attemps to output entire database and get table names, users and passwords to crack
- 