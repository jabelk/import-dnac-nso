# import-dnac-nso.py
Cisco DNA Center Lab 3
https://devnetsandbox.cisco.com/RM/Topology

results
```
[root@devbox belk-code]# python3 import-dnac-nso.py
Host1.abc.inc 10.10.20.83
Host2 10.10.20.84
leaf1.abc.inc 10.10.20.81
Setting device leaf1.abc.inc configuration...
Committing the device configuration...
Committed
Fetching SSH keys...
Result: updated
Syncing configuration...
Result: True
leaf2.abc.inc 10.10.20.82
Setting device leaf2.abc.inc configuration...
Committing the device configuration...
Committed
Fetching SSH keys...
Result: updated
Syncing configuration...
Result: True
spine1.abc.inc 10.10.20.80
Setting device spine1.abc.inc configuration...
Committing the device configuration...
Committed
Fetching SSH keys...
Result: updated
Syncing configuration...
Result: True
[root@devbox belk-code]#
```


```
sudo yum install ant
# download NSO from website to home directory
sh nso-5.2.1.linux.x86_64.signed.bin
sh nso-5.2.1.linux.x86_64.installer.bin --dest nso-install
sh nso-5.2.1.linux.x86_64.installer.bin  nso-install
source /root/nso-install/ncsrc
ncs-setup --dest nso-run
echo 'export DNA_CENTER_USERNAME=admin'
echo 'export DNA_CENTER_USERNAME=admin' >> ~/.bashrc
echo 'export DNA_CENTER_PASSWORD=Cisco1234!' >> ~/.bashrc
echo 'export DNA_CENTER_BASE_URL=10.10.20.85' >> ~/.bashrc
echo 'source /root/nso-install/ncsrc' >> ~/.bashrc
echo 'export DNA_CENTER_VERIFY=False' >> ~/.bashrc
source .bashrc
git clone https://github.com/cisco-en-programmability/dnacentersdk.git
cd dnacentersdk/
python3.6 setup.py install

#add authgroup
devices authgroups group dnac default-map remote-name admin remote-password ciscopsdt


#remove lines forcing to go to python2

[root@devbox nso-run]# cat  $NCS_DIR/bin/ncs-start-python-vm
#!/bin/sh

pypath="${NCS_DIR}/src/ncs/pyapi"
dnacenterpath="/usr/local/lib/python3.6/site-packages"
# Make sure everyone finds the NCS Python libraries at startup
if [ "x$PYTHONPATH" != "x" ]; then
    PYTHONPATH=${dnacenterpath}:${pypath}:$PYTHONPATH
else
    PYTHONPATH=${dnacenterpath}:${pypath}
fi
export PYTHONPATH

main="${pypath}/ncs_pyvm/startup.py"

echo "Starting python -u $main $*"
exec python3 -u "$main" "$@"
```
