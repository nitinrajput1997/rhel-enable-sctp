# rhel-enable-sctp

### 1. Install kernel-modules-extra and SCTP for the currently installed kernel;
```
yum install -y lksctp-tools lksctp-tools-devel lksctp-tools-doc
```

### 2. Add sctp to /etc/modules-load.d/* to load sctp before systemd-sysctl.service during boot. Loading sctp before systemd-sysctl.service allows the sctp sysctl.conf settings to be effective;
```
sudo vi /etc/modules-load.d/sctp.conf ## add sctp
# cat /etc/modules-load.d/sctp.conf
sctp
```

### 3. sctp is blacklisted by default on installation. Comment out the blacklisting to enable sctp to be loaded.
```
# grep sctp /etc/modprobe.d/*
/etc/modprobe.d/sctp-blacklist.conf:#blacklist sctp
/etc/modprobe.d/sctp_diag-blacklist.conf:#blacklist sctp_diag
```

### 4. Reboot (or simply manually load the module, modprobe sctp)
```
modprobe sctp
```
### 5. Check some command such as ncat provided from the nmap-ncat package to ensure sctp sockets can be created
```
lsmod | grep sctp
```
