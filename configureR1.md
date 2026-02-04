
`router> en` <br>
`router# conf t`<br>
`router(config)# enable secret Tomilino321` **задаём пароль на `enable`** <br>
`router(config)# service password-encryption` **теперь пароль храниться в хэшированном виде** <br>
`router(config)# hostname router1` **Изменение имени устройства на `router1`, необходимо для настройки SSh** <br>
`router1(config)# username admin_R privilege 15 secret Pa$$w0rd321` **задаём пользователя с максимальными правами** <br>
`router1(config)# line console 0` **переходим в режим настройки консольного подключения** <br>
`router1(config-line)# login authentication default` **Требование аутентификации по локальной базе пользователей при подключении `через консоль`** <br>
`router1(config-line)#en` <br>
`router1(config)# line vty 0 15` **Переходим в режим настройки виртуальных терминальных линий (VTY) с 0 по 15. Эти линии используются для удаленного доступа (Telnet/SSH)** <br>
`router1(config-line)# login authentication default` <br>
`router1(config-line)# transport input ssh` **Разрешение только SSH подключений на VTY линиях** <br>
`router1(config-line)# en` <br>

`router1(config)#ip domain-name test.local` **Установка доменного имени для устройства. Это необходимо для генерации RSA ключей, которые используются в SSH** <br>
`(config)#crypto key generate rsa general-keys modulus 2048` **Генерируем ключи шифрования** <br>

`router1(config)# int g0/0` **Переходим в режим `настройки интерфейса`** <br>
`router1(config-if)# no shutdown` **физически включаем интерфейс** <br>
`router1(config-if)#ex` <br>
`router1(config)# int g0/0.2` <br>
`router1(config-subif)# encapsulation dot1Q 2` **включаем инкапсуляцию трафика** <br>
`router1(config-subif)#ip addr 192.168.2.1 255.255.255.252` **задаём ip адресс шлюза по умолчаннию и маску сети** <br>
`router1(config-subif)# encapsulation dot1Q 2` <br>
`router1(config-subif)# ip helper-address 192.168.4.2` <br>
`router1(config-subif)# ip nat inside` <br>
`router1(config-subif)#ex` <br>
`router1(config)# int g0/0.3` <br>
`router1(config-subif)# encapsulation dot1Q 3` <br>
`router1(config-subif)#ip addr 192.168.3.1 255.255.255.0` <br>
`router1(config-subif)# ip helper-address 192.168.4.2` **эта команда осуществляет ретрансляцию вещательных DHCP-запросов** <br>
`router1(config-subif)# ip nat inside`  **указыываем внутренний интерфейс для NAT**  <br>
`router1(config-subif)#ex`  <br>
`router1(config)# int g0/0.4 `<br>
`router1(config-subif)# encapsulation dot1Q 4` <br>
`router1(config-subif)#ip addr 192.168.4.1 255.255.255.0` <br>
`router1(config-subif)#ex` <br>
`router1(config)# int g0/0.5` **создаем sub-inetface для дальнейшего удалённого подключения к коммутатору** <br>
`router1(config-subif)# encapsulation dot1Q 5` <br>
`router1(config-subif)#ip addr 192.168.5.1 255.255.255.252 ` <br>
`router1(config-subif)#ex` <br>

`router1(config)# access-list 1 permit 192.168.2.0 0.0.0.255` **создаем номерной `лист` доступа и даем разрешение для сети и всех хостов** <br>
`router1(config)# access-list 1 permit 192.168.3.0 0.0.0.255` <br>
`router1(config)# int g0/1` <br>

`router1(config-if)# no shutdown` <br>
`router1(config-if)# ip address 100.100.100.1 255.255.255.252` <br>
`router1(config-if)# ip nat outside` **Указываем исходящий `интерфейс` где происходит подмена ip** <br>
`router1(config-if)# ex` <br>

`router1(config)# ip nat inside source list 1 interface G0/1 overload` **включаем nat указывая какой лист доступа использовать и на каком интерфейсе происходит подмена ip и включаем PAT** <br>
`router1(config)# ip route 0.0.0.0 0.0.0.0 100.100.100.2` **включим маршрутизацию , указав что все `сети находятся за этим адресом`** <br>

`router1(config)#aaa new-model` **задаём новую моедель** <br>
`router1(config)# radius server MY_RADIUS`  **настраиваенм название сервера, и переходим в режим конфигурации** <br>
`router1(config-radius-server)# address ipv4 192.168.4.3 auth-port 1645` **указываем ip адрес сервера и порт на `котором будем работать`** <br>
`router1(config-radius-server)#key DerParol213 ` **задаём пароль , он должен совпадать  с паролем `настроенном на сервере`** <br>
`router1(config-radius-server)# ex` <br>
`router1(config)# aaa authentication login default group radius`   **настраиваем политику аутентификации**  <br>
`router1(config)# aaa authorization exec default local group radius local`   **настраиваем политику авторизации** <br>

`router1(config)# aaa accounting exec default start-stop group radius`   **настраиваем политику учёта** <br>
`router1(config)# ip ftp username admin_FTP`  **Настраиваем имя пользователя для FTP-соединений** <br>
`router1(config)# ip ftp password cisco`   **Настраиваем пароль пользователя для FTP-соединений** <br>
`router1(config)# ex`<br>
`router1# copy running-config ftp:`   **Делаем backup** <br>
`Address or name of remote host []? 192.168.4.4`  **указываем адрес FTP сервера** <br>
`Destination filename []? Router1_conf`   **Указываем названия файла** <br>










