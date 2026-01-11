# Домашнее задание к занятию "`Кластеризация и балансировка нагрузки`" - `Герасимов Антон`


---

### Задание 1

1. Запустите два simple python сервера на своей виртуальной машине на разных портах
2. Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
3. Настройте балансировку Round-robin на 4 уровне.
* На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.

```
Что добавил в дефолтный конфигурационный файл:
listen stats
	bind 			:888
	mode 			http			
	stats			enable
	stats uri		/stats
	stats refresh 		5s
	stats realm		Haproxy\ Statistics

listen web_tcp
	bind :1325
	balance roundrobin
	server s1 127.0.0.1:8888 check
	server s2 127.0.0.1:9999 check

```
![Балансировка](https://github.com/Anthony13375/haproxy/blob/main/img/img1.png)
![Балансировка tcp](https://github.com/Anthony13375/haproxy/blob/main/img/img2.png)

---

### Задание 2
1. Запустите три simple python сервера на своей виртуальной машине на разных портах
2. Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
3. HAproxy должен балансировать только тот http-трафик, который адресован домену example.local
* На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.


```
Что добавил в дефолтный конфигурационный файл:
listen stats
	bind 			:888
	mode 			http			
	stats			enable
	stats uri		/stats
	stats refresh 		5s
	stats realm		Haproxy\ Statistics
frontend acl
	mode http
	bind :8088
	acl ACL_example.local hdr(host) -i example.local
	use_backend weight_servers if ACL_example.local

backend weight_servers
	mode http
	balance roundrobin
	option httpchk
	http-check send meth GET uri /index.html
	server s1 127.0.0.1:8888 check weight 2
	server s2 127.0.0.1:9999 check weight 3
	server s3 127.0.0.1:7777 check weight 4
```
![Балансировка](https://github.com/Anthony13375/haproxy/blob/main/img/img3.png)
![Балансировка http](https://github.com/Anthony13375/haproxy/blob/main/img/img4.png)



