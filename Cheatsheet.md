# Dockerfile-Befehle
FROM     → Basis-Image
WORKDIR  → Arbeitsverzeichnis
COPY     → Datei(en) kopieren
RUN      → Befehl beim Build
ENV      → Umgebungsvariable
EXPOSE   → Port dokumentieren
CMD      → Startbefehl (überschreibbar)
ENTRYPOINT → Fixer Startbefehl

# Docker-Befehle
docker build -t name:tag .
docker run -p host:container name
docker ps / docker ps -a
docker logs <id>
docker stop <id>

# Compose-Befehle
docker compose up -d
docker compose down
docker compose logs -f
docker compose ps
docker compose exec app sh

# Secrets-Reihenfolge
1. Passwort in .env auslagern
2. .env in .gitignore eintragen
3. In compose.yml per ${VARIABLE} referenzieren
4. Für Produktion: Docker Secrets mit _FILE-Pattern
