# Introduction Azure Kubernetes Service
Introduction Azure Kubernetes Service


## Create Resource Group

- login at https://portal.azure.com
- create new Resource Group
- Location : Southeast Asia

## Create Service Principle

- login with cli

  ```bash
  az login
  ```

- switch subscription
  
  ```bash
  az account set --subscription xxx
  ```
  
- create SP with SDK Tool
  
  ```bash
  az ad sp create-for-rbac --name sp-xx-xx-xx --skip-assignment --sdk-auth
  ```

## Create Kubernetes Service

- go to Create in Resource group
- in the Create a resource page then select Kubernetes Service
  - Basics
    - Subscrption
    - Kubernetes cluster name : aks-lab-001
    - Region : Southeast Asia
    - Aviability zones :
  - Authentication
    - Authenication method : Service principal
    - Service principal client ID : xxx
    - Service principal client secret : xxx
- Review & Create

