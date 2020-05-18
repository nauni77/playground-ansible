# prepare using ansible

1. install ansible via brew, yum, ...
2. copy public ssh keys to all target systems
   `ssh-copy-id -i ~/.ssh/id_rsa.pub <client-host>`
3. user should switch to root without password
   1. `visudo`
   2. at end of file add (tab between rows)
      `<benutzer>     ALL=(ALL)     NOPASSWD: ALL`
      Nun kann `sudo` eingesetzt werden ohne das Passwort eingeben zu müssen.

# Module

## command

* verwendet nicht die Shell (BASH/SH)
* pipe und redirect werden somit nicht unterstützt

## shell

* pipe und redirect werden unterstützt
* **Achtung:** falsche Befehle können sich auf das gesamte System auswirken

## raw

* sendet Befehle über ssh
* python wird nicht benötigt
* eingeschränkte funktion

# Inventory

By default the inventory is located at `/etc/ansible/hosts` (different location can be specified at command line with `-i <path>`. The file looks like (INI-like format):

```ini
mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```

YAML format:

```yaml
all:
  hosts:
    mail.example.com:
  children:
    webservers:
      hosts:
        foo.example.com:
        bar.example.com:
    dbservers:
      hosts:
        one.example.com:
        two.example.com:
        three.example.com:
```

Working with static IPs you can describe hosts via variables:

```ini
jumper ansible_port=5555 ansible_host=192.0.2.50
```

YAML format:

```yaml
...
  hosts:
    jumper:
      ansible_port: 5555
      ansible_host: 192.0.2.50
```

Host variables - can be used later inside playbooks:

```ini
[atlanta]
host1 http_port=80 maxRequestsPerChild=808
host2 http_port=303 maxRequestsPerChild=909
```

Group variables:

```ini
[atlanta]
host1
host2

[atlanta:vars]
ntp_server=ntp.atlanta.example.com
proxy=proxy.atlanta.example.com
```

YAML format:

```yaml
atlanta:
  hosts:
    host1:
    host2:
  vars:
    ntp_server: ntp.atlanta.example.com
    proxy: proxy.atlanta.example.com

```

