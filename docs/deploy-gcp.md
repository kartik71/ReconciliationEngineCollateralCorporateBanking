# Deploy on Google Cloud Platform

## Prerequisites
- Google Cloud SDK installed
- Docker installed
- GCP project with billing enabled

## Deployment Options

### Option 1: Cloud Run (Recommended)
```bash
# Build and push container
gcloud builds submit --tag gcr.io/PROJECT_ID/ReconciliationEngineCollateralCorporateBanking

# Deploy to Cloud Run
gcloud run deploy ReconciliationEngineCollateralCorporateBanking \
  --image gcr.io/PROJECT_ID/ReconciliationEngineCollateralCorporateBanking \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated
```

### Option 2: Google Kubernetes Engine
```bash
# Create GKE cluster
gcloud container clusters create ReconciliationEngineCollateralCorporateBanking-cluster \
  --num-nodes=3 \
  --zone=us-central1-a

# Deploy application
kubectl apply -f k8s/
```

## Environment Variables
- `OPENAI_API_KEY`: Your OpenAI API key
- `N8N_BASE_URL`: n8n instance URL
- `N8N_API_KEY`: n8n API key

## Monitoring
- Cloud Monitoring
- Cloud Logging
- Error Reporting
