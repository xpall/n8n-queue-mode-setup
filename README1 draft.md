Initial set up of vps

root@n8n-main:~# history
    1  sudo apt update
    2  sudo apt upgrade
    3  adduser n8n-main
    4  usermod -aG sudo n8n-main

n8n-main@n8n-main:~$ history
    1  cd
    2  cd .s
    3  mkdir .ssh
    4  cd .ssh/
    5  sudo vim authorized_keys

n8n-main@n8n-main:~$ sudo vim /etc/ssh/sshd_config
PasswordAuthentication from yes to no
PermitRootLogin from yes to no
UsePAM from yes to no

Some vps providers have an extra file in /etc/ssh/sshd_config.d/50-cloud-init.conf

PasswordAuthentication from yes to no

n8n-main@n8n-main:~$ history
    9  cd /etc/ssh/sshd_config.d/
   10  ls
   11  cd
   12  sudo systemctl reload ssh
   13  sudo apt install ufw
   14  sudo ufw default deny incoming
   15  sudo ufw default allow outgoing
   16  sudo ufw allow OpenSSH
   17  sudo ufw show added
   18  sudo ufw enable


n8n-main@n8n-main:~$ history 4
   21  sudo apt install unattended-upgrades
   22  sudo dpkg-reconfigure unattended-upgrades

In debian 12
sudo apt install python3-systemd -y # For backend = systemd

n8n-main@n8n-main:/etc/fail2ban$ sudo vim  /etc/fail2ban/jail.local
In the [sshd] section add backend = systemd and ensure enabled = true

Or just use
```
[DEFAULT]
bantime = 1h
findtime = 10m
maxretry = 5

[sshd]
enabled = true
port = ssh
backend = systemd
maxretry = 5
```
n8n-main@n8n-main:~$ history
   52  sudo systemctl start fail2ban
   53  sudo systemctl status fail2ban
   54  sudo fail2ban-client status
   55  sudo fail2ban-client status sshd
