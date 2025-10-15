# Deploy on Azure

## Prerequisites
- Azure CLI installed and configured
- Azure subscription with appropriate permissions
- Docker (for containerized deployment)

## Deployment Options

### Option 1: Azure Container Apps (Recommended)
```bash
# Create resource group
az group create --name ReconciliationEngineCollateralCorporateBanking-rg --location eastus

# Create container app environment
az containerapp env create \
  --name ReconciliationEngineCollateralCorporateBanking-env \
  --resource-group ReconciliationEngineCollateralCorporateBanking-rg \
  --location eastus

# Deploy container app
az containerapp create \
  --name ReconciliationEngineCollateralCorporateBanking \
  --resource-group ReconciliationEngineCollateralCorporateBanking-rg \
  --environment ReconciliationEngineCollateralCorporateBanking-env \
  --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest \
  --target-port 3000 \
  --ingress 'external' \
  --env-vars OPENAI_API_KEY=secretref:openai-key
```

### Option 2: Azure App Service
```bash
# Create App Service plan
az appservice plan create \
  --name ReconciliationEngineCollateralCorporateBanking-plan \
  --resource-group ReconciliationEngineCollateralCorporateBanking-rg \
  --sku B1 \
  --is-linux

# Create web app
az webapp create \
  --resource-group ReconciliationEngineCollateralCorporateBanking-rg \
  --plan ReconciliationEngineCollateralCorporateBanking-plan \
  --name ReconciliationEngineCollateralCorporateBanking \
  --runtime "NODE|18-lts"
```

## Environment Variables
Configure these in Azure:
- `OPENAI_API_KEY`: Your OpenAI API key
- `N8N_BASE_URL`: n8n instance URL
- `N8N_API_KEY`: n8n API key
- `NODE_ENV`: production

## Monitoring
- Enable Application Insights
- Configure health check endpoints
- Set up alerts for critical metrics
