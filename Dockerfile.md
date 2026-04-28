# Wichtige Befehle
## Basis-Image wählen
`FROM node:20-alpine`

## Arbeitsverzeichnis im Container
`WORKDIR /app`

## Dateien kopieren (Host → Container)
`COPY package*.json ./`
`COPY . .`

## Befehl ausführen (beim Build)
`RUN npm install`

## Umgebungsvariable setzen
`ENV NODE_ENV=production`

## Port dokumentieren (nur Doku, kein echtes Öffnen)
`EXPOSE 3000`

## Startbefehl des Containers
`CMD ["node", "server.js"]`

## RUN vs CMD vs ENTRYPOINT
RUN – wird beim Build ausgeführt (z.B. Pakete installieren)

CMD – Standardbefehl beim Start; überschreibbar per CLI

ENTRYPOINT – Fixer Startbefehl; CMD wird als Argument angehängt
