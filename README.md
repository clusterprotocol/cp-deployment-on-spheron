# cp-deployment-on-spheron
Decentralized Cluster Protocol deployment using Spheron Protocol. Complete guide and configuration for deploying blockchain-based applications.


# CP Deployment on Spheron

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Wallet Setup](#wallet-setup)
- [Deployment](#deployment)
- [Accessing the Deployment](#accessing-the-deployment)
- [Fetching Deployment Logs](#fetching-deployment-logs)
- [Contact Information](#contact-information)

---

## Overview
**CP Deployment on Spheron** is a decentralized, blockchain-based solution deployed on the **Spheron Protocol**. This guide helps you set up and deploy the Cluster Protocol app, including environment configuration, wallet creation, and deployment execution.

---

## Prerequisites
Before starting, ensure the following are installed:
- Linux or macOS
- **curl** for CLI installation
- Docker (for containerized services)
- Access to **Spheron Protocol CLI**
- Wallet with USDT or other supported tokens for escrow

---

## Installation
1. **Install the Spheron CLI**:
   Run this command to install:
   
   curl -sL1 https://sphnctl.sh | bash

     sphnctl -h

2. Verify the installation: After installation, check if it’s installed correctly:

**Configuration**

                  version: "1.0"
              services:
                cluster-protocol:
                  image: public.ecr.aws/b0i8r5m0/clusterprotocol/provider-setup:latest
                  expose:
                    - port: 8080
                      as: 8080
                      to:
                        - global: true
                  env:
                    - ENV_VAR=value
              
              profiles:
                name: cluster-profile
                duration: 1h
                tier:
                  - community
                compute:
                  cluster-protocol:
                    resources:
                      cpu:
                        units: 2
                      memory:
                        size: 8Gi
                      storage:
                        size: 25Gi
                placement:
                  westcoast:
                    attributes:
                      region: finland
                    pricing:
                      cluster-protocol:
                        denom: USDT
                        amount: 5000000
              
              deployment:
                cluster-protocol:
                  westcoast:
                    profile: cluster-protocol


    **Wallet Setup : **

    **Create a new wallet:**

        sphnctl wallet create --name [wallet_name]

        Ensure you save the wallet mnemonic and secret for future use.

    2. Get USDT test tokens from the Spheron Faucet and verify the balance:

          sphnctl wallet balance --token USDT


 ** Deployment : **

    **Deposit tokens into escrow:**

      sphnctl payment deposit --amount 10000000 --token USDT

    **Deploy your app:**

        sphnctl deployment create gpu.yml

**Accessing the Deployment**

    **Get the deployment details:**

      sphnctl deployment get --lid [lease_id]

      
**Fetching Deployment Logs**

    Retrieve logs using the Lease ID:

        sphnctl deployment logs --lid [lease_id]

        
  **Contact Information**
