---
layout: post
title:  "Install samba server on ubuntu [pt-Br]"
date:   2019-07-20 19:10:44 -0300
categories: linux ubuntu services samba
---

## Instalação

### 1. Instalar pacote samba
```sh
sudo apt update
sudo apt install samba
```

### 2. Verificar status do serviço
```sh
sudo systemctl status nmbd
```

output
```sh
● nmbd.service - Samba NMB Daemon
Loaded: loaded (/lib/systemd/system/nmbd.service; enabled; vendor preset: enabled)
Active: active (running) since Sun 2019-01-27 02:36:20 PST; 4s ago
    Docs: man:nmbd(8)
        man:samba(7)
        man:smb.conf(5)
Main PID: 4262 (nmbd)
Status: "nmbd: ready to serve connections..."
    Tasks: 1 (limit: 2319)
CGroup: /system.slice/nmbd.service
        `-4262 /usr/sbin/nmbd --foreground --no-process-group
```

### 3. Permitir acesso a portas no firewall local
```sh
sudo ufw allow 'Samba'
```

### 4. Criar usuário e diretório para o serviço.
* 4.1 Criar diretório
```sh
sudo mkdir <PATH>
```
* 4.2 Configurar permissões para o diretório
```sh
sudo chgrp sambashare <PATH>
```

### 5. Criar usuário para o serviço
```sh
sudo useradd -M -d <PATH>/<USER> -s /usr/sbin/nologin -G sambashare <USER>
```

### 6. Fazer bind do diretório com o usuário criado
```sh
sudo mkdir <PATH>/<USER>
sudo chown <USER>:sambashare <PATH>/<USER>
sudo chmod 2770 <PATH>/<USER>
```

### 7. Criar senha e ativar usuário
```sh
sudo smbpasswd -a <USER>
sudo smbpasswd -e <USER>
```

### 8. Configurar compartilhadores samba em `/etc/samba/smb.conf`
> adicionar ao fim do arquivo

```sh
[<USER>]
    path = <PATH>/<USER>
    browseable = yes
    read only = no
    force create mode = 0660
    force directory mode = 2770
    valid users = <USER> @sadmin <USER_NAME>
```

### Final. Reiniciar serviço:
```sh
sudo systemctl restart nmbd
```