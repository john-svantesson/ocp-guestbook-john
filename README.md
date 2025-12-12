# OpenShift Guestbook – Full CI/CD med GitHub Actions

Detta repo är en fortsättning på tidigare labb där jag driftsatte en gästbok med:
- Go-backend
- Nginx-frontend
- PostgreSQL
- Redis
- Route med TLS Edge-termination

Målet med denna uppgift var att helt automatisera bygg och driftsättning med GitHub Actions – inga manuella `oc`-kommandon efter första setup.

## Vad som gjordes

- Anpassade alla YAML-filer så de fungerar på skolans OpenShift-kluster (istället för CRC)

- Skapade en GitHub Actions-workflow som vid varje push till `master`:
  - Bygger frontend- och backend-imagen med Docker
  - Taggar och pushar till GHCR
  - Loggar in på skolklustret
  - Kör `oc apply -f` på mapparna 1-postgres → 5-route

- Tog bort alla `secret.yaml`-filer från repot
  - Skapade ett enda secret lokalt: `guestbook-common-secrets` (hanteras manuellt)
  - Uppdaterade referenser i PostgreSQL StatefulSet, Redis Deployment och Backend Deployment

- Gjorde repot publikt utan att exponera några lösenord

## Resultat

Vid varje push till `master` byggs, pushas och deployas hela applikationen automatiskt inom 3–5 minuter.

Gästboken är live och nås här:  
https://guestbook-frontend-ocp-guestbook-john.apps.devops24.cloud2.se
