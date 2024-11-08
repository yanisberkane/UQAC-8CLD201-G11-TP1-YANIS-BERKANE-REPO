# Travail Pratique #1: UQAC-8CLD201-G11-TP1-YANIS-BERKANE-REPO

## Auteurs

- BERY02010200, Berkane, Yanis
- OUIR24090302, Ouiz, Rachid
- TOUM26119900, Touta, Mohamed
- ZAAM13110000, Zaaboub, Mehdi

## Description

Ce dépôt contient le travail pratique #1 du cours 8CLD201 de l'UQAC. Il s'agit d'un projet de groupe réalisé par les auteurs mentionnés ci-dessus.

## Structure du projet

Le projet est structuré de la manière suivante:

```
.
├── AzureResourceGroup1 (VMSS)
│   ├── azuredeploy.json
│   └── azuredeploy.parameters.json
├── AzureResourceGroup2 (Key Vault)
│   ├── azuredeploy.json
│   └── azuredeploy.parameters.json
├── README.md
├── azure-pipelines-1.yml
├── azure-pipelines.yml
├── customData.txt
└── webdoe (Web app source code)
```

``AzureResourceGroup1`` contient les fichiers nécessaires pour déployer une instance de VMSS (Virtual Machine Scale Set) sur Azure. ``AzureResourceGroup2`` contient les fichiers nécessaires pour déployer un Key Vault sur Azure. ``webdoe`` contient le code source de l'application web à déployer.
``customData.txt`` contient le script de personnalisation de la VMSS. Ce fichier pernet de configurer le serveur nginx pour servir l'application web.

## Azure Resource Group 1 (VMSS)

### Parameters

The parameters allow customization for various settings like location, OS disk type, virtual network, security settings, VM name, scale set settings, and load balancer configuration.

### Variables

Variables such as storageApiVersion and networkApiVersion are used to maintain API consistency across different Azure resources. The namingInfix helps in uniquely naming resources to avoid conflicts.

### Resources

* Virtual Network: Sets up the VNet with specified address spaces and subnets.
* Network Security Groups: Configures multiple NSGs as specified in the parameters, with a copy loop to allow multiple security groups to be created as needed.
* Public IP for Load Balancer: Creates a static IP address for the Load Balancer.
* Load Balancer: Configures a Load Balancer with frontend IP configuration, backend pools, load balancing rules, and inbound NAT rules.
* Autoscale Settings: Establishes autoscaling rules based on CPU percentage, allowing scale-in and scale-out based on utilization thresholds.
* VM Scale Set: The core of this template, defining the VM scale set, network interface configurations, health extension, and OS profile, with options for secure boot and vTPM for enhanced security.

## Azure Resource Group 2 (Key Vault)

### Parameters

The parameters section allows customization for Key Vault settings:

* Name and Location: Defines the Key Vault's name and Azure region.
* SKU: Specifies the pricing tier (e.g., Standard or Premium).
* Access Policies: Configures access policies to control permissions for different users or applications.
* Tenant ID: Specifies the tenant ID for authentication.
* Security and Deployment Settings: Optional settings to enable deployment, template deployment, disk encryption, and Role-Based Access Control (RBAC).
* Public Network Access and Retention: Configures public access, enables soft delete, sets the retention duration for deleted data, and applies network ACLs.

### Variables

This template does not define any variables, focusing on direct parameterization.

### Resources

* Microsoft.KeyVault/vaults: Creates an Azure Key Vault with properties configured based on the parameters. Key properties include:
* Deployment Options: Allows enabling or disabling template deployment and disk encryption.
* RBAC and Access Policies: Enables RBAC if specified and applies custom access policies.
* Soft Delete and Retention: Enables soft delete and retention settings for data protection.
* Network ACLs: Configures network access control lists (ACLs) for security.

## Déploiement

Le déploiement de ce projet se fait en utilisant Azure DevOps. Pour ce faire, il suffit de créer un pipeline Azure DevOps et de lui associer les fichiers `azure-pipelines.yml` et `azure-pipelines-1.yml` situés à la racine du projet. Ces fichiers contiennent les étapes nécessaires pour déployer les ressources Azure.
