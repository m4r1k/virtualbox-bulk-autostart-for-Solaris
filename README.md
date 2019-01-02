# Virtualbox VM Bulk Autostart (and stopstop)

1) Copy file on the Virtualbox headless Solaris server

2) Exec the following commands

```
chmod +x virtualbox-bulk-autostart

cp virtualbox-bulk-autostart /usr/sbin/

mkdir /lib/svc/manifest/application/virtualbox

cp virtualbox-bulk-autostart.xml /lib/svc/manifest/application/virtualbox/

svcadm restart manifest-import

svcadm enable svc:/application/virtualbox/bulk-autostart:default

svcs -vL svc:/application/virtualbox/bulk-autostart:default

svcs -x svc:/application/virtualbox/bulk-autostart:default
```

# Docs
https://docs.oracle.com/cd/E53394_01/html/E54799/dzhid.html#indexterm-id-14
https://docs.oracle.com/cd/E53394_01/html/E54799/profsvcbndl.html#indexterm-id-266
https://docs.oracle.com/cd/E26502_01/html/E29003/eqbrs.html

# About VBOX Official autostart
https://learnings-on-solaris.blogspot.nl/2017/04/virtualbox-vm-autostart.html
