# Configuration Asterisk

## Fichier : `/etc/asterisk/iax.conf`

```ini
[general]
bindport=4569
bindaddr=0.0.0.0
tos=ef
cos=5

[enzo_in]
type=user
context=from-internal
auth=md5
secret=etudiant_007
disallow=all
allow=ulaw
allow=alaw

[enzo_out]
type=peer
host=172.16.55.130
username=sefa_in
secret=etudiant_007
auth=md5
qualify=yes
disallow=all
allow=ulaw
allow=alaw
trunk=yes
Fichier : /etc/asterisk/pjsip.conf
[transport-udp]
type=transport
protocol=udp
bind=0.0.0.0:5060
tos=cs3
cos=3

[1001]
type=endpoint
context=from-internal
disallow=all
allow=ulaw,alaw,gsm
auth=auth1001
aors=1001
rewrite_contact=yes
rtp_symmetric=yes
force_rport=yes

[auth1001]
type=auth
auth_type=userpass
username=1001
password=1234

[1001]
type=aor
max_contacts=1
qualify_frequency=30

[1002]
type=endpoint
context=from-internal
disallow=all
allow=ulaw,alaw,gsm
auth=auth1002
aors=1002
rewrite_contact=yes
rtp_symmetric=yes
force_rport=yes

[auth1002]
type=auth
auth_type=userpass
username=1002
password=1234

[1002]
type=aor
max_contacts=1
qualify_frequency=30
Fichier : /etc/asterisk/extensions.conf
[from-internal]
exten => 1001,1,Dial(PJSIP/1001)
 same => n,Hangup()

exten => 1002,1,Dial(PJSIP/1002)
 same => n,Hangup()

exten => 101,1,Dial(IAX2/enzo_out/101)
 same => n,Hangup()
Configuration QoS
Pare-feu

Le pare-feu applique le marquage QoS sur le trafic VoIP :

DSCP : EF (46)
Priorité : haute / temps réel
Switch L2
conf t
interface range fa0/1-2
mls qos trust dscp
end
Switch L3 (ports accès)
conf t
interface range GigabitEthernet1/0/1-2
trust dscp
end
Switch L3 (trunks)
conf t
interface range GigabitEthernet1/0/21-24
trust dscp
end
Explication QoS

Le DSCP est défini par le pare-feu ou par les équipements VoIP.

Exemple :

VoIP -> DSCP EF (46)

Le switch ne modifie pas les paquets. Il applique uniquement :

trust dscp

Cela signifie qu’il fait confiance au marquage déjà présent dans les paquets.

Conclusion

La solution VoIP est fonctionnelle avec :

SIP pour les postes locaux
IAX pour l’interconnexion entre les serveurs
QoS mise en place sur le pare-feu
Switches configurés en trust DSCP pour conserver la priorité du trafic voix