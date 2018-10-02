# FreeRADIUS configuration for IdP
FreeRADIUS configuration for the eduroam training, where FreeRADIUS act like simple IdP only authentication service using LDAP for storing user credentials. 

To change inital base DN use follow command like root in /etc/raddb directory :

grep -rli 'dc=training,dc=eduroam,dc=si' * | egrep -v '*README*' | xargs -i@ sed -i 's/dc=training,dc=eduroam,dc=si/new-word/g' @
