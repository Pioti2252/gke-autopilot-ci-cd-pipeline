# CI/CD dla aplikacji w GKE Autopilot (Cloud Build + Artifact Registry)

Projekt pokazuje kompletny, prosty pipeline CI/CD dla aplikacji kontenerowej uruchomionej w **Google Kubernetes Engine (Autopilot)**.

Pipeline:
- buduje obraz Dockera z repozytorium,
- publikuje obraz do **Artifact Registry**,
- wdraża nową wersję do **GKE Autopilot** automatycznie po `git push` (Cloud Build Trigger).

---

## Architektura

**GitHub (repo) → Cloud Build Trigger → Build & Push → Artifact Registry → Deploy → GKE Autopilot → Service (LoadBalancer)**

- Repo: kod aplikacji + `Dockerfile` + `cloudbuild.yaml` + manifesty Kubernetes (`k8s/`)
- Artifact Registry: przechowuje wersje obrazów
- Cloud Build: buduje i deployuje
- GKE Autopilot: uruchamia aplikację
- Service typu `LoadBalancer`: wystawia aplikację na zewnątrz

---

## Wymagania

- Projekt w Google Cloud z włączonym billingiem
- Klaster **GKE Autopilot**
- Repozytorium na GitHubie połączone z Cloud Build (Triggers)

Włączone API:
- Cloud Build API
- Artifact Registry API
- Kubernetes Engine API

---

## Konfiguracja (podmień wartości)

Używane nazwy (przykładowe):
- `PROJECT_ID`: `pipeline-ci-cd-gke`
- `REGION`: `europe-central2`
- `CLUSTER_NAME`: `YOUR_CLUSTER_NAME`
- `AR_REPO`: `app-repo`
- `IMAGE_NAME`: `myapp`
- `NAMESPACE`: `default`
- `SERVICE_NAME`: `myapp`
- `DEPLOYMENT_NAME`: `myapp`

---

## Struktura repozytorium

```text
.
├── Dockerfile
├── cloudbuild.yaml
└── k8s/
    ├── deployment.yaml
    └── service.yaml
