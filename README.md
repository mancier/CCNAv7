# CCNAv7 Commands
Catalyst 2960 
## Basic Configurations
```
Switch> enable # Like sudo in unix
Switch# configure terminal # Global Configuration mode
Switch(config)# hostname <desired_name> # change device name
<desired_name>(config)# service password-encryption
<desired_name>(config)# enable secret <new_password> # secret encrypt the password
<desired_name>(config)# banner motd $<text>$ # motd => message of the day ; $ => text delimiter
<desired_name>(config)# banner motd $:ENTER:
- text 1
- text 2
- $
Switch> enable # Like sudo in unix
Switch# configure terminal # Global Configuration mode
Switch(config)# interface fastEthernet 0/1 || int fa0/1
<desired_name>(config-if)# shutdown # off the port
<desired_name>(config-if)# no shutdown # up the port
<desired_name>(config-if)# interface range fa0/11-24 # configure ports from 11 to 24
<desired_name>(config-if-range)# interface range fa0/11-15,fa0/20-24 # range of interfaces
<desired_name>(config-if-range)# interface range fa0/11-15, fa0/20-24, g0/1-2 # range of interfaces
<desired_name>(config-if-range)# description <message>  # is not needded text delimiter
<desired_name>(config-if-range)# shut
<desired_name>(config-if-range)# CTRL+Z # return for priveliged mode
<desired_name># show run # see all the switch configs
```

## Console Config
```
<desired_name># configure terminal
<desired_name>(config)# line console 0
<desired_name>(config-line)# password <pass>
<desired_name>(config-line)# login # enable service the request password for console connections
<desired_name>(config-line)# CTRL+Z
<desired_name># copy running-config startup-config
<desired_name># write
```

## SSH Config
```
<desired_name># configure terminal
<desired_name>(config)# inter vlan 1
<desired_name>(config-if)# ip addr <ip> <net-mask>
<desired_name>(config-if)# ip default-gateway <ip>
<desired_name>(config-if)# no shutdown # redundancy
<desired_name>(config-if)# line vty 0 15 # virtual tty
<desired_name>(config-line)# password <pass>
<desired_name>(config-line)# login
```

## Configure Router
```
> enable
# configure terminal
(confg)# inter g0/0
(confg-if)# ip addr 192.168.0.1 255.255.255.0
(confg-if)# no shut

(confg)# inter g0/1
(confg-if)# ip addr 172.16.0.1 255.255.255.0
(confg-if)# no shut
```

## Config 2 routers
### Rota estática
```
R1(config)# ip route 172.16.0.0 255.255.255.0 G0/1
ou 
R1(config)# ip route 172.16.0.0 255.255.255.0 10.0.0.2
ou 
R1(config)# ip route 172.16.0.0 255.255.255.0 G0/1 10.0.0.2 # Rota totalmente especificada
```
```
R2(config)# ip route 192.168.0.1 255.255.255.0 G0/1
ou
R2(config)# ip route 192.168.0.1 255.255.255.0 10.0.0.1
ou
R2(config)# ip route 192.168.0.1 255.255.255.0 G0/1 10.0.0.1 # Rota totalmente especificada
```

### Rota padrão
```
R1(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2
R2(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.1
```

## Security
```
all(config)# service password-encryption
router-only(config)# security password min-lenght 10

# evade brute force
router(config)# login block-for 120 attemps 3 within 60

# drop inactive connections
(confg-line)# exec-timeout 5 30 # <min> <sec>
```

### Acessos e Usernames
```
(config)# ip ssh version 2
(config)# hostname cpm22
(config)# ip domain-name rockinrio.arpa
(config)# crypto key generate rsa generate-keys modulus 1024
(config)# username victor secret 1020304050
(config)# line vty 0 15
(config-line)# login local # assume o banco de dados local
(config-line)# transport input ssh
```

## Bonus
```
(config)# do <command> # executa como sudo
(config)# no ip domain-lookup # desabilita o lookup de domains
(config)# show ip int b # mostra as configs das interfaces
(config-if)# no ip addr #remove o ip configurado da interface
```
