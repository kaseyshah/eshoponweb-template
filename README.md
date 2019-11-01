# eshoponweb-template

Docker Application Template for deploying [eShopOnWeb](TODO) onto Azure Kubernetes Service.

## Pre-requisites

1. You need [Docker Desktop Enterprise](https://hub.docker.com/editions/community/docker-desktop-ent) which has the [Application Templates](https://blog.docker.com/2019/07/application-templates-docker-desktop-enterprise/) feature.

> The demo is a Linux app, so on Windows you need to use Linux container mode

2. You need a Docker Hub account, so the pipeline can push images.

> If you've set your account to create private repos on push, make sure you have capacity for another repo.

3. Create a Service Principal in Azure. You can use the [Azure CLI](https://github.com/Azure/azure-cli):

```
az ad sp create-for-rbac --name http://app-template
```

4. Your GitHub account needs to be approved for [GitHub Actions](https://help.github.com/en/articles/about-github-actions) (currently in beta). Then create an empty repo and set the following secrets (under _Settings...Secrets_):

- `AZURE_SP_APP_ID` - Service Principal application ID
- `AZURE_SP_NAME` - Service Principal name
- `AZURE_SP_PASSWORD` - Service Principal password
- `AZURE_SP_TENANT` - Service Principal tenant
- `AZURE_SQL_SERVER_NAME` - Name of the SQL Server instance
- `AZURE_SQL_PASSWORD` - Password for SQL Server
- `DOCKER_HUB_USERNAME` - Docker Hub username
- `DOCKER_HUB_ACCESS_TOKEN` - Docker Hub [Personal Access Token](https://www.docker.com/blog/docker-hub-new-personal-access-tokens/)

## Setup

Update your App Template config in `~/.docker/application-template/preferences.yaml` to include the template library at `https://raw.githubusercontent.com/sixeyed/eshoponweb-template/master/eshoponweb-library.yaml`.

This example includes the local demo libraries and the main Docker library:

```
apiVersion: v1alpha1
disableFeedback: false
kind: Preferences
repositories:
- name: eshoponweb-library
  url: https://raw.githubusercontent.com/sixeyed/eshoponweb-template/master/eshoponweb-library.yaml
- name: library
  url: https://docker-application-template.s3.amazonaws.com/production/v0.1.5/library.yaml
```
