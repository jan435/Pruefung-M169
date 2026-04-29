# Ablauf bei praktischen Prüfungsfragen zu Docker/Docker Compose
## 1. Dockerfile-Aufgabe
Typische Frage: „Erstelle ein Dockerfile für eine Node.js-App"
1. Basis-Image wählen          FROM node:18-alpine
2. Arbeitsverzeichnis setzen   WORKDIR /app
3. Abhängigkeiten kopieren     COPY package*.json ./
4. Abhängigkeiten installieren RUN npm install
5. Quellcode kopieren          COPY . .
6. Port freigeben              EXPOSE 3000
7. Startbefehl definieren      CMD ["node", "index.js"]

### Testen:
bashdocker build -t meine-app .
docker run -p 3000:3000 meine-app

## 2. Docker Compose – YAML-Datei erstellen
Typische Frage: „Erstelle eine compose.yml für App + Datenbank"
```
yamlservices:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=db
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      - POSTGRES_PASSWORD=${DB_PASSWORD}   # ← Geheimnis via .env
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

## 3. Umgang mit Passwörtern / Secrets
### Vorgehen:
```
Option A – .env-Datei (einfach, lokal)
├── .env Datei erstellen:        DB_PASSWORD=geheim123
├── In compose.yml referenzieren: ${DB_PASSWORD}
└── .env in .gitignore eintragen  ← wichtig!

Option B – Docker Secrets (produktiv)
├── Secret erstellen: docker secret create db_pass ./passwort.txt
└── In compose.yml:   secrets: [db_pass]
```
## 4. Anwenden & Testen
```
# Starten
docker compose up -d

# Status prüfen
docker compose ps

# Logs anschauen
docker compose logs app

# Stoppen
docker compose down
```
