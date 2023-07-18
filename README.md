**Product:**                          ClusterControl 
 
**Manufacturer:**              Severalnines (https://severalnines.com/) 
 
**Version:**                          Controller: 1.9.0.4710, Frontend: 1.9.0.8008-#97ddd4 
 
**Vulnerability Type:**      Improper Authorization, Authenticated SQL Injection 
 
**Manufacturer Notification:**  8/9/2021 
 
**CVE Reference:**             TBD 



**Product Overview:**
The ClusterControl Community Edition is a free-to-use, all-in-one database management system that allows you to deploy and monitor the top open source database technologies like MySQL, MariaDB, Percona, MongoDB, PostgreSQL, Galera Cluster and more.

**Vulnerability Details:**
An authenticated SQL injection was detected within the “hostname” and “sender” parameters of the below request.  



Using the default configuration there are two levels of authentication available in the web ui, ‘admins’ and ‘users’.  The Post request below is supposed to only be available to the ‘admins’ level accounts.  However, when we replace the ‘admins’ cookies in the request with a ‘users’ cookies it still completes the request and the subsequent sql injection.
This allows a lower-level user to perform a sql injection through the web ui and elevate privileges by accessing all databases, etc.

```
POST /clustercontrol/access2/settings?clusterid=0&operation=set_mailserver HTTP/1.1
Host: x.x.x.x
Content-Length: 133
Accept: application/json, text/plain, */*
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.131 Safari/537.36
Content-Type: application/json;charset=UTF-8
Origin: http://x.x.x.x
Referer: http://x.x.x.x/clustercontrol/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: _ga=GA1.1.16598096.1628429909; _gid=GA1.1.2049508896.1628429909; PHPSESSID=redactednumbersletters; CakeCookie[expire]=August%2010%2C2021%2008%3A12%3A24; CakeCookie[clone_cluster_check]=N; CakeCookie[ping_home]=Y; _gat=1
Connection: close
{“smtp_server”:{“hostname”:”testhostname”,”password”:” testpassword “,”port”:356,”sender”:”testuser@test.com”,”use_tls”:false,”username”:”testuser”}}
```

I would like to congratulate Severalnines on their stellar time to fix with this issue.

-   08-08-2021: Vulnerability discovered
-   08-09-2021: Vulnerability reported to manufacturer
-   08-15-2021: Patch released by manufacturer
-   08-16-2021: Public disclosure of vulnerability
-   Who knows when: mitre fumble creation of cve number

