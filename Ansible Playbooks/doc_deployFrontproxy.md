## Beschreibung

Das Playbook übernimmt das vollständige deployen einens frontproxys via docker. Alle Files und Directorys werden richtig erstellt.

Es werden folgende Aufgaben ausgeführt:
1. Directorys werden erstellt.
2. files werden gefüllt
    - in .env werden auf dem Server generierte Passwörter geladen (sicher)
3. file wird ausführbar gemacht
4. der command `docker compose up -d` wird ausgeführt.
 

# WICHTIG:

Es wird vorausgesetzt, dass docker korrekt installiert ist und der Ansible User der docker Gruppe hinzugefügt wurde.

**inventorydocker.ini**

```ini
[your_server]
49.13.149.31 ansible_user=philipp ansible_ssh_private_key_file=/home/kronos/.ssh/testserver ansible_port=1461 ansible_become_pass="changeme443"

[all:vars]
ansible_become=true
ansible_become_method=sudo
```
> Das `User Passwort` muss natürlich ausgetauscht werden. Genauso auch der `Pfad` zum rsa key und der `user` name.

Die angaben unterhalb sind nötig damit ansible commands als sudo ausführen kann.

> Das Script braucht jenachdem ob das Server Hardening durchgeführt wurde ca 3-4 Minuten bis es durchgelaufen ist. Für einen genaueren Debug Prozess kann am Ende des Commands die `-vv` Flag gesetzt werden.
### Ausführung

Ein Befehl womit sich das Playbook ausführen lässt:
```bash
ansible-playbook configureHardening.yml -i inventorydocker.ini
```