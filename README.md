# VirtualBox VM Bulk Autostart
## What is virtualbox-bulk-autostart?
**virtualbox-bulk-autostart**, as the name suggests, provides a way to auto-start VirtualBox VM during Solaris boot process in on the global zone. The script is executed by the Solaris' SMF framework. At shutdown, the script tries to gracefully shut down any running VMs and in case of timeout will terminate any blocking ones. *virtualbox-bulk-autostart* also supports excluding VM from the auto-start process. Simply add the word "exclude" in the VM's description.
## Where it has been tested?
Test with the following Solaris versions:
* Oracle Solaris 11.3
* Oracle Solaris 11.4

Test with the following VirtualBox versions:
* Oracle VM VirtualBox 5.2
* Oracle VM VirtualBox 6.0
## Installation Process
* Copy file on the Virtualbox headless Solaris server
* Exec the following commands

```sh
chmod +x virtualbox-bulk-autostart
cp virtualbox-bulk-autostart /usr/sbin/
mkdir /lib/svc/manifest/application/virtualbox
cp virtualbox-bulk-autostart.xml /lib/svc/manifest/application/virtualbox/
svcadm restart manifest-import
svcadm enable svc:/application/virtualbox/bulk-autostart:default
svcs -vL svc:/application/virtualbox/bulk-autostart:default
svcs -x svc:/application/virtualbox/bulk-autostart:default
```

## About Solaris 11.4 and SMAP (Supervisor Mode Access Prevention)
Running VirtualBox on an Oracle Solaris x64 host system with Supervisor Mode Access Prevention (SMAP) enabled might panic the host with a message similar to the following:
```
BAD TRAP: type=e (#pf Page fault) rp=fffffffc802c98e0 addr=ffff80ffbc8ff5e0
occurred in module "<unknown>" due to an illegal access to a user address
```
Workaround: Run the **sxadm disable smap** command and reboot before starting VirtualBox.
https://docs.oracle.com/cd/E37838_01/html/E60973/appcompat.html#SERNSgtaji
## References
* https://docs.oracle.com/cd/E53394_01/html/E54799/dzhid.html#indexterm-id-14
* https://docs.oracle.com/cd/E53394_01/html/E54799/profsvcbndl.html#indexterm-id-266
* https://docs.oracle.com/cd/E26502_01/html/E29003/eqbrs.html
### About VBOX Official autostart
* https://learnings-on-solaris.blogspot.nl/2017/04/virtualbox-vm-autostart.html
* https://www.virtualbox.org/manual/ch10.html#autostart-solaris
