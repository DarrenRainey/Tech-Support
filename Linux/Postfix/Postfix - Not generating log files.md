# Postfix - Not generating log files

## Description
New postfix install not creating log files at /var/log/mail.log

## Solution
Check if rsyslogd is running orr installed otherwise install it and restart postfix with the following commands (Debian Based distro's):
```
sudo apt install rsyslogd -y
service postfix restart
```
