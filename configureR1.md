
`router> en` <br>
`router# conf t`<br>
`router(config)# enable secret Tomil123` **задаём пароль на enable** <br>
`router(config)# service password-encryption ` **теперь пароль храниться в хэшированном виде, а не открытом**<br>
`router(config)# hostname andr `**Изменение имени устройства на "andr, необходимо для настройки SSh**<br>
`andr(config)# username admin privilege 15 secret Tomil123 `**задаём пользователя с максимальными правами**<br>
`andr(config)# username adrei privilege 15 secret Tomil123 `**задаём пользователя с минимальными правами**<br>
`andr(config)# line console 0 `**переходим в режим настройки консольного подключения**<br>
`andr(config-line)# login local `**nребование аутентификации по локальной базе пользователей при подключении через консоль**<br>
`andr(config-line)#en`<br>
`andr(config)# line vty 0 15 `**Переход в режим настройки виртуальных терминальных линий (VTY) с 0 по 15. Эти линии используются для удаленного доступа (Telnet/SSH).**<br>
`andr(config-line)# login local `<br>
`andr(config-line)# transport input ssh `**Разрешение только SSH подключений на VTY линиях**<br>
`andr(config-line)# en`<br>
`andr(config)#ip domain-name test.local `**Установка доменного имени для устройства. Это необходимо для генерации RSA ключей, которые используются в SSH**<br>
`andr(config)#crypto key generate rsa general-keys modulus 2048` **Генерируем ключи шифрования**<br>
`andr(config)# int g0/1 `**Переходим в режим настройки интерфейса**<br>
`andr(config-if)# no shutdown `**физически включаем интерфейс**<br>
`andr(config-if)#ex`<br>
`andr(config)# int g0/1.2 `**создаем sub-inetface**<br>
`andr(config-subif)# encapsulation dot1Q 2 `** включаем инкапсуляцию трафика**<br>
`andr(config-subif)#ip addr 192.168.2.1 255.255.255.252 `**задаём ip адресс шлюза по умолчаннию и маску сети**<br>
`andr(config-subif)#ex`<br>
`andr(config)# int g0/1.3`<br>
`andr(config-subif)# encapsulation dot1Q 3`<br>
`andr(config-subif)#ip addr 192.168.3.1 255.255.255.0`<br>
`andr(config-subif)# ip helper-address 192.168.2.2` *эта команда осуществляет ретрансляцию вещательных DHCP-запросов *<br>
`andr(config-subif)# ip nat inside `**указыываем внутренний интерфейс для NAT**<br>
`andr(config-subif)#ex`<br>
`andr(config)# int g0/1.4 `<br>
`andr(config-subif)# encapsulation dot1Q 4`<br>
`andr(config-subif)#ip addr 192.168.4.1 255.255.255.0 `<br>
`andr(config-subif)# ip helper-address 192.168.2.2`<br>
`andr(config-subif)# ip nat inside`<br>
`andr(config-subif)#ex`<br>
`andr(config)# int g0/1.5 `**создаем sub-inetface для дальнейшего удалённого подключения к коммутатору**<br>
`andr(config-subif)# encapsulation dot1Q 5 `<br>
`andr(config-subif)#ip addr 192.168.5.1 255.255.255.252 `<br>
`andr(config-subif)#ex`<br>
`andr(config)# access-list 1 permit 192.168.3.0 0.0.0.255` **создаем номерной лист доступа и даем разрешение для сети и всех хостов**<br>
`andr(config)# access-list 1 permit 192.168.3.0 0.0.0.255 `<br>
`andr(config)# ip nat inside source list 1 interface G0/0 overload `**включаем nat указывая какой лист доступа использовать на каком интерфейсе происходит подмена ip и включаем PAT**<br>
`andr(config)# ip route 0.0.0.0 0.0.0.0 100.100.100.2 `**включим маршрутизацию , указав что все сети находятся за этим адресом**<br>
