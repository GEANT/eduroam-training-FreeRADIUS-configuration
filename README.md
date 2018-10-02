# FreeRADIUS configuration for IdP
FreeRADIUS configuration for the eduroam training, where FreeRADIUS act like simple IdP only authentication service using LDAP for storing user credentials. 

## Instaling FreeRADIUS can be done issuing follow commands : 
```
# yum install freeradius freeradius-utils freeradius-ldap freeradius-doc git wget
# cd /etc
# rm /etc/raddb
# git clone https://github.com/GEANT/eduroam-training-FreeRADIUS-configuration.git raddb
# cd raddb
# git branch -a | grep -v HEAD | perl -ne 'chomp($_); s|^\*?\s*||; if (m|(.+)/(.+)| && not $d{$2}) {print qq(git branch --track $2 $1/$2\n)} else {$d{$_}=1}' | bash -xfs
# chown -R root:radiusd *	 
```
To change inital base DN use follow command like root in /etc/raddb directory :

```
# grep -rli 'dc=training,dc=eduroam,dc=si' * | egrep -v '*README*' | xargs -i@ sed -i 's/dc=training,dc=eduroam,dc=si/dc=new,dc=realm/g' @
# grep -rli 'training.eduroam.si' * | egrep -v '*README*' | xargs -i@ sed -i 's/training\.eduroam\.si/new\.realm/g' @
```

## Instaling eapol_test can be done issuing follow commands : 

[Help link](http://deployingradius.com/scripts/eapol_test/)

```
# yum install libnl-devel openssl-devel
# yum groupinstall "Development tools"
# cd /root
# mkdir sources
# cd sources
# git clone git://w1.fi/hostap.git
# cd hostap/wpa_supplicant/
# cp defconfig .config

edit defconfig to enable (remove #) CONFIG_EAPOL_TEST=y  
# vi defconfig
# make eapol_test
# cp eapol_test /usr/local/bin
```

## Running FreeRADIUS service :
Enable `# systemctl enable radiusd`

Start `# systemctl start radiusd`

Stop `# systemctl stop radiusd`

Debug
```
# radiusd -Xf
# radiusd -XXXXf
# radiusd -xxxxf &
``` 
