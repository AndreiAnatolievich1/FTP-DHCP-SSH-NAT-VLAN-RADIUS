`switch0> en`<br>
`switch0# conf t`<br>
`switch0(config)#hostname core-Switch`<br>
`core-Switch(config)# enable secret Tomilino123` <br>
`core-Switch(config)# service password-encryption` <br>

`core-Switch(config)#vlan 2`<br>
`core-Switch(config-vlan)# name user`<br>
`core-Switch(config-vlan)# ex`<br>
`core-Switch(config)#vlan 3`<br>
`core-Switch(config-vlan)# name guest`<br>
`core-Switch(config-vlan)# ex`<br>
`core-Switch(config)#vlan 4`<br>
`core-Switch(config-vlan)# name server`<br>
`core-Switch(config-vlan)# ex`<br>
`core-Switch(config)#vlan 5`<br>
`core-Switch(config-vlan)# name switch1`<br>
`core-Switch(config-vlan)# ex`<br>
`core-Switch(config)#int vlan 5`<br>
`core-Switch(config-if)#ip address 192.168.5.4 255.255.255.252` <br>
`core-Switch(config-if)# ip default-gateway 192.168.5.1` <br>
`core-Switch(config-if)# ex`<br>

`core-Switch(config)#int range f0/1-3` <br>
`core-Switch(config-if-range)#switchport mode trunk` <br>
`core-Switch(config-if-range)#switchport trunk all vlan 2,3,4,5`<br>
`core-Switch(config-if-range)#ex`<br>
`core-Switch(config)#int range f0/10-11`<br>
`core-Switch(config-if-range)#switchport mode access`  <br>
`core-Switch(config-if)#switchport access vlan 4`  <br>
`core-Switch(config-if-range)#ex`<br>

`core-Switch(config)# username admin_Csw privilege 15 secret Pa$$w0rd123` <br>
`core-Switch(config)# line console 0` <br>
`core-Switch(config-line)# login local` <br>
`core-Switch(config-line)#en`<br>
`core-Switch(config)# line vty 0 15` <br>
`core-Switch(config-line)# login local`<br>
`core-Switch(config-line)# transport input ssh` <br>
`core-Switch(config-line)# login authentication default`<br>
`core-Switch(config-line)# en`<br>

`core-Switch(config)#ip domain-name test1.local` <br>
`core-Switch(config)#crypto key generate rsa general-keys modulus 2048` <br>

`core-Switch(config)#aaa new-model`<br>
`core-Switch(config)#radius-server host 192.168.4.2 auth-port 1645`<br>
`core-Switch(config)#radius-server key DerParol12`<br>
`core-Switch(config)#aaa authentication login default group radius`<br>
`core-Switch(config)#aaa authorization exec default local group radius local`<br>
`core-Switch(config)#aaa accounting exec default start-stop group radius`<br>

`core-Switch(config)# ip ftp username admin_FTP`  <br>
`core-Switch(config)# ip ftp password cisco`   <br>
`core-Switch(config)# ex`<br>
`core-Switch# copy running-config ftp:`  <br>
`Address or name of remote host []? 192.168.4.4`   <br>
`Destination filename []? CoreSwitch_conf`  <br>
