# Hilfestellung
https://awesome-docker-compose.com/

# Typisches Beispiel: App + PostgreSQL
`
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=db
    depends_on:
      - db
  db:
    image: postgres:16
    volumes:
      - db_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=geheim
volumes:
  db_data:
  `

# Wichtige Befehle
## Alle Services starten (im Hintergrund)
`docker compose up -d`

## Alles stoppen
`docker compose down`

## Logs aller Services
`docker compose logs -f`

## Neu bauen
`docker compose up -d --build`

# Einzelnen Service neustarten
`docker compose restart app`
