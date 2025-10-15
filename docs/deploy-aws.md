# Deploy on AWS

## Prerequisites
- AWS CLI configured
- Docker installed
- AWS account with appropriate IAM permissions

## Deployment Options

### Option 1: AWS Fargate (Recommended)
```bash
# Create ECS cluster
aws ecs create-cluster --cluster-name ReconciliationEngineCollateralCorporateBanking-cluster

# Create task definition
aws ecs register-task-definition --cli-input-json file://task-definition.json

# Create service
aws ecs create-service \
  --cluster ReconciliationEngineCollateralCorporateBanking-cluster \
  --service-name ReconciliationEngineCollateralCorporateBanking-service \
  --task-definition ReconciliationEngineCollateralCorporateBanking:1 \
  --desired-count 1 \
  --launch-type FARGATE
```

### Option 2: AWS Lambda
```bash
# Package and deploy
zip -r function.zip .
aws lambda create-function \
  --function-name ReconciliationEngineCollateralCorporateBanking \
  --runtime nodejs18.x \
  --role arn:aws:iam::ACCOUNT:role/lambda-execution-role \
  --handler index.handler \
  --zip-file fileb://function.zip
```

## Environment Variables
- `OPENAI_API_KEY`: Your OpenAI API key
- `N8N_BASE_URL`: n8n instance URL
- `N8N_API_KEY`: n8n API key

## Monitoring
- CloudWatch logs and metrics
- X-Ray tracing
- Health check endpoints
