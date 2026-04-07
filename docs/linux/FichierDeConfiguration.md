# Contexte CUB 

## Fichier de configuration Switch lV2 

```
version 15.0
no service pad
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname switchLv2
!
boot-start-marker
boot-end-marker
!
!
username etudiant privilege 15 secret 4 XJs1kDT984d4u/RcgM1oWYsonq4S11mG8xa9fZJ0J8Q
no aaa new-model
system mtu routing 1500
!
!
ip domain-name btssio2.lan
!
spanning-tree mode pvst
spanning-tree extend system-id
!
vlan internal allocation policy ascending
!
ip ssh version 2
!
!
!
!
!
interface FastEthernet0/1
 switchport access vlan 10
!         
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
 switchport access vlan 20
!
interface FastEthernet0/14
 switchport access vlan 20
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!         
interface FastEthernet0/25
!
interface FastEthernet0/26
!
interface FastEthernet0/27
!
interface FastEthernet0/28
!
interface FastEthernet0/29
!
interface FastEthernet0/30
!
interface FastEthernet0/31
!
interface FastEthernet0/32
!
interface FastEthernet0/33
!
interface FastEthernet0/34
!
interface FastEthernet0/35
!
interface FastEthernet0/36
!         
interface FastEthernet0/37
!
interface FastEthernet0/38
!
interface FastEthernet0/39
!
interface FastEthernet0/40
!
interface FastEthernet0/41
!
interface FastEthernet0/42
!
interface FastEthernet0/43
!
interface FastEthernet0/44
!
interface FastEthernet0/45
 switchport trunk allowed vlan 10,20,52
 switchport mode trunk
!
interface FastEthernet0/46
!
interface FastEthernet0/47
!         
interface FastEthernet0/48
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
!
interface Vlan20
 ip address 192.168.2.193 255.255.255.240
!
ip http server
ip http secure-server
!
!
line con 0
line vty 0 4
 login local
 transport input ssh
line vty 5 15
 login
!
end       
```
<b>

## Fichier de configuration SwitchLV3

```
version 17.6
service timestamps debug datetime msec
service timestamps log datetime msec
! Call-home is enabled by Smart-Licensing.
service call-home
platform punt-keepalive disable-kernel-core
!
hostname switchLvL3
!
!
vrf definition Mgmt-vrf
 !
 address-family ipv4
 exit-address-family
 !
 address-family ipv6
 exit-address-family
!
!         
!
!
!
no aaa new-model
switch 1 provision c9200l-24t-4g
!
!
!
!
!
!
!
!
!
ip routing
!
ip domain name local.barcelone.cub.sioplc.fr
!
!
!
login on-success log
!
crypto pki trustpoint SLA-TrustPoint
 enrollment pkcs12
 revocation-check crl
!
crypto pki trustpoint TP-self-signed-1295377663
 enrollment selfsigned
 subject-name cn=IOS-Self-Signed-Certificate-1295377663
 revocation-check none
 rsakeypair TP-self-signed-1295377663
!
!
crypto pki certificate chain SLA-TrustPoint
 certificate ca 01
  30820321 30820209 A0030201 02020101 300D0609 2A864886 F70D0101 0B050030 
  32310E30 0C060355 040A1305 43697363 6F312030 1E060355 04031317 43697363 
  6F204C69 63656E73 696E6720 526F6F74 20434130 1E170D31 33303533 30313934 
  3834375A 170D3338 30353330 31393438 34375A30 32310E30 0C060355 040A1305 
  43697363 6F312030 1E060355 04031317 43697363 6F204C69 63656E73 696E6720 
  526F6F74 20434130 82012230 0D06092A 864886F7 0D010101 05000382 010F0030 
  82010A02 82010100 A6BCBD96 131E05F7 145EA72C 2CD686E6 17222EA1 F1EFF64D 
  CBB4C798 212AA147 C655D8D7 9471380D 8711441E 1AAF071A 9CAE6388 8A38E520 
  1C394D78 462EF239 C659F715 B98C0A59 5BBB5CBD 0CFEBEA3 700A8BF7 D8F256EE 
  4AA4E80D DB6FD1C9 60B1FD18 FFC69C96 6FA68957 A2617DE7 104FDC5F EA2956AC 
  7390A3EB 2B5436AD C847A2C5 DAB553EB 69A9A535 58E9F3E3 C0BD23CF 58BD7188 
  68E69491 20F320E7 948E71D7 AE3BCC84 F10684C7 4BC8E00F 539BA42B 42C68BB7 
  C7479096 B4CB2D62 EA2F505D C7B062A4 6811D95B E8250FC4 5D5D5FB8 8F27D191 
  C55F0D76 61F9A4CD 3D992327 A8BB03BD 4E6D7069 7CBADF8B DF5F4368 95135E44 
  DFC7C6CF 04DD7FD1 02030100 01A34230 40300E06 03551D0F 0101FF04 04030201 
  06300F06 03551D13 0101FF04 05300301 01FF301D 0603551D 0E041604 1449DC85 
  4B3D31E5 1B3E6A17 606AF333 3D3B4C73 E8300D06 092A8648 86F70D01 010B0500 
  03820101 00507F24 D3932A66 86025D9F E838AE5C 6D4DF6B0 49631C78 240DA905 
  604EDCDE FF4FED2B 77FC460E CD636FDB DD44681E 3A5673AB 9093D3B1 6C9E3D8B 
  D98987BF E40CBD9E 1AECA0C2 2189BB5C 8FA85686 CD98B646 5575B146 8DFC66A8 
  467A3DF4 4D565700 6ADF0F0D CF835015 3C04FF7C 21E878AC 11BA9CD2 55A9232C 
  7CA7B7E6 C1AF74F6 152E99B7 B1FCF9BB E973DE7F 5BDDEB86 C71E3B49 1765308B 
  5FB0DA06 B92AFE7F 494E8A9E 07B85737 F3A58BE1 1A48A229 C37C1E69 39F08678 
  80DDCD16 D6BACECA EEBC7CF9 8428787B 35202CDC 60E4616A B623CDBD 230E3AFB 
  418616A9 4093E049 4D10AB75 27E86F73 932E35B5 8862FDAE 0275156F 719BB2F0 
  D697DF7F 28
        quit
crypto pki certificate chain TP-self-signed-1295377663
 certificate self-signed 01
  30820330 30820218 A0030201 02020101 300D0609 2A864886 F70D0101 05050030 
  31312F30 2D060355 04031326 494F532D 53656C66 2D536967 6E65642D 43657274 
  69666963 6174652D 31323935 33373736 3633301E 170D3236 30333033 30383432 
  34325A17 0D333630 33303230 38343234 325A3031 312F302D 06035504 03132649 
  4F532D53 656C662D 5369676E 65642D43 65727469 66696361 74652D31 32393533 
  37373636 33308201 22300D06 092A8648 86F70D01 01010500 0382010F 00308201 
  0A028201 0100B574 C6A8D8CA 6FE7C3A4 2E482B41 6FE80B74 9A939FD0 687B24F8 
  645191C3 2EC99374 524E40F1 6AEB3CAF 5CE777D2 2C466C3B F43C139F F04D3421 
  FC8505E8 E14F055D 6B2ED3BA 1EC7C5BC 9A1AFF30 E5860E21 5DF171FE CCFC6089 
  0C931ECA 582647DD FB17AC65 116A4649 7E6553F5 0383B7D2 F655B4C1 E54C0EE0 
  662E2306 E827B1A1 63B1CE74 1623D364 AE9CE3B0 9BF1B497 B4DD2E53 DC957BB6 
  03690C02 98899609 6139C83D 2DA33E89 6796EF78 BAEF4680 BBFE6A4B C26F55E0 
  DFCFAD07 CEF5EFCF BA9963F6 A09B6066 9378B3C0 31EA0C1F 2D502177 1A439692 
  746FBF92 EEE061B3 AB5C3DD2 20D9804B 49BD9F9C 3EEDA12A 80DC97BD 1FE7CCA6 
  73F54BC0 AC9B0203 010001A3 53305130 0F060355 1D130101 FF040530 030101FF 
  301F0603 551D2304 18301680 14B98872 C1BF04A0 4A2A2480 87931CC4 CC93E756 
  3A301D06 03551D0E 04160414 B98872C1 BF04A04A 2A248087 931CC4CC 93E7563A 
  300D0609 2A864886 F70D0101 05050003 82010100 02D29431 FD89852E C2A937CC 
  716E82B9 7833CE54 510E2F89 F66CFDFA 6DB35F5D 4D2C2116 CBA0C5C8 FD343317 
  74610B88 9469774D A95A511E 4DACBAA0 C4742FC7 CFF21E13 4FE07E22 2A9A1EA7 
  1B9129E1 82AEE6CE 6F991B51 5DD5331C B7849E10 5532EF42 6D0F689B E68F3957 
  9B226B87 9040C892 D304F83A BCC3CEA4 BA562E46 9CF62E2F 57E2969F 5CB196B5 
  6139877D 5E7EA3FC 5B3EF542 85D95696 D482A9DE 21A194D8 7EF61B3D 9C3C010A 
  D97F60B1 704A59F6 315EC048 2B139B79 41D7A635 D1194935 D920E0C1 FCA81324 
  66BB9AE5 7797718E 8B5FDE3D F1050245 0D869FB5 12F8D17C 0E909AB9 E87DD0AC 
  CDD59EFA B7EE045F EA822825 E049573E C97053F7
        quit
!         
license boot level network-essentials addon dna-essentials
!
!
diagnostic bootup level minimal
!
spanning-tree mode rapid-pvst
spanning-tree extend system-id
memory free low-watermark processor 10626
!
username etudiant privilege 15 password 0 etudiant_007
!
redundancy
 mode sso
!
!
transceiver type all
 monitoring
!
!
class-map match-any system-cpp-police-ewlc-control
  description EWLC Control 
class-map match-any system-cpp-police-topology-control
  description Topology control
class-map match-any system-cpp-police-sw-forward
  description Sw forwarding, L2 LVX data packets, LOGGING, Transit Traffic
class-map match-any system-cpp-default
  description EWLC data, Inter FED Traffic 
class-map match-any system-cpp-police-sys-data
  description Openflow, Exception, EGR Exception, NFL Sampled Data, RPF Failed
class-map match-any system-cpp-police-punt-webauth
  description Punt Webauth
class-map match-any system-cpp-police-l2lvx-control
  description L2 LVX control packets
class-map match-any system-cpp-police-forus
  description Forus Address resolution and Forus traffic
class-map match-any system-cpp-police-multicast-end-station
  description MCAST END STATION
class-map match-any system-cpp-police-high-rate-app
  description High Rate Applications 
class-map match-any system-cpp-police-multicast
  description MCAST Data
class-map match-any system-cpp-police-l2-control
  description L2 control
class-map match-any system-cpp-police-dot1x-auth
  description DOT1X Auth
class-map match-any system-cpp-police-data
  description ICMP redirect, ICMP_GEN and BROADCAST
class-map match-any system-cpp-police-stackwise-virt-control
  description Stackwise Virtual OOB
class-map match-any non-client-nrt-class
class-map match-any system-cpp-police-routing-control
  description Routing control and Low Latency
class-map match-any system-cpp-police-protocol-snooping
  description Protocol snooping
class-map match-any system-cpp-police-dhcp-snooping
  description DHCP snooping
class-map match-any system-cpp-police-ios-routing
  description L2 control, Topology control, Routing control, Low Latency
class-map match-any system-cpp-police-system-critical
  description System Critical and Gold Pkt
class-map match-any system-cpp-police-ios-feature
  description ICMPGEN,BROADCAST,ICMP,L2LVXCntrl,ProtoSnoop,PuntWebauth,MCASTData,Transit,DOT1XAuth,Swfwd,LOGGING,L2LVXData,ForusTraffic,ForusARP,McastEndStn,Openflow,Exception,EGRExcption,NflSampledd
!
policy-map system-cpp-policy
!
! 
!         
!
!
!
!
!
!
!
!
!
!
!
interface GigabitEthernet0/0
 vrf forwarding Mgmt-vrf
 no ip address
 shutdown
!
interface GigabitEthernet1/0/1
 switchport access vlan 52
!
interface GigabitEthernet1/0/2
 switchport access vlan 52
!
interface GigabitEthernet1/0/3
!
interface GigabitEthernet1/0/4
!
interface GigabitEthernet1/0/5
!
interface GigabitEthernet1/0/6
!
interface GigabitEthernet1/0/7
!
interface GigabitEthernet1/0/8
!
interface GigabitEthernet1/0/9
!
interface GigabitEthernet1/0/10
!
interface GigabitEthernet1/0/11
!
interface GigabitEthernet1/0/12
!
interface GigabitEthernet1/0/13
 switchport access vlan 22
 switchport mode access
!         
interface GigabitEthernet1/0/14
!
interface GigabitEthernet1/0/15
!
interface GigabitEthernet1/0/16
!
interface GigabitEthernet1/0/17
!
interface GigabitEthernet1/0/18
!
interface GigabitEthernet1/0/19
!
interface GigabitEthernet1/0/20
!
interface GigabitEthernet1/0/21
 switchport trunk allowed vlan 10,20,52
 switchport mode trunk
!
interface GigabitEthernet1/0/22
!
interface GigabitEthernet1/0/23
!
interface GigabitEthernet1/0/24
!
interface GigabitEthernet1/1/1
!
interface GigabitEthernet1/1/2
!
interface GigabitEthernet1/1/3
!
interface GigabitEthernet1/1/4
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan10
 ip address 192.168.2.190 255.255.255.192
 ip helper-address 192.168.2.1
 ip helper-address 192.168.2.2
!
interface Vlan20
 ip address 192.168.2.206 255.255.255.240
 ip helper-address 192.168.2.1
 ip helper-address 192.168.2.2
!         
interface Vlan22
 ip address 192.168.22.253 255.255.255.240
!
interface Vlan52
 ip address 192.168.2.126 255.255.255.128
!
ip forward-protocol nd
ip http server
ip http authentication local
ip http secure-server
ip route 0.0.0.0 0.0.0.0 192.168.22.254
ip ssh version 2
!
!
ip access-list extended reseau-admin
 10 permit icmp 192.168.2.192 0.0.0.15 any echo
 20 deny   ip 192.168.2.192 0.0.0.15 192.168.2.128 0.0.0.63
 30 deny   tcp 192.168.2.192 0.0.0.15 192.168.2.0 0.0.0.127 eq 22
 40 deny   tcp 192.168.2.192 0.0.0.15 192.168.2.0 0.0.0.127 eq 3389
 60 permit ip 192.168.2.192 0.0.0.15 host 192.168.2.2
 70 permit ip 192.168.2.192 0.0.0.15 host 192.168.2.110
 80 permit ip 192.168.2.192 0.0.0.15 host 192.168.2.111
 90 permit udp 192.168.2.192 0.0.0.15 host 192.168.2.10 eq domain
 100 permit udp 192.168.2.192 0.0.0.15 host 192.168.2.11 eq domain
 110 permit tcp 192.168.2.192 0.0.0.15 host 192.168.2.125 eq 8080
 120 deny   ip 192.168.2.192 0.0.0.15 192.168.2.0 0.0.0.127
 130 permit ip 192.168.2.192 0.0.0.15 any
ip access-list extended reseau-client
 10 permit tcp any any established
 20 permit icmp 192.168.2.128 0.0.0.63 any echo-reply
 30 permit udp 192.168.2.128 0.0.0.63 host 192.36.2.10 eq domain
 40 permit udp 192.168.2.128 0.0.0.63 host 192.36.2.11 eq domain
 50 permit udp any eq bootps any eq bootpc
 60 deny   tcp 192.168.2.128 0.0.0.63 192.168.2.0 0.0.0.127 eq 22
 70 deny   tcp 192.168.2.128 0.0.0.63 192.168.2.0 0.0.0.127 eq 3389
 80 permit ip 192.168.2.128 0.0.0.63 host 192.168.2.1
 90 permit ip 192.168.2.128 0.0.0.63 host 192.168.2.2
 100 permit ip 192.168.2.128 0.0.0.63 host 192.168.2.110
 110 permit ip 192.168.2.128 0.0.0.63 host 192.168.2.111
 120 deny   ip 192.168.2.128 0.0.0.63 192.168.2.0 0.0.0.127
 130 deny   ip 192.168.2.128 0.0.0.63 192.168.2.192 0.0.0.15
 140 permit ip 192.168.2.128 0.0.0.63 any
ip access-list extended reseau-production
 10 permit tcp any any established
 20 permit icmp 192.168.2.0 0.0.0.127 any echo-reply
 30 permit udp host 192.168.2.10 eq domain any
 40 permit udp host 192.168.2.11 eq domain any
 50 permit udp host 192.168.2.1 eq bootps any
 60 permit udp host 192.168.2.2 eq bootps any
 70 deny   ip 192.168.2.0 0.0.0.127 192.168.2.192 0.0.0.15
 80 deny   ip 192.168.2.0 0.0.0.127 192.168.2.128 0.0.0.63
 90 permit ip 192.168.2.0 0.0.0.127 any
!
!
control-plane
 service-policy input system-cpp-policy
!
!
line con 0
 stopbits 1
line aux 0
line vty 0 4
 login local
 transport input ssh
line vty 5
 login local
 transport input ssh
line vty 6 15
 login    
 transport input ssh
!
call-home
 ! If contact email address in call-home is configured as sch-smart-licensing@cisco.com
 ! the email address configured in Cisco Smart License Portal will be used as contact email address to send SCH notifications.
 contact-email-addr sch-smart-licensing@cisco.com
 profile "CiscoTAC-1"
  active
  destination transport-method http
!
!
!
!
!
!
end
```