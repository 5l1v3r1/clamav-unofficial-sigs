# Basic guide to Installing on Ubuntu / Debian

# CLAMAV INSTALL INSTRUCTIONS
# Install clamav
```
apt-get update && apt-get install -y clamav-base clamav-freshclam clamav clamav-daemon
```

## Make sure you do not have the package installed via apt
```
apt-get purge -y clamav-unofficial-sigs
```

## Install
Run the following commands in shell (console/terminal)
```
mkdir -p /usr/local/sbin/
wget https://raw.githubusercontent.com/extremeshok/clamav-unofficial-sigs/master/clamav-unofficial-sigs.sh -c -O /usr/local/sbin/clamav-unofficial-sigs.sh && chmod 755 /usr/local/sbin/clamav-unofficial-sigs.sh
mkdir -p /etc/clamav-unofficial-sigs/
wget https://raw.githubusercontent.com/extremeshok/clamav-unofficial-sigs/master/conf/master.conf -c -O /etc/clamav-unofficial-sigs/master.conf
wget https://raw.githubusercontent.com/extremeshok/clamav-unofficial-sigs/master/conf/user.conf -c -O /etc/clamav-unofficial-sigs/user.conf
```
Select your operating system config from https://github.com/extremeshok/clamav-unofficial-sigs/tree/master/config/
**replace os.centos7.conf with your required config, centos6 = os.centos6.conf, centos7-atomic = os.centos7-atomic.conf, centos6-cpanel = os.centos6-cpanel.conf**
```
os_conf="os.centos7.conf"
wget "https://raw.githubusercontent.com/extremeshok/clamav-unofficial-sigs/master/conf/os/${os_conf}" -c -O /etc/clamav-unofficial-sigs/os.conf
```

### Optional: configure your user config /etc/clamav-unofficial-sigs/user.conf

## RUN THE SCRIPT ONCE AS ROOT
ensure there are no errors, fix any missing dependencies
script must run once as your superuser to set all the permissions and create the relevant directories
```
/usr/local/sbin/clamav-unofficial-sigs.sh --force
```

### Install logrotate and Man files
```
/usr/local/sbin/clamav-unofficial-sigs.sh --install-logrotate
/usr/local/sbin/clamav-unofficial-sigs.sh --install-man
```

### Install Systemd configs or use cron
#### cron
```
/usr/local/sbin/clamav-unofficial-sigs.sh --install-cron
```
### OR
#### systemd
```
wget https://raw.githubusercontent.com/extremeshok/clamav-unofficial-sigs/master/systemd/clamav-unofficial-sigs.service -c -O /etc/systemd/system/clamav-unofficial-sigs.service
wget https://raw.githubusercontent.com/extremeshok/clamav-unofficial-sigs/master/systemd/clamav-unofficial-sigs.timer -c -O /etc/systemd/system/clamav-unofficial-sigs.timer
wget https://raw.githubusercontent.com/extremeshok/clamav-unofficial-sigs/master/systemd/clamd.scan.service -c -O /etc/systemd/system/clamd.scan.service
```