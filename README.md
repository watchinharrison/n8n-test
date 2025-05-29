# n8n GCP Deployment Guide

## Purpose

This repository provides a complete solution for deploying n8n workflow automation platform to Google Cloud Platform (GCP). It includes infrastructure as code, configuration templates, and comprehensive documentation to enable quick and reliable cloud deployments.

## Architecture Overview

The deployment leverages several GCP services to create a scalable, secure, and maintainable n8n instance:

- Cloud Run for containerized n8n application
- Cloud SQL (PostgreSQL) for persistent workflow data storage
- Secret Manager for secure credentials management
- Cloud Storage for file storage
- Cloud IAM for access management
- Cloud Monitoring and Logging for observability

```
┌─────────────────┐     ┌───────────────┐     ┌──────────────┐
│   Cloud Run     │     │   Cloud SQL   │     │Cloud Storage │
│  (n8n service)  │◄───►│  (PostgreSQL) │     │ (File store) │
└────────┬────────┘     └───────────────┘     └──────────────┘
         │                                            ▲
         ▼                                            │
┌─────────────────┐                           ┌──────┴───────┐
│ Secret Manager  │                           │  n8n Service │
│  (Credentials)  │◄─────────────────────────►│   (Runtime)  │
└─────────────────┘                           └──────────────┘
```

## GCP Services Used

### Cloud Run
Hosts the containerized n8n application, providing automatic scaling and pay-per-use billing.

### Cloud SQL (PostgreSQL)
Provides a managed PostgreSQL database for workflow data persistence.

### Secret Manager
Securely stores sensitive configuration like database credentials and API keys.

### Cloud Storage
Used for file storage and backups.

### Cloud IAM
Manages access control and service account permissions.

### Cloud Monitoring and Logging
Provides visibility into application performance and troubleshooting capabilities.

## Deployment Instructions

### Prerequisites
- GCP account with billing enabled
- gcloud CLI installed and configured
- Docker installed (for local testing)
- Terraform (optional, for infrastructure as code)

### Quick Start
1. Clone this repository
2. Configure environment variables in `.env.example` and rename to `.env`
3. Run the deployment script: `./deploy.sh`

### Manual Deployment Steps
Detailed step-by-step instructions are available in [deployment guide](docs/deployment.md).

## Configuration Guide

### Environment Variables
The following environment variables must be configured:

- `DB_TYPE`: Set to "postgresdb"
- `DB_POSTGRESDB_HOST`: Cloud SQL host address
- `DB_POSTGRESDB_DATABASE`: Database name
- `DB_POSTGRESDB_USER`: Database username
- `DB_POSTGRESDB_PASSWORD`: Database password
- `N8N_ENCRYPTION_KEY`: Encryption key for sensitive data
- `N8N_HOST`: Public URL for n8n

Full list of environment variables is available in [environment variables reference](docs/environment-variables.md).

## Maintenance Procedures

### Backup and Restore
Regular database backups are configured with Cloud SQL automated backups. Manual backup procedures are documented in [maintenance guide](docs/maintenance.md).

### Updates
Steps to update n8n to newer versions while maintaining data integrity are provided in [update procedure](docs/updates.md).

### Monitoring
Monitoring dashboards are automatically created for:
- Service performance
- Database metrics
- Cost tracking

## Troubleshooting

Common issues and their solutions are documented in [troubleshooting guide](docs/troubleshooting.md).

### Common Issues
- Connection problems between n8n and database
- Authentication failures
- Workflow execution errors
- Resource limitations

## Security Considerations

This deployment follows security best practices:
- Private networking for database connections
- Secret Manager for credentials
- Minimal IAM permissions
- Regular security updates
- HTTPS enforcement

Detailed security information is available in [security guide](docs/security.md).

## Cost Estimation

Approximate monthly costs for different scales of deployment:

| Deployment Size | Estimated Cost (USD/month) | Workflows | Users |
|----------------|----------------------------|-----------|-------|
| Small          | $50-100                    | <100      | 1-5   |
| Medium         | $100-250                   | 100-1000  | 5-20  |
| Large          | $250-600+                  | 1000+     | 20+   |

Detailed cost breakdown available in [cost estimation](docs/costs.md).

## Contributing

Contributions to improve the deployment are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.