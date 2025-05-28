# BeyondMachines

## Second Phase of Application for BeyondMachines Internship


### Задача 1 – Пасивен DNS скен

**Цел:** Пасивен скен на доменот `beyondmachines.net` и пронаоѓање на број на DNS записи.


**Алатки користени:**

- [Subdomain Finder Scan (15 May 2025)](https://subdomainfinder.c99.nl/scans/2025-05-15/beyondmachines.net)
- [CRT.sh Certificate Transparency](https://crt.sh/?q=%25.beyondmachines.net)
- Kali Linux алатки: `subfinder`, `sublist3r`, `dnsrecon`, `amass`


#### Опис:
- Скенирани SSL/TLS сертификати за subдомените.
- Податоци од пасивни извори (search engines, CT logs, DNS history).


### Резултати

- BeyondMachines има **13 subдомени**
  - Од нив, **5 имаат IP адреси**
  - **1 има Cloudflare заштита**


**Активни субдомени:**

- `challenge.beyondmachines.net` - IP адреса, хостиран
- `old.beyondmachines.net` - активен, потенцијално ризичен
- `trust.beyondmachines.net` - Cloudflare
- `beyondmachines.net` - активен
- `yieldcat.beyondmachines.net` - активен


### Скенови во Kali виртуелна машина

```bash
subfinder -d beyondmachines.net -o subfinder_results.txt
```

```bash
ping -c 1 yieldcat.beyondmachines.net
whois 216.24.57.1
```

**yieldcat.beyondmachines.net:**
- IP: `216.24.57.1`
- Хостирано од: Render, San Francisco, US


```bash
ping old.beyondmachines.net
whois 192.0.78.233
```

**old.beyondmachines.net:**
- IP: `192.0.78.233`
- Хостирано од: Automattic (WordPress.com)


###  Безбедносни препораки

**Не треба да бидат јавно достапни:**
- Admin панели
- Интерни сервиси/датабази
- Backup или test околини


**Администратор треба да:**
- Ревидира ризични subдомени
- Користи SSL, Cloudflare
- Отстрани стари или неактивни поддомени
- Мониторинг и updates
- Користи пасивни скени



## Задача 2 – Анализа на логови

**Заклучок:** Сајтот бил **успешно хакиран**.


### Типови на напади:

- Reconnaissance
- SQL Injection
- XSS / LFI / RCE
- Brute-force login
- Прикачен `shell.php` за remote control
- Access до admin панели


### IP адреси вклучени во нападот:

| IP Address       | Локација         |
|------------------|------------------|
| 45.33.49.201     | US               |
| 121.18.83.75     | China            |
| 185.173.35.19    | Europe/MENA      |
| 213.87.160.214   | Russia           |
| 198.51.100.73    | Reserved/Test IP |
| 104.28.97.142    | Cloudflare       |
| 93.184.216.34    | US               |


### Користени GREP команди:

```bash
grep -Ei "(\?id=|union.*select|1=1|--|%27)" access_log.csv
grep "\.\./" access_log.csv
grep " 404 " access_log.csv
grep " 403 " access_log.csv
grep "/login" access_log.csv
grep -Ei "curl|wget|python|bot" access_log.csv
```


### Што се случило:

- `/admin/login.php` → redirect `302` = успешен логин
- `shell.php` прикачен и користен
- Бројни POST барања со payloads
- Пристап до admin/control панели и uploads


### Што треба да направи администраторот

- Да се отстрани `shell.php`
- Промена на admin лозинки
- Проверка за модифицирани/страни фајлови
- Чистење `/uploads/`
- Ресетирање на сите сесии
- Ограничувања на `/admin` (2FA, IP restrict)
- Вметнување на WAF / input validation


### Што НЕ треба да се прави

- Игнорирање на 401/404 ерори
- Јавни upload-и без валидација
- Остават изложени тајни патеки
- Логирање на лозинки во access_log
- Немање на rate limiting


### Финален заклучок

Да, сајтот бил хакиран. Напаѓачите успешно прикачиле shell и добиле пристап до административните панели. Детектирани се напади од најмалку 7 различни IP адреси. Администраторот мора итно да ги исчисти компромитираните фајлови, да рестартира сите активни сесии и да имплементира засилени безбедносни мерки. Во зависност од сериозноста на нападот, можеби ќе биде потребно целосно бришење на системот и враќање од безбеден backup.
