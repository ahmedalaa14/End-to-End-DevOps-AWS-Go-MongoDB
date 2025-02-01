# End-to-end-DevOps | Go-MongoDB App

- This repository contains scripts and Kubernetes manifests for deploying the Go Survey application on an AWS EKS cluster with an accompanying ECR repository and EBS volumes. The deployment includes setting up an Ingress controller, monitoring with Prometheus and Grafana, and a continuous deployment pipeline.

## Prerequisites

- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) configured with appropriate permissions
- [Docker](https://docs.docker.com/engine/install/) installed and configured
- [kubectl](https://kubernetes.io/docs/tasks/tools/) installed and configured to interact with your Kubernetes cluster
- [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) installed
- [Helm](https://helm.sh/docs/intro/install/) installed
- [GitHub_CLI](https://github.com/cli/cli) installed
- [K9s](https://k9scli.io/topics/install/) installed
- [MongoDB_Compass](https://www.mongodb.com/try/download/atlascli)

# Steps 

1. **Creating Infrastructure**: Sets up the AWS EKS cluster, ECR repository, and EBS volumes using Terraform.

2. **Update Kubeconfig**: Configures `kubectl` to interact with the newly created EKS cluster.

3. **Build Docker Image**: Removes any existing Docker images and builds a new one with the Go Survey app.

4. **Push Docker Image**: Logs into ECR and pushes the new Docker image to the repository.

5. **Deploy to Kubernetes**: Creates the specified namespace if it doesn't exist and applies the Kubernetes manifests from the `k8s` directory.

6. **Wait for Deployment**: Waits for 60 seconds to allow the Kubernetes resources to be deployed.

7. **Ingress URL**: Retrieves the Ingress URL for accessing the deployed application.

8. **Application URLs**: Prints out the URLs for accessing the Go Survey app and the monitoring tools (Alertmanager, Prometheus, Grafana).

### Setting Up GitHub Secrets for AWS

Before using the GitHub Actions workflows, you need to set up the AWS credentials as secrets in your GitHub repository. The included `github_secrets.sh` script automates the process of adding your AWS credentials to GitHub Secrets, which are then used by the workflows. To use this script:

1. Ensure you have the GitHub CLI (`gh`) installed and authenticated.
2. Run the script with the following command:

   ```bash
   ./github_secrets.sh
   ```

This script will:

- Extract your AWS Access Key ID and Secret Access Key from your local AWS configuration.
- Use the GitHub CLI to set these as secrets in your GitHub repository.

**Note**: It's crucial to handle AWS credentials securely. The provided script is for demonstration purposes, and in a production environment, you should use a secure method to inject these credentials into your CI/CD pipeline.

## GitHub Actions Secrets

The following secrets need to be set in your GitHub repository for the workflows to function correctly:

- `AWS_ACCESS_KEY_ID`: Your AWS Access Key ID.
- `AWS_SECRET_ACCESS_KEY`: Your AWS Secret Access Key.
- `KUBECONFIG_SECRET`: Your Kubernetes config file encoded in base64.

These secrets are consumed by the GitHub Actions workflows to access your AWS resources and manage your Kubernetes cluster.

## Support

If you encounter any issues or require assistance, please file an issue in the repository.
