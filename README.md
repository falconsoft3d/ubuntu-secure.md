
## 1- Actualizar el sistema
```
sudo apt update
sudo apt upgrade
```

## 2- Instalar fail2ban
Fail2ban es una herramienta de seguridad que protege tu servidor bloqueando temporalmente IP que realizan demasiados intentos fallidos de acceso

```
sudo apt update
sudo apt install fail2ban -y
sudo systemctl enable --now fail2ban
sudo systemctl status fail2ban --no-pager
sudo fail2ban-client status
sudo fail2ban-client status sshd
sudo nano /etc/fail2ban/jail.d/sshd.local

[sshd]
enabled = true
maxretry = 5
findtime = 10m
bantime = 24h

sudo fail2ban-client -t
sudo systemctl restart fail2ban
sudo fail2ban-client status sshd
sudo fail2ban-client -t
```

## 3- Proteger por ssh
```
ls -la ~/.ssh
ssh-keygen -lf ~/.ssh/id_ed25519.pub
ssh-copy-id -i ~/.ssh/id_ed25519.pub root@157.xxx.xxx.xxx
ssh root@157.xxx.xxx.xxx
sudo nano /etc/ssh/sshd_config

PubkeyAuthentication yes
PasswordAuthentication no
KbdInteractiveAuthentication no
PermitRootLogin prohibit-password

sudo sshd -t
sudo systemctl reload ssh
sudo sshd -T | grep -E 'passwordauthentication|kbdinteractiveauthentication|pubkeyauthentication|permitrootlogin'
```




