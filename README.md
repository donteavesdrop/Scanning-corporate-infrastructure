# Scanning-corporate-infrastructure
# Практика №2. Сканирование корпоративной инфраструктуры

<aside>
<img src="https://www.notion.so/icons/chevrons-vertical_gray.svg" alt="https://www.notion.so/icons/chevrons-vertical_gray.svg" width="40px" /> **Navigation**

</aside>

## Задание к практической работе №2

---

> **1) Подготовить стенд для выполнения практической работы:**
> 
> - Установлена Kali Linux не старше 2021 года
> - Установлены сетевые сканеры Nmap и Nessus
> - Установлены сетевые утилиты для OSINT
> 
> [Подготовка стенда (1)](https://www.notion.so/1-72902ecdcdf94ce7a07dc5253b9288fc?pvs=21)
> 
> **2) Провести поиск по открытым источникам организаций, имеющих домены: [mirea.tech](http://mirea.tech/) и [ptlab.ru](http://ptlab.ru/). В отчет включить:**
> 
> - Сотрудников организации, их должности, email адреса, телефоны (в том числе рабочие и личные), социальные сети.
> - Сайты организаций, IP адреса, доменные имена, поддомены, DNS записи
> - Результаты сканирования всех IP адресов организации, в том числе с использованием Nessus
>     
>     [Nmap - manuals](https://www.notion.so/Nmap-manuals-dff1dd1f05d0492686834c98d82d28f9?pvs=21)
>     
>     [Установка Nessus](https://www.notion.so/Nessus-b9ca13deea8342709c7a4102d0dc83f7?pvs=21)
>     
> - Возможную организационную структуру организации и лиц, принимающих решения
> - Оборудование, которое используется в организации
> - Все связанные под

## Ход работы

---

### Nmap

Для начала просканируем адреса с помощью nmap

![Untitled](https://github.com/user-attachments/assets/d0e6c9ec-288a-4f30-be89-fab35be671e1)

mirea.tech

![Untitled 1](https://github.com/user-attachments/assets/e1fad35a-ee91-41ac-b964-0a58f33ad635)


[**ptlab.ru**](http://ptlab.ru/)

***- mirea.tech***

IP-адрес - 85.142.160.226.

**Не показано: 997 отфильтрованных портов**

- **`80/tcp open http`**: Эта строка указывает, что порт 80 (стандартный порт для HTTP) открыт и используется сервером HTTP.
- **`443/tcp open https`**: Эта строка указывает, что порт 443 (стандартный порт для HTTPS) открыт и используется сервером HTTPS.
- **`7777/tcp open cbt`**: Эта строка указывает, что порт 7777 также открыт.

***- ptlab.ru***

IP-адрес - 85.142.160.226.

**Не показано: 998 отфильтрованных портов**

- **`80/tcp open http`**: Эта строка указывает, что порт 80 (стандартный порт для HTTP) открыт и используется сервером HTTP.
- **`443/tcp open https`**: Эта строка указывает, что порт 443 (стандартный порт для HTTPS) открыт и используется сервером HTTPS.

Сканирование с опциями **`-T4 -A`** предназначено для более детального и быстрого анализа. Опция **`-T4`** увеличивает скорость сканирования, а **`-A`** включает в себя обнаружение ОС, версию сервиса, скриптовое сканирование и трассировку.

![mirea,tech](%25D0%25A1%25D0%25BD%25D0%25B8%25D0%25BC%25D0%25BE%25D0%25BA_%25D1%258D%25D0%25BA%25D1%2580%25D0%25B0%25D0%25BD%25D0%25B0_2024-05-19_141915.png)

mirea,tech

![Untitled 2](https://github.com/user-attachments/assets/50d54396-b3e8-4e0e-8fef-682e66851374)


ptlab.ru

***- mirea.tech*** 

**Не показано: 998 отфильтрованных портов**

- **`80/tcp open http nginx 1.14.2`**: На порту 80 запущен HTTP-сервер nginx версии 1.14.2. Сервер не перенаправил запрос на HTTPS.
- **`443/tcp open ssl/http nginx 1.14.2`**: На порту 443 запущен HTTPS-сервер nginx версии 1.14.2. Запрос на HTTP к этому порту вернул ошибку 400, указывая, что запрос был направлен на HTTPS-порт.
    - **SSL-сертификат**:
        - Общий домен (commonName): **`.kb4-lab.ru`**
        - Альтернативные имена (Subject Alternative Name): **`.kb4-lab.ru`**
        - Действителен с: 2022-03-27 по 2022-06-25
    - **TLS-поддержка**:
        - ALPN: **`h2`**, **`http/1.1`**
        - Next Protocol Negotiation (NPN): **`h2`**, **`http/1.1`**

***- ptlab.ru*** 

**Не показано: 998 отфильтрованных портов**

- **`80/tcp open tcpwrapped`**: Порт 80 открыт, но сервис завёрнут (tcpwrapped), что может указывать на использование системы для предотвращения сканирования.
    - HTTP-сервер: nginx 1.14.2. Сервер не перенаправил запрос на HTTPS.
- **`443/tcp open tcpwrapped`**: Порт 443 открыт, но сервис завёрнут (tcpwrapped).
    - HTTP-сервер: nginx 1.14.2. Запрос на HTTP к этому порту вернул ошибку 400, указывая, что запрос был направлен на HTTPS-порт.
    - **SSL-сертификат**:
        - Общий домен (commonName): **`.kb4-lab.ru`**
        - Альтернативные имена (Subject Alternative Name): **`.kb4-lab.ru`**
        - Действителен с: 2022-03-27 по 2022-06-25
    - **TLS-поддержка**:
        - ALPN: **`h2`**, **`http/1.1`**
        - Next Protocol Negotiation (NPN): **`h2`**, **`http/1.1`**

**Общие выводы:**

1. Оба домена (**`mirea.tech`** и **`ptlab.ru`**) имеют одинаковый IP-адрес и используют один и тот же сервер с nginx 1.14.2 на портах 80 и 443.

![Untitled 3](https://github.com/user-attachments/assets/1222966c-023a-48d6-98ad-47d67e7f5b55)


1. Сервисы на обоих доменах настроены аналогично, с одинаковыми SSL-сертификатами и поддержкой протоколов ALPN и NPN.
2. Сертификаты SSL уже недействительны, их срок действия закончился 25 июня 2022 года.
3. На домене **`mirea.tech`** открыт дополнительный порт 7777, который отсутствует на домене **`ptlab.ru`**.
- ***Поиск версий ОС***

![Untitled 4](https://github.com/user-attachments/assets/7011d3b0-d548-4f91-bdd5-538967267372)


mirea.tech

![Untitled 5](https://github.com/user-attachments/assets/4846cd3b-acce-444f-ae95-72860d7b5aa4)


ptlab.ru

Для **`mirea.tech`** получены следующие данные:

- **Устройство**: Специализированное, точка доступа (WAP), телефон.
- **Запущенное**: iPXE 1.X, Linux 2.4.X|2.6.X, встроенный Sony Ericsson.
- **Детали ОС**: iPXE 1.0.0+, Tomato 1.28 (Linux 2.4.20), Прошивка Tomato (Linux 2.6.22), мобильный телефон Sony Ericsson U8i Vivaz.

Для **`ptlab.ru`** получены следующие данные:

- **Открытые порты**: Только порт 7777.
- **Предположения о ОС**: Может быть различными устройствами, такими как принтер Brother MFC-7820N, мост Digi Connect ME серийно-этанетный, устройство хранения Netgear SC101 Storage Central NAS и другими.

![Untitled 6](https://github.com/user-attachments/assets/02923a30-07ce-40bd-a73f-aa27a5b0fb16)


- **Тип устройства:** Точка доступа (WAP) или общего назначения.
- **Запущенные ОС:**
    - Actiontec MI424WR-GEN3I WAP.
    - DD-WRT v24-sp2 (Linux 2.4.37).
    - Linux 3.2.
    - Microsoft Windows XP SP3.
    - Microsoft Windows 7.
    - Microsoft Windows Server 2012.

**CPE (Common Platform Enumeration):**

- Actiontec MI424WR-GEN3I WAP.
- Linux Kernel версии 2.4.37 и 3.2.
- Microsoft Windows XP SP3.
- Microsoft Windows 7.
- Microsoft Windows Server 2012.

### WHOIS

[WHOIS Search, Domain Name, Website, and IP Tools - Who.is](https://who.is/)

![Untitled 7](https://github.com/user-attachments/assets/587f2f27-6823-4337-a900-840f14fa2d88)


![Untitled 8](https://github.com/user-attachments/assets/54b4cc27-0a85-49a5-85e9-49d888a57a60)


![Untitled 9](https://github.com/user-attachments/assets/28714ef7-59b6-4ece-bda7-0d7f546b0e08)


1. Домен mirea.tech зарегистрирован у REG.RU LLC. Статус регистрации указан как "clientTransferProhibited", что означает, что перенос домена запрещен.
2. Домен зарегистрирован до 30 ноября 2024 года, а зарегистрирован он был 30 ноября 2020 года. Последнее обновление данных произошло 10 ноября 2023 года.
3. Серверы имен (Name Servers) для домена указаны как ns1.reg.ru (с IP-адресом 194.67.73.174) и ns2.reg.ru (с IP-адресом 194.67.73.176).
4. В контактной информации отсутствуют личные данные, они скрыты в соответствии с применимыми законами. Для всех контактов (регистранта, администратора, технического контакта) предоставлены только общие данные организации и контактные телефоны и адреса электронной почты, без указания конкретных лиц.

**Registrant Contact Information:**

**Phone**

+7.4955801111

**Fax**

+7.4955801111

**Email**

[https://who.is/tools/stringImage?img=BP2%2BqyKze01P7oWYguuX1HFiqqqAjOGXv1v1%2BxCQ48k%3D](https://who.is/tools/stringImage?img=BP2%2BqyKze01P7oWYguuX1HFiqqqAjOGXv1v1%2BxCQ48k%3D)

---

**Administrative Contact Information:**

**Phone**

+7.4955801111

**Fax**

+7.4955801111

**Email**

[https://who.is/tools/stringImage?img=BP2%2BqyKze01P7oWYguuX1HFiqqqAjOGXv1v1%2BxCQ48k%3D](https://who.is/tools/stringImage?img=BP2%2BqyKze01P7oWYguuX1HFiqqqAjOGXv1v1%2BxCQ48k%3D)

---

**Technical Contact Information:**

**Phone**

+7.4955801111

**Fax**

+7.4955801111

**Email**

[https://who.is/tools/stringImage?img=BP2%2BqyKze01P7oWYguuX1HFiqqqAjOGXv1v1%2BxCQ48k%3D](https://who.is/tools/stringImage?img=BP2%2BqyKze01P7oWYguuX1HFiqqqAjOGXv1v1%2BxCQ48k%3D)

![Untitled 10](https://github.com/user-attachments/assets/3828412e-a5de-47a5-b9bd-1faa1c752d47)


![Untitled 11](https://github.com/user-attachments/assets/f75a91c5-28d1-4280-aac7-d85808c52859)


Домен [ptlab.ru](http://ptlab.ru/) зарегистрирован через регистратор REGRU-RU. Записи Whois указывают на то, что домен зарегистрирован до 16 марта 2025 года и был создан 16 марта 2021 года. Состояние домена на данный момент - "REGISTERED, DELEGATED, UNVERIFIED". Контактная информация о лице или организации, зарегистрировавшей домен, не предоставлена, так как домен принадлежит частному лицу. Доменные серверы для этого домена установлены на [ns1.reg.ru](http://ns1.reg.ru/) и [ns2.reg.ru](http://ns2.reg.ru/). IP-адрес домена [ptlab.ru](http://ptlab.ru/) - 85.142.160.226.

### DNSDumpster

[DNSDumpster.com - dns recon and research, find and lookup dns records](https://dnsdumpster.com/)

![Untitled 12](https://github.com/user-attachments/assets/ed6a3c1f-6fac-4fa3-b4fe-fbfb3cb4ad57)


![Untitled 13](https://github.com/user-attachments/assets/38758fad-d117-4d3f-94e4-322d58a755c7)


![Untitled 14](https://github.com/user-attachments/assets/b0ac7bdb-d64b-4b4f-98b4-84e9b34f9665)


![Untitled 15](https://github.com/user-attachments/assets/f45fd8e5-0940-4c23-b4d4-d4e05ef46cd8)


Домен mirea.tech использует DNS-серверы [ns1.reg.ru](http://ns1.reg.ru/) и [ns2.reg.ru](http://ns2.reg.ru/) с IP-адресами 176.99.13.11 и 176.99.13.12 соответственно. 

Для обработки электронной почты домена используются MX-записи. 

Размещение (Host Records) домена mirea.tech связано с двумя IP-адресами, 85.142.160.226 для ctf.mirea.tech и kb.mirea.tech. Оба сайта используют веб-сервер nginx версии 1.14.2.

![Untitled 16](https://github.com/user-attachments/assets/c7c8db05-9bdd-4627-979c-06929e5e1cad)


![Untitled 17](https://github.com/user-attachments/assets/36efe1bf-18b0-4462-88d8-3d63b17390a0)


![Untitled 18](https://github.com/user-attachments/assets/0a693ce7-e406-4363-9cca-373e6040df19)


DNS-серверы:

- ns1.reg.ru с IP-адресом 176.99.13.11
- ns2.reg.ru с IP-адресом 176.99.13.12

Отсутствуют записи MX (для электронной почты) и TXT (для SPF-конфигураций).

Данные о хостах (A записи) отсутствуют85, так как используется статическая база данных, которая обновляется ежемесячно.

### Pentest-tools

[Free subdomain finder online 🛡️ find subdomains of domain](https://pentest-tools.com/information-gathering/find-subdomains-of-domain)

Находим субдомены сайтов

![Untitled 19](https://github.com/user-attachments/assets/8e053051-daee-4ef9-b574-5f8f5cb78ada)


![Untitled 20](https://github.com/user-attachments/assets/61881d34-9037-46de-a075-f2ced07cd883)


С помощью других ресурсов найдено немного больше

![Untitled 21](https://github.com/user-attachments/assets/503986b1-6fe3-46a6-bc10-f3da529e5f15)


### Nessus

![Untitled 22](https://github.com/user-attachments/assets/d4fe7959-8b88-4941-9b4e-03eca58eb601)


Описание части полученной информации

![Untitled 23](https://github.com/user-attachments/assets/a6eb7f80-fc9d-4089-8b4f-30d87d601aa0)


1. **Remote Operating System (Удалённая операционная система):**
    - **CPE match:** **`cpe:/o:cisco:pix_firewall:7.0`**
        - Cisco PIX Firewall Software
    - Плагин определил, что удалённая система использует программное обеспечение Cisco PIX Firewall версии 7.0. Это указывает на то, что эта система, вероятно, является сетевым устройством Cisco PIX Firewall.
2. **Applications (Приложения):**
    - **CPE match:** **`cpe:/a:igor_sysoev:nginx:1.14.2`**
        - Nginx
    - Плагин определил, что на удалённой системе установлено и работает приложение Nginx версии 1.14.2. Nginx - это широко используемый веб-сервер и обратный прокси-сервер.
    
    ![Untitled 24](https://github.com/user-attachments/assets/33fcd901-9d4c-45db-b411-0a1b6a31f9bd)

    
     Сканирование выявило, что удаленный хост работает под управлением Cisco PIX Firewall Software версии 7.0.
    
    1. **Устройство и операционная система**:
        - Устройство: Firewall (CISCO PIX 7.0)
        - Операционная система: CISCO PIX 7.0
    2. **Открытые порты**:
        - tcp/80: Открыт
        - tcp/443/www: Открыт (поддерживает TLSv1.0/TLSv1.1/TLSv1.2)
    3. **Сертификат и шифрование**:
        - Сертификат: DST Root CA X3
            - Издатель: Digital Signature Trust Co.
            - Алгоритм подписи: SHA-1 с RSA шифрованием
        - Шифрование (поддерживаемые шифры SSL/TLS):
            - TLSv1.2 поддерживает следующие шифры:
                - DHE-RSA-AES128-SHA256, DHE-RSA-AES-256-CCM-AEAD, DHE-RSA-AES-256-CCM8-AEAD, DHE-RSA-AES256-SHA384, DHE-RSA-AES256-SHA, ECDHE-RSA-AES256-SHA, DHE-RSA-AES256-SHA256, ECDHE-RSA-AES256-SHA384
            - Обнаружены шифры с ключом длиной >= 112 бит.
    4. **Протоколы**:
        - Поддерживаемые протоколы SSL / TLS: h2, http/1.1
        - TLSv1.2 включен, и сервер поддерживает хотя бы один шифр.
    5. **Доверие к сертификату**:
        - Предупреждение о недоверенном SSL-сертификате, так как цепочка сертификатов не начинается от известного общедоступного центра сертификации.
    
    ### Выводы
    
    В рамках практической работы №2 по сканированию корпоративной инфраструктуры был проведен анализ доменов mirea.tech и [ptlab.ru](http://ptlab.ru/) с использованием инструментов Nmap, WHOIS, DNSDumpster и Nessus.
    
    В результате анализа было выявлено, что оба домена используют одинаковый IP-адрес - 85.142.160.226. Порты 80 и 443 открыты на обоих доменах и используют сервер nginx версии 1.14.2. Интересно отметить, что домен mirea.tech имеет дополнительный открытый порт 7777, которого нет на домене [ptlab.ru](http://ptlab.ru/).
    
    Оба домена используют одинаковые SSL-сертификаты. Однако, эти сертификаты уже недействительны, поскольку их срок действия истек 25 июня 2022 года.
    
    С точки зрения регистрации доменов, оба сайта зарегистрированы через [REG.RU](http://reg.ru/) LLC. Однако личная информация о регистранте скрыта, что соответствует стандартам защиты личной информации.
