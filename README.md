# BeyondMachines
## Second Phase of Application for BeyondMachines Internship

---

### Задача 1  
**Пасивен скен на доменот `beyondmachines.net`, и пронаоѓање на колку DNS записи има во него.**

Извршен е пасивен скен на доменот со помош на следниве алатки:

- [Subdomain Finder Scan (15 May 2025)](https://subdomainfinder.c99.nl/scans/2025-05-15/beyondmachines.net)
- [CRT.sh Certificate Transparency](https://crt.sh/?q=%25.beyondmachines.net)

Опис:

- Во првиот скен, пасивно се скрејпирани и побарани SSL/TLS сертификати за `subдомените`.
- Вториот алат (сличен на `subfinder` и `amass`) собира `subдомени` од пасивни извори: search engines, CT логови и DNS историја.
- Дополнително беа користени Kali алатки: `subfinder`, `sublist3r`, `dnsrecon`, `amass`.

### Резултати:

BeyondMachines има **13 subдомени**, од кои:

- 5 имаат IP адреси.
- 1 subдомен има **Cloudflare заштита**.

**Активни subдомени:**

- `challenge.beyondmachines.net` → IP адреса и хостиран  
- `old.beyondmachines.net` → активен, потенцијално ризичен  
- `trust.beyondmachines.net` → активен, Cloudflare заштита  
- `beyondmachines.net` → активен  
- `yieldcat.beyondmachines.net` → активен

---

### Дополнителен скен во Kali виртуелна машина:

```bash
┌──(kali㉿kali)-[~] 
└─$ subfinder -d beyondmachines.net -o subfinder_results.txt

[INF] Current subfinder version v2.6.0 (outdated) 
[INF] Loading provider config from the default location: /home/kali/.config/subfinder/provider-config.yaml 
[INF] Enumerating subdomains for beyondmachines.net

 
┌──(kali㉿kali)-[~] 
└─$ ping -c 1 yieldcat.beyondmachines.net 
PING yieldcat.beyondmachines.net (216.24.57.1) 56(84) bytes of data. 
64 bytes from 216.24.57.1: icmp_seq=1 ttl=51 time=47.6 ms 
 
--- yieldcat.beyondmachines.net ping statistics --- 
1 packets transmitted, 1 received, 0% packet loss, time 0ms 
rtt min/avg/max/mdev = 47.550/47.550/47.550/0.000 ms 
                                                                                                                                                                 
┌──(kali㉿kali)-[~] 
└─$ whois 216.24.57.1 
NetRange:       216.24.57.0 - 216.24.57.255 
CIDR:           216.24.57.0/24 
NetName:        RS-1125 
NetHandle:      NET-216-24-57-0-1 
Parent:         NET216 (NET-216-0-0-0-0) 
NetType:        Direct Allocation 
OriginAS:        
Organization:   Render (RS-1125) 
RegDate:        2019-01-28 
Updated:        2024-02-05 
Ref:            https://rdap.arin.net/registry/ip/216.24.57.0 
 
 
OrgName:        Render 
OrgId:          RS-1125 
Address:        525 Brannan St, Ste 300 
City:           San Francisco 
StateProv:      CA 
PostalCode:     94107 
Country:        US 
RegDate:        2018-12-21 
Updated:        2024-02-06 
Ref:            https://rdap.arin.net/registry/entity/RS-1125 
 
 
OrgTechHandle: RAC91-ARIN 
OrgTechName:   Render ARIN Contact 
OrgTechPhone:  +1-415-980-3185  
OrgTechEmail:  arin-contact@render.com 
OrgTechRef:    https://rdap.arin.net/registry/entity/RAC91-ARIN 
 
OrgAbuseHandle: RAC90-ARIN 
OrgAbuseName:   Render Abuse Contact 
OrgAbusePhone:  +1-415-980-3185  
OrgAbuseEmail:  abuse@render.com 
OrgAbuseRef:    https://rdap.arin.net/registry/entity/RAC90-ARIN 
 
OrgNOCHandle: RAC91-ARIN 
OrgNOCName:   Render ARIN Contact 
OrgNOCPhone:  +1-415-980-3185  
OrgNOCEmail:  arin-contact@render.com 
OrgNOCRef:    https://rdap.arin.net/registry/entity/RAC91-ARIN 
 
Subdomain: yieldcat.beyondmachines.net 
IP: 216.24.57.1 
Status:  Active 
Resolved with: dig, ping 
Hosting Provider: Render 
WHOIS Source: ARIN 
 
Заклучок: yieldcat.beyondmachines.net 
-	yieldcat.beyondmachines.net одговара на IP адресата 216.24.57.1. 
-	Таа IP адреса е регистрирана на Render, hosting компанија со седиште во Сан Франциско, САД. 
-	Render нуди хостирање web-апликации и микросервиси. ---- 
-	IP адресата е дел од нивна директна алокација, што значи дека Render е директно одговорен за нејзиното управување. 
-	Whois податоците вклучуваат достапни контакти за техничка поддршка и злоупотреба (телефонски број и е-mail). 
-	Sub-доменот yieldcat.beyondmachines.net е активен и хостиран на инфраструктурата на Render. 
 
 
┌──(kali㉿kali)-[~] 
└─$ ping old.beyondmachines.net  
PING old.beyondmachines.net (192.0.78.233) 56(84) bytes of data. 
64 bytes from 192.0.78.233: icmp_seq=1 ttl=51 time=29.5 ms 
64 bytes from 192.0.78.233: icmp_seq=2 ttl=51 time=26.6 ms 
64 bytes from 192.0.78.233: icmp_seq=3 ttl=51 time=26.8 ms 
64 bytes from 192.0.78.233: icmp_seq=4 ttl=51 time=26.8 ms 
^C 
--- old.beyondmachines.net ping statistics --- 
4 packets transmitted, 4 received, 0% packet loss, time 7235ms 
rtt min/avg/max/mdev = 26.638/27.424/29.451/1.172 ms 
                                                                                                                                           
┌──(kali㉿kali)-[~] 
└─$ whois 192.0.78.233 
 
# 
# ARIN WHOIS data and services are subject to the Terms of Use 
# available at: https://www.arin.net/resources/registry/whois/tou/ 
# 
# If you see inaccuracies in the results, please report at 
# https://www.arin.net/resources/registry/whois/inaccuracy_reporting/ 
# 
# Copyright 1997-2025, American Registry for Internet Numbers, Ltd. 
# 
 
 
NetRange:       192.0.64.0 - 192.0.127.255 
CIDR:           192.0.64.0/18 
NetName:        AUTOMATTIC 
NetHandle:      NET-192-0-64-0-1 
Parent:         NET192 (NET-192-0-0-0-0) 
NetType:        Direct Allocation 
OriginAS:       AS2635 
Organization:   Automattic, Inc (AUTOM-93) 
RegDate:        2012-11-20 
Updated:        2024-05-21 
Comment:        Geofeed https://as2635.network/geofeed.csv 
Ref:            https://rdap.arin.net/registry/ip/192.0.64.0 
 
 
OrgName:        Automattic, Inc 
OrgId:          AUTOM-93 
Address:        60 29th Street #343 
City:           San Francisco 
StateProv:      CA 
PostalCode:     94110 
Country:        US 
RegDate:        2011-10-05 
Updated:        2023-08-11 
Ref:            https://rdap.arin.net/registry/entity/AUTOM-93 
 
 
OrgTechHandle: NOC12276-ARIN 
OrgTechName:   NOC 
OrgTechPhone:  +1-877-273-8550  
OrgTechEmail:  ipadmin@automattic.com 
OrgTechRef:    https://rdap.arin.net/registry/entity/NOC12276-ARIN 
 
OrgNOCHandle: NOC12276-ARIN 
OrgNOCName:   NOC 
OrgNOCPhone:  +1-877-273-8550  
OrgNOCEmail:  ipadmin@automattic.com 
OrgNOCRef:    https://rdap.arin.net/registry/entity/NOC12276-ARIN 
 
OrgAbuseHandle: ABUSE3970-ARIN 
OrgAbuseName:   Abuse 
OrgAbusePhone:  +1-877-273-8550  
OrgAbuseEmail:  abuse@automattic.com 
OrgAbuseRef:    https://rdap.arin.net/registry/entity/ABUSE3970-ARIN 
 
┌──(kali㉿kali)-[~] 
└─$ ping old.beyondmachines.net  
PING old.beyondmachines.net (192.0.78.233) 56(84) bytes of data. 
64 bytes from 192.0.78.233: icmp_seq=1 ttl=51 time=29.5 ms 
64 bytes from 192.0.78.233: icmp_seq=2 ttl=51 time=26.6 ms 
64 bytes from 192.0.78.233: icmp_seq=3 ttl=51 time=26.8 ms 
64 bytes from 192.0.78.233: icmp_seq=4 ttl=51 time=26.8 ms 
^C 
--- old.beyondmachines.net ping statistics --- 
4 packets transmitted, 4 received, 0% packet loss, time 7235ms 
rtt min/avg/max/mdev = 26.638/27.424/29.451/1.172 ms 
                                                                                                                                           
┌──(kali㉿kali)-[~] 
└─$ whois 192.0.78.233 
 
# 
# ARIN WHOIS data and services are subject to the Terms of Use 
# available at: https://www.arin.net/resources/registry/whois/tou/ 
# 
# If you see inaccuracies in the results, please report at 
# https://www.arin.net/resources/registry/whois/inaccuracy_reporting/ 
# 
# Copyright 1997-2025, American Registry for Internet Numbers, Ltd. 
# 
 
 
NetRange:       192.0.64.0 - 192.0.127.255 
CIDR:           192.0.64.0/18 
NetName:        AUTOMATTIC 
NetHandle:      NET-192-0-64-0-1 
Parent:         NET192 (NET-192-0-0-0-0) 
NetType:        Direct Allocation 
OriginAS:       AS2635 
Organization:   Automattic, Inc (AUTOM-93) 
RegDate:        2012-11-20 
Updated:        2024-05-21 
Comment:        Geofeed https://as2635.network/geofeed.csv 
Ref:            https://rdap.arin.net/registry/ip/192.0.64.0 
 
 
OrgName:        Automattic, Inc 
OrgId:          AUTOM-93 
Address:        60 29th Street #343 
City:           San Francisco 
StateProv:      CA 
PostalCode:     94110 
Country:        US 
RegDate:        2011-10-05 
Updated:        2023-08-11 
Ref:            https://rdap.arin.net/registry/entity/AUTOM-93 
 
 
OrgTechHandle: NOC12276-ARIN 
OrgTechName:   NOC 
OrgTechPhone:  +1-877-273-8550  
OrgTechEmail:  ipadmin@automattic.com 
OrgTechRef:    https://rdap.arin.net/registry/entity/NOC12276-ARIN 
 
OrgNOCHandle: NOC12276-ARIN 
OrgNOCName:   NOC 
OrgNOCPhone:  +1-877-273-8550  
OrgNOCEmail:  ipadmin@automattic.com 
OrgNOCRef:    https://rdap.arin.net/registry/entity/NOC12276-ARIN 
 
OrgAbuseHandle: ABUSE3970-ARIN 
OrgAbuseName:   Abuse 
OrgAbusePhone:  +1-877-273-8550  
OrgAbuseEmail:  abuse@automattic.com 
OrgAbuseRef:    https://rdap.arin.net/registry/entity/ABUSE3970-ARIN 
 
Заклучок: old.beyondmachines.net 
-	old.beyondmachines.net одговара на IP адресата 192.0.78.233. 
-	Оваа IP адреса е регистрирана на Automattic, Inc, компанија позната по WordPress.com и други сервиси. 
-	IP опсегот 192.0.64.0/18 е директно доделен на Automattic. 
-	Whois податоците содржат информации за техничка поддршка и злоупотреба, достапни преку телефон и е-пошта. 
-	Сабдоменот old.beyondmachines.net е активен и хостиран на инфраструктурата на Automattic. 
-	Станува збор за архивирана или постара верзија на BeyondMachines, хостирана од WordPress.com. 
  
 
-	Што не треба да е онлајн? 
Од безбедносна гледна точка, следниве работи не би требало да се он-лајн или јавно достапни: 
-	Административни интерфејси и контрол панели (да се користат само преку внатрешна мрежа или VPN) 
-	Интерни сервиси и датабази коишто сордржат осетливи и доверливи податоци, коишто треба да се заштитени позади firewall-и. 
-	Backup и пробни околини коишто не се активно користат во продукција, бидејќи може да содржат копии од реални податоци/слаби конфиг., и експонирањето на овие овозможува уште едно потенцијално место за напад. 
 
Што треба да направи администраторот? 
-	Проверка и ревизија на ризични sub-домени 
-	Заштита на public subдомени (Cloudflare, SSL) 
-	Редовно мониторирање и update на серверите 
-	Отстранување или заштита на поздаборавени или некористени subдомени 
-	Користење пасивни алати 
 
 
2. Задача 2
Од логовите во прилог, дури по изглед, има малициозна активност. 
Доаѓаат од повеќе IP адреси, од повеќе локации низ светот (можеби).
Типови на напади коишто се увидени:
- Reconnaissance (извидување, собирање на ранливи информации)
- SQL Injection Attempts (манипулација со базата на податоци)
- Local file inclusion, Remote code execution (вметнување на локални фајлови и извршување код, далечински)
- Brute force login attempts (присилни повторени обиди за логирање со цел да се пробие лозинка)
- shell.php (скрипта прикачена на серверот што би овозможилa целосен remote control)
- Unauthorized admin access - посета на vulnerable админ панели (/admin/dashboard.php, /admin/backup.php, admin/users.php)

Адресите од коишто доаѓаат нападите, и од каде би можеле да бидат:
-	45.33.49.201 - US	
-	121.18.83.75 - China
-	185.173.35.19 - Europe/MENA	
-	213.87.160.214 - Russia	
-	198.51.100.73 - Reserved/Test IP
-	104.28.97.142 - Cloudflare	
-	93.184.216.34 - US	

- Дали сајтот беше хакиран?
Да, сајтот бил успешно хакиран. Напаѓачот или напаѓачите пристапиле до повеќе работи меѓу кои се:
- /admin/login.php со 302 (redirect, значи успешен логин по неколку промашени обиди
- пристапиле до административните панели, наведовме и горе некои, а дополнително и settings.php и uploads.php;
- успешно го прикачиле shell.php (аналогија - remote access trojan за web сервери)
- праќале POST реквести до shell-от повеќепати, со постепено зголемување на големина на товарот (payload-и)

Логовите прво ги разгледував рачно, или визуелно ги читав. 
Потоа побарав неколку насоки од А.I. со кои греп команди би можела да започнам да екстрахирам неколку примери/извадоци.
Долу наведени се некои од примерите:

┌──(kali㉿kali)-[~] └─$ grep -Ei "(\?id=|union.*select|1=1|--|%27)" access_log.csv
┌──(kali㉿kali)-[~] └─$ grep "\.\./" access_log.csv
┌──(kali㉿kali)-[~] └─$ grep " 404 " access_log.csv
┌──(kali㉿kali)-[~] └─$ grep " 403 " access_log.csv
┌──(kali㉿kali)-[~] └─$ grep "/login" access_log.csv
┌──(kali㉿kali)-[~] └─$ grep -Ei "curl|wget|python|bot" access_log.csv



Резултати:
┌──(kali㉿kali)-[~]
└─$ grep -Ei "(\?id=|union.*select|1=1|--|%27)" access_log.csv 
121.18.83.75 - - [06/May/2025:09:23:42 +0000] "GET /products/search?q=phone%27%20OR%20%271%27%3D%271 HTTP/1.1" 500 1243 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
121.18.83.75 - - [06/May/2025:09:31:18 +0000] "GET /products/search?q=phone%27%3B%20DROP%20TABLE%20users%3B%20-- HTTP/1.1" 500 1243 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
198.51.100.73 - - [06/May/2025:10:42:16 +0000] "GET /blog/comment?id=15&text=<script>alert('XSS')</script> HTTP/1.1" 400 1253 "https://companyxyz.com/blog/article/15" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0"
104.28.97.142 - - [06/May/2025:15:26:19 +0000] "GET /track-order?id=ORD78954 HTTP/1.1" 200 4532 "https://companyxyz.com/order/confirmation/ORD78954" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
213.87.160.214 - - [06/May/2025:16:43:52 +0000] "GET /track-order?id=ORD78756 HTTP/1.1" 200 4532 "https://companyxyz.com/account/orders" "Mozilla/5.0 (iPhone; CPU iPhone OS 17_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Mobile/15E148 Safari/604.1"
193.58.156.12 - - [06/May/2025:18:35:27 +0000] "GET /track-order?id=ORD79012 HTTP/1.1" 200 4532 "https://companyxyz.com/order/confirmation/ORD79012" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Edge/123.0.0.0 Safari/537.36"
45.33.49.201 - - [06/May/2025:19:25:12 +0000] "GET /admin/user-edit.php?id=1 HTTP/1.1" 200 9823 "https://companyxyz.com/admin/users.php" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
45.33.49.201 - - [06/May/2025:19:27:34 +0000] "POST /admin/user-edit.php HTTP/1.1" 302 0 "https://companyxyz.com/admin/user-edit.php?id=1" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
45.33.49.201 - - [06/May/2025:19:27:35 +0000] "GET /admin/users.php HTTP/1.1" 200 12567 "https://companyxyz.com/admin/user-edit.php?id=1" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
                                                                         
                                                                         
┌──(kali㉿kali)-[~]
└─$ grep "\.\./" access_log.csv 
121.18.83.75 - - [06/May/2025:11:42:33 +0000] "GET /download.php?file=../../../etc/passwd HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
                                                                         
                                                                         
┌──(kali㉿kali)-[~]
└─$ grep " 404 " access_log.csv 
45.33.49.201 - - [06/May/2025:08:27:35 +0000] "GET /robots.txt HTTP/1.1" 404 452 "-" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
45.33.49.201 - - [06/May/2025:08:27:42 +0000] "GET /.git/HEAD HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
45.33.49.201 - - [06/May/2025:08:44:08 +0000] "GET /.env HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
45.33.49.201 - - [06/May/2025:08:49:12 +0000] "GET /config.php HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
45.33.49.201 - - [06/May/2025:08:51:32 +0000] "GET /wp-login.php HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
45.33.49.201 - - [06/May/2025:09:12:27 +0000] "GET /phpmyadmin HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
45.33.49.201 - - [06/May/2025:09:13:05 +0000] "GET /backup HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
121.18.83.75 - - [06/May/2025:11:42:33 +0000] "GET /download.php?file=../../../etc/passwd HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
121.18.83.75 - - [06/May/2025:15:13:45 +0000] "GET /cgi-bin/status?command=ls%20-la HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
121.18.83.75 - - [06/May/2025:15:14:26 +0000] "GET /cgi-bin/status?command=;cat%20/etc/passwd HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
121.18.83.75 - - [06/May/2025:19:04:27 +0000] "GET /api/debug HTTP/1.1" 404 452 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
                                                                         
┌──(kali㉿kali)-[~]
└─$ grep " 403 " access_log.csv
216.58.212.110 - - [06/May/2025:11:03:58 +0000] "GET /api/users HTTP/1.1" 403 321 "-" "PostmanRuntime/7.32.3"
70.35.197.74 - - [06/May/2025:14:33:45 +0000] "GET /api/orders/ORD78954 HTTP/1.1" 403 321 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
203.0.113.42 - - [06/May/2025:14:45:32 +0000] "POST /api/inventory HTTP/1.1" 403 321 "-" "python-requests/2.31.0"
45.33.49.201 - - [06/May/2025:16:23:05 +0000] "GET /uploads HTTP/1.1" 403 752 "-" "Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)"
45.33.49.201 - - [06/May/2025:16:23:18 +0000] "GET /uploads/ HTTP/1.1" 403 752 "-" "Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)"
121.18.83.75 - - [06/May/2025:17:32:47 +0000] "GET /api/user/1/profile HTTP/1.1" 403 321 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
121.18.83.75 - - [06/May/2025:17:33:21 +0000] "GET /api/user/2/profile HTTP/1.1" 403 321 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Safari/605.1.15"
                                                                         
┌──(kali㉿kali)-[~]
└─$ grep "/login" access_log.csv 
45.33.49.201 - - [06/May/2025:09:14:58 +0000] "GET /admin/login.php HTTP/1.1" 200 3452 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
45.33.49.201 - - [06/May/2025:10:02:05 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:02:08 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:02:11 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:02:14 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:02:17 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:02:20 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:13:42 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:13:45 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:10:13:48 +0000] "POST /admin/login.php HTTP/1.1" 302 0 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
45.33.49.201 - - [06/May/2025:13:17:20 +0000] "GET /admin/login.php HTTP/1.1" 200 3452 "https://companyxyz.com/admin/dashboard.php" "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"
213.87.160.214 - - [06/May/2025:15:31:48 +0000] "GET /login HTTP/1.1" 200 3582 "https://companyxyz.com/account" "Mozilla/5.0 (iPhone; CPU iPhone OS 17_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Mobile/15E148 Safari/604.1"
213.87.160.214 - - [06/May/2025:15:32:43 +0000] "POST /login HTTP/1.1" 302 0 "https://companyxyz.com/login" "Mozilla/5.0 (iPhone; CPU iPhone OS 17_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Mobile/15E148 Safari/604.1"
213.87.160.214 - - [06/May/2025:15:32:45 +0000] "GET /account HTTP/1.1" 200 8752 "https://companyxyz.com/login" "Mozilla/5.0 (iPhone; CPU iPhone OS 17_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Mobile/15E148 Safari/604.1"
41.82.97.189 - - [06/May/2025:17:42:39 +0000] "GET /login HTTP/1.1" 200 3582 "https://companyxyz.com/account/wishlist" "Mozilla/5.0 (iPhone; CPU iPhone OS 17_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Mobile/15E148 Safari/604.1"
198.51.100.73 - - [06/May/2025:17:47:23 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0"
104.16.248.131 - - [06/May/2025:18:03:29 +0000] "GET /login HTTP/1.1" 200 3582 "https://companyxyz.com/products/item/24563" "Mozilla/5.0 (Linux; Android 14; SM-S918B) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Mobile Safari/537.36"
45.33.49.201 - - [06/May/2025:18:57:26 +0000] "GET /admin/login.php HTTP/1.1" 200 3452 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
45.33.49.201 - - [06/May/2025:19:12:04 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
45.33.49.201 - - [06/May/2025:19:12:07 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
45.33.49.201 - - [06/May/2025:19:12:10 +0000] "POST /admin/login.php HTTP/1.1" 401 752 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
45.33.49.201 - - [06/May/2025:19:12:13 +0000] "POST /admin/login.php HTTP/1.1" 302 0 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.87 Safari/537.36"
104.16.248.131 - - [06/May/2025:19:38:45 +0000] "POST /login HTTP/1.1" 302 0 "https://companyxyz.com/login" "Mozilla/5.0 (Linux; Android 14; SM-S918B) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Mobile Safari/537.36"
104.16.248.131 - - [06/May/2025:19:38:47 +0000] "GET /account HTTP/1.1" 200 8752 "https://companyxyz.com/login" "Mozilla/5.0 (Linux; Android 14; SM-S918B) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Mobile Safari/537.36"
                                                                         
                                                                         
┌──(kali㉿kali)-[~]
└─$ grep -Ei "curl|wget|python|bot" access_log.csv 
45.33.49.201 - - [06/May/2025:08:27:35 +0000] "GET /robots.txt HTTP/1.1" 404 452 "-" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
203.0.113.42 - - [06/May/2025:14:43:27 +0000] "POST /products/search HTTP/1.1" 200 10456 "-" "python-requests/2.31.0"
203.0.113.42 - - [06/May/2025:14:44:05 +0000] "POST /api/subscribe HTTP/1.1" 201 142 "-" "python-requests/2.31.0"
203.0.113.42 - - [06/May/2025:14:45:32 +0000] "POST /api/inventory HTTP/1.1" 403 321 "-" "python-requests/2.31.0"
203.0.113.42 - - [06/May/2025:17:13:28 +0000] "GET /robots.txt HTTP/1.1" 200 452 "-" "python-requests/2.31.0"
203.0.113.42 - - [06/May/2025:17:13:45 +0000] "GET /sitemap.xml HTTP/1.1" 200 24536 "-" "python-requests/2.31.0"
203.0.113.42 - - [06/May/2025:17:15:22 +0000] "GET /api/products HTTP/1.1" 200 47834 "-" "python-requests/2.31.0"
203.0.113.42 - - [06/May/2025:17:17:13 +0000] "GET /api/categories HTTP/1.1" 200 2843 "-" "python-requests/2.31.0"
203.0.113.42 - - [06/May/2025:17:19:27 +0000] "GET /api/products?category=electronics HTTP/1.1" 200 32456 "-" "python-requests/2.31.0"

Во овие ‘grep’ команди на acces_log.csv, проверивме за:
-	SQL Injection напади
-	XSS напади
-	Directory Traversal (Патеки) 
-	Статус кодови – 403 и 404
-	Логин активности
-	Детекција на бот/автоматизирани алатки


Што треба (или не треба) да направи администраторот?
- да го симне shell.php најбрзо што може (доколку е сеуште активен)
- да ги смени сите администраторски креденцијали
- да провери за прикачени или модифицирани фајлови
- да исчисти /uploads/ од туѓи скрипти
- да ги ресетира сите сесии 
- да постави WAF (Web application firewall) или input sanitization на формите за пребарување и пополнување
- заштита на админ панели (2fa/mfa, rate limitng, ip restriction)

Што НЕ треба да направи администраторот?
- да ги игнорира 401 и 404 ерорите,
- да дозволува јавни upload-и без филтри
- експониран /admin патеки без заштита
- логување на пасворди и сензитивни податоци во логови
- промашени IP Lогови за POST реквести

Значи, да заклучиме: 
- Да, сајтот бил "хакиран", бил прикачен и извршен shell,  имало напаѓачи од повеќе IP адреси (најмногу од 45.33.49.201 и 121.18.83.75), ранливостите беа пронајдени анализирајќи респонзивни кодови, endpoint-и и однесувањето на логовите. Администраторот мора да ги поништи пристапите/сесиите, да го исчисти сајтот комплетно и да ги поправи овие ранливости.

To make your content look *clean and beautiful* on GitHub (especially in a Markdown `.md` file), I’ve formatted your text using Markdown code blocks and styling conventions. GitHub supports syntax highlighting and preserves formatting inside triple backticks, which is perfect for logs, terminal outputs, and your analysis.

Here's your full content ready to paste into GitHub:

---

```bash
┌──(kali㉿kali)-[~]
└─$ whois 192.0.78.233

#
# ARIN WHOIS data and services are subject to the Terms of Use
# available at: https://www.arin.net/resources/registry/whois/tou/
#
# If you see inaccuracies in the results, please report at
# https://www.arin.net/resources/registry/whois/inaccuracy_reporting/
#
# Copyright 1997-2025, American Registry for Internet Numbers, Ltd.
#

NetRange:       192.0.64.0 - 192.0.127.255
CIDR:           192.0.64.0/18
NetName:        AUTOMATTIC
NetHandle:      NET-192-0-64-0-1
Parent:         NET192 (NET-192-0-0-0-0)
NetType:        Direct Allocation
OriginAS:       AS2635
Organization:   Automattic, Inc (AUTOM-93)
RegDate:        2012-11-20
Updated:        2024-05-21
Comment:        Geofeed https://as2635.network/geofeed.csv
Ref:            https://rdap.arin.net/registry/ip/192.0.64.0

OrgName:        Automattic, Inc
OrgId:          AUTOM-93
Address:        60 29th Street #343
City:           San Francisco
StateProv:      CA
PostalCode:     94110
Country:        US
RegDate:        2011-10-05
Updated:        2023-08-11
Ref:            https://rdap.arin.net/registry/entity/AUTOM-93

OrgTechHandle: NOC12276-ARIN
OrgTechName:   NOC
OrgTechPhone:  +1-877-273-8550
OrgTechEmail:  ipadmin@automattic.com
OrgTechRef:    https://rdap.arin.net/registry/entity/NOC12276-ARIN

OrgNOCHandle: NOC12276-ARIN
OrgNOCName:   NOC
OrgNOCPhone:  +1-877-273-8550
OrgNOCEmail:  ipadmin@automattic.com
OrgNOCRef:    https://rdap.arin.net/registry/entity/NOC12276-ARIN

OrgAbuseHandle: ABUSE3970-ARIN
OrgAbuseName:   Abuse
OrgAbusePhone:  +1-877-273-8550
OrgAbuseEmail:  abuse@automattic.com
OrgAbuseRef:    https://rdap.arin.net/registry/entity/ABUSE3970-ARIN
```

---

### 📌 Заклучок

`old.beyondmachines.net`

* одговара на IP адресата `192.0.78.233`
* Регистрирана е на **Automattic, Inc.**, познати по **WordPress.com**
* IP опсегот `192.0.64.0/18` е директно доделен
* Whois содржи и технички и abuse контакти
* Сабдоменот е **активен** и **хостиран** од Automattic
* Се чини дека е архивирана/постара верзија на BeyondMachines

---

### ❌ Што не треба да е онлајн?

> Од безбедносна гледна точка, следниве работи не треба да бидат јавно достапни:

* Административни интерфејси и контрол панели (само преку внатрешна мрежа/VPN)
* Интерни сервиси и бази на податоци со осетливи информации
* Backup и staging околини што не се продуктивни (можат да содржат реални податоци и конфигурации)

---

### ✅ Што треба да направи администраторот?

* Ревизија на ризични sub-домени
* SSL + CDN за заштита на јавните поддомени (пример: Cloudflare)
* Мониторинг и редовни updates
* Укинување или заштита на заборавени субдомени
* Користење на пасивни алати за набљудување

---

## 🛠️ Задача 2: Преглед на логови

> Од логовите, видлива е малициозна активност од повеќе IP адреси и геолокации.

### Видови напади:

* 🕵 Reconnaissance
* 🧬 SQL Injection Attempts
* 🗃️ Local File Inclusion, Remote Code Execution
* 🔐 Brute-force login attempts
* 💻 `shell.php` - за целосен remote control
* 🛑 Unauthorized admin access (`/admin/dashboard.php`, `/admin/backup.php`, `/admin/users.php`)

### Примери на IP адреси:

* `45.33.49.201` — US
* `121.18.83.75` — China
* `185.173.35.19` — Europe/MENA
* `213.87.160.214` — Russia
* `198.51.100.73` — Reserved/Test IP
* `104.28.97.142` — Cloudflare
* `93.184.216.34` — US

---

### ❓ Дали сајтот беше хакиран?

✅ Да. Нападот беше успешен.
**Докази:**

* `/admin/login.php` со `302` redirect → успешен логин
* Пристап до админ панели (`settings.php`, `uploads.php`)
* Прикачен `shell.php`
* Повеќекратни POST барања до `shell.php` со payload-и со растечки големини

---

### 👀 Анализа на логови

Прво визуелна анализа, потоа помош од A.I. за **grep** команди:

```bash
grep -Ei "(\?id=|union.*select|1=1|--|%27)" access_log.csv
grep "\.\./" access_log.csv
grep " 404 " access_log.csv
grep " 403 " access_log.csv
grep "/login" access_log.csv
grep -Ei "curl|wget|python|bot" access_log.csv
```

---

