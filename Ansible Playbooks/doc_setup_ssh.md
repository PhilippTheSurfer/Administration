## Beschreibung

Das Playbook übernimmt die basis config für ssh Zugang per RSA key. 

# WICHTIG:

Wenn es sich um ein System von Hetzner handelt wird der User automatisch beim ersten login aufgefordert das Root passwort zu ändern. Dieser vorgang lässt sich in Ansible nicht abbilden, daher muss das erste login manuell erfolgen und das root passwort per hand geändert werden. Danach kann sich ausgeloggt werden.

> Passwörter in der `ini` File müssen immer in `"passwort"` stehen. Ansible hat schwierigkeiten mit Sonderzeichen.

## Erklärung

Das Script benötigt eine `inventory.ini` Datei. Diese Datei muss wie folgt aussehen:
```ini
[your_server]
49.13.149.31 ansible_user=root ansible_ssh_pass=%f%D^Wu9f^@fj9V7oyJg
```
Es ist wichtig genau das zu übernehmen und das root passwort gegen das manuell gesetzte auszutauschen. (auch die IPv4). `[your_server]` wurde so im Playbook definiert.

Ein Befehl womit sich das Playbook ausführen lässt:
```bash
ansible-playbook setup_ssh.yml -i inventory.ini
```