# Домашнее задание к занятию "`Кластеризация и балансировка нагрузки`" - `Герасимов Антон`


---

### Задание 1

1. Запустите два simple python сервера на своей виртуальной машине на разных портах
2. Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
3. Настройте балансировку Round-robin на 4 уровне.
* На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.

[Конфиг](https://github.com/Anthony13375/haproxy/blob/main/configs/haproxy_tcp.cfg)

![Балансировка](https://github.com/Anthony13375/haproxy/blob/main/img/img1.png)
![Балансировка tcp](https://github.com/Anthony13375/haproxy/blob/main/img/img2.png)

---

### Задание 2
1. Запустите три simple python сервера на своей виртуальной машине на разных портах
2. Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
3. HAproxy должен балансировать только тот http-трафик, который адресован домену example.local
* На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.

[Конфиг](https://github.com/Anthony13375/haproxy/blob/main/configs/haproxy_http.cfg)

![Балансировка](https://github.com/Anthony13375/haproxy/blob/main/img/img3.png)
![Балансировка http](https://github.com/Anthony13375/haproxy/blob/main/img/img4.png)



