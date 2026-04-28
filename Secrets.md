# Was man NICHT tun soll
## SCHLECHT: Passwort direkt in compose.yml
environment:
  - POSTGRES_PASSWORD=meinGeheimesPasswort
Problem: Datei landet in Git → Passwort für alle sichtbar.

Lösung 1: .env-Datei Empfohlen
# .env (diese Datei in .gitignore eintragen!)
POSTGRES_PASSWORD=meinGeheimesPasswort
DB_USER=admin
# compose.yml – Variablen referenzieren
environment:
  - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
  - POSTGRES_USER=${DB_USER}
Lösung 2: Docker Secrets (für Produktion)
# compose.yml
services:
  db:
    image: postgres:16
    secrets:
      - db_password
    environment:
      - POSTGRES_PASSWORD_FILE=/run/secrets/db_password

secrets:
  db_password:
    file: ./secrets/db_password.txt
Secret wird als Datei in /run/secrets/ gemountet – nie als Umgebungsvariable im Prozess sichtbar.

.gitignore nicht vergessen
# .gitignore
.env
secrets/
