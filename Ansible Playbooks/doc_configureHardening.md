## Beschreibung

Das Playbook übernimmt die Ausführung des Hardening. Allerdings ohne log Server.

Es werden folgende Aufgaben ausgeführt:
1. git wird installiert
2. Repository mit hardening scripts wird geklont
3. file wird ausführbar gemacht
4. der command `sudo ./server-hardening.sh --log-user philipp --ssh 1461 --web yes --pw-auth no` wird ausgeführt.

Der `User` muss natürlich ersetzt werden. Ebenfalls wenn certs genutzt werden sollen muss das im Befehl mit angegeben werden. 

# WICHTIG:

Da jetzt ssh konfiguriert sein muss und lediglich ssh-key authentication erlaubt ist muss das ansible mitgeteilt werden. Dazu braucht es eine andere `inventory.ini`:

```
[your_server]
49.13.149.31 ansible_user=philipp ansible_ssh_private_key_file=/home/kronos/.ssh/testserver ansible_port=1461 ansible_become_pass="changeme443"

[all:vars]
ansible_become=true
ansible_become_method=sudo
```
> Das `User Passwort` muss natürlich ausgetauscht werden. Genauso auch der `Pfad` zum rsa key und der `user` name.

Die angaben unterhalb sind nötig damit ansible commands als sudo ausführen kann.


### Ausführung

Ein Befehl womit sich das Playbook ausführen lässt:
```bash
ansible-playbook configureHardening.yml -i inventorygit.ini
```