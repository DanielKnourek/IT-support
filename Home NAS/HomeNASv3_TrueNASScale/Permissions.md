# Permissions for SMB share

## ~/HomeArchive/HomeArchiveData

```BASH
sudo -i
cd /mnt/HomeArchive/HomeArchiveData
install -d -m 0770 -o daniel -g noFamily Daniel/
install -d -m 0770 -o vaclav -g noFamily Táta/
install -d -m 0770 -o vasek -g noFamily Vašek/
install -d -m 0770 -o blanka -g noFamily Mamča/

install -d -m 0770 -o root -g Family Společné/
install -d -m 0770 -o root -g Family Media/

chmod 770 Společné/

nfs4xdr_getfacl Mamča/ | nfs4xdr_setfacl -X Mamča/ 
sudo nfs4xdr_getfacl Společné/ | nfs4xdr_setfacl -X - Společné/
nfs4xdr_getfacl Společné/ | tail -n +7 | nfs4xdr_setfacl -X - Společné/
nfs4xdr_getfacl Společné/ | tail -n +7 | nfs4xdr_setfacl -X Společné/ Společné/
nfs4_getfacl Společné/ | tail -n +7 | nfs4xdr_setfacl -X Společné/ Společné/
nfs4xdr_getfacl Společné/ | tail -n +7 | nfs4xdr_setfacl -x - Společné/
nfs4xdr_getfacl Společné/ | grep @ | nfs4xdr_getfacl -S - Společné/
chmod A- Společné
```
<!-- 
# File: ./Mamča
# owner: 1004
# group: 1005
# mode: 0o40770
# trivial_acl: false
# ACL flags: none
            owner@:-----d--------:------I:deny
            owner@:rwxpDdaARWc--s:fd----I:allow
            group@:rwxpDdaARWc--s:fd----I:allow
         everyone@:--------------:fd----I:allow
            group@:r-x---a-R-c---:fd----I:allow 
-->