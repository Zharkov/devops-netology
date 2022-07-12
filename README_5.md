1) anton@anton-Extensa-2520G:~$ telnet stackoverflow.com 80
Trying 151.101.193.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: 835e7333-0981-4548-bb1a-735d6cde71d9
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Tue, 12 Jul 2022 19:24:19 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-bma1681-BMA
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1657653859.964576,VS0,VE102
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=eda15878-5e13-6197-3e7b-ae2a0406bd2c; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.


HTTP код 301 указывает на то что запрашиваемый ресурс был перемещенн

скриншот stackowerflow.jpg

2)

получили первый код HTTP 307 редиекрт с HTTP на HTTPS
самая долгая загрузка была обращение за документками к stackoverflow.com и заняло 545 ms
общее время загрузки 1.35 s
 

3) 
anton@anton-Extensa-2520G:~$  wget -qO- eth0.me
95.29.138.20

4)
anton@anton-Extensa-2520G:~$ whois 95.25.138.20
% This is the RIPE Database query service.
% The objects are in RPSL format.
%
% The RIPE Database is subject to Terms and Conditions.
% See http://www.ripe.net/db/support/db-terms-conditions.pdf

% Note: this output has been filtered.
%       To receive output for a database update, use the "-B" flag.

% Information related to '95.24.0.0 - 95.30.255.255'

% Abuse contact for '95.24.0.0 - 95.30.255.255' is 'abuse-b2b@beeline.ru'

inetnum:        95.24.0.0 - 95.30.255.255
netname:        BEELINE-BROADBAND
descr:          Dynamic IP Pool for broadband customers
country:        RU
admin-c:        CORB1-RIPE
tech-c:         CORB1-RIPE
status:         ASSIGNED PA
mnt-by:         RU-CORBINA-MNT
created:        2010-05-12T10:14:50Z
last-modified:  2011-10-24T07:14:07Z
source:         RIPE

role:           CORBINA TELECOM Network Operations
address:        PAO Vimpelcom - CORBINA TELECOM/Internet Network Operations
address:        111250 Russia Moscow Krasnokazarmennaya, 12
phone:          +7 495 755 5648
fax-no:         +7 495 787 1990
remarks:        -----------------------------------------------------------
remarks:        Feel free to contact Corbina Telecom NOC to
remarks:        resolve networking problems related to Corbina
remarks:        -----------------------------------------------------------
remarks:        User support, general questions: support@corbina.net
remarks:        Routing, peering, security: corbina-noc@beeline.ru
remarks:        Report spam and abuse: abuse@beeline.ru
remarks:        Mail and news: postmaster@corbina.net
remarks:        DNS: hostmaster@corbina.net
remarks:        Engineering Support ES@beeline.ru
remarks:        -----------------------------------------------------------
admin-c:        SVNT1-RIPE
tech-c:         SVNT2-RIPE
nic-hdl:        CORB1-RIPE
mnt-by:         RU-CORBINA-MNT
abuse-mailbox:  abuse-b2b@beeline.ru
created:        1970-01-01T00:00:00Z
last-modified:  2022-05-11T13:21:44Z
source:         RIPE # Filtered

% Information related to '95.25.138.0/24AS8402'

route:          95.25.138.0/24
descr:          RU-CORBINA-BROADBAND-POOL1
origin:         AS8402
mnt-by:         RU-CORBINA-MNT
created:        2011-04-28T08:54:14Z
last-modified:  2011-04-28T08:54:14Z
source:         RIPE # Filtered


5)
anton@anton-Extensa-2520G:~$ traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  192.168.0.1 [*]  3.214 ms  3.149 ms  3.096 ms
 2  95.29.128.1 [AS8402]  6.488 ms  6.765 ms  7.017 ms
 3  * * *
 4  81.211.29.30 [AS3216]  7.123 ms  7.393 ms  7.638 ms
 5  79.104.235.213 [AS3216]  12.874 ms  13.501 ms  13.070 ms
 6  72.14.213.116 [AS15169]  29.116 ms 81.211.29.103 [AS3216]  9.244 ms 194.186.131.42 [AS3216/AS23649]  10.021 ms
 7  * * 108.170.250.130 [AS15169]  9.928 ms
 8  72.14.234.20 [AS15169]  20.358 ms 108.170.227.82 [AS15169]  9.263 ms 209.85.249.158 [AS15169]  27.821 ms
 9  142.250.235.74 [AS15169]  31.202 ms 108.170.250.66 [AS15169]  10.175 ms *
10  142.250.239.64 [AS15169]  22.176 ms 142.250.238.214 [AS15169]  24.907 ms 172.253.64.113 [AS15169]  33.970 ms
11  * * 209.85.254.20 [AS15169]  30.761 ms
12  * 72.14.235.193 [AS15169]  27.004 ms 216.239.58.65 [AS15169]  33.567 ms
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * 8.8.8.8 [AS15169]  30.801 ms *

6)

большая задержка на AS8402 

7)
;; ANSWER SECTION:
dns.google.		2873	IN	A	8.8.8.8
dns.google.		2873	IN	A	8.8.4.4

8)

8.8.8.8.in-addr.arpa.	10516	IN	PTR	dns.google.
4.4.8.8.in-addr.arpa.	20929	IN	PTR	dns.google.
