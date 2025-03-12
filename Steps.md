# Raspberry Pi 5 - K3s Kubernetes Cluster Setup

## Overview
This guide outlines the process of setting up a **K3s Kubernetes cluster** on a **Raspberry Pi 5** using **Ubuntu 24.10 (ARM64)**. It covers the steps for installation, MongoDB deployment, and application deployment, leveraging the built-in **Traefik ingress controller** provided by K3s.

## Prerequisites
- **Raspberry Pi 5**
- **128GB MicroSD Card** (for storage and OS installation)
- **Ubuntu 24.10 (ARM64) ISO**
- **Raspberry Pi Imager Tool**
- **Stable Internet Connection**
- **Monitor & Keyboard (for initial setup)**

## Step 1: Boot Raspberry Pi 5 with Ubuntu 24.10 (ARM64)
1. **Download Ubuntu 24.10 (ARM64)** from the official Raspberry Pi website.
2. Use **Raspberry Pi Imager** to create a bootable **128GB MicroSD card**.
3. Configure WiFi settings within the Imager tool by entering the **WiFi SSID** and **password**.
4. Complete the imaging process and safely eject the MicroSD card.
5. Insert the bootable MicroSD card into **Raspberry Pi 5** and power it on.
6. The remaining storage on the **128GB MicroSD card** can be used for other purposes after installation.

## Step 2: Initial System Setup
1. Connect a **monitor and keyboard** to Raspberry Pi 5.
2. Open a terminal and update the system:
   ```sh
   sudo apt-get update && sudo apt-get upgrade -y
   ```

## Step 3: Install K3s Kubernetes Cluster (Single Node)
1. Run the following command to install K3s:
   ```sh
   curl -sfL https://get.k3s.io | sh -
   ```
2. Verify the installation:
   ```sh
   sudo kubectl get nodes
   ```
3. For additional configurations, refer to the [K3s Setup Guide](https://github.com/sprathmesh/k3ssetup-pratham.git).

## Step 4: Deploy MongoDB (Standalone)
1. Deploy a **MongoDB standalone pod**:
   ```sh
   kubectl apply -f mongo-deployment.yaml
   ```
2. Check the status of the pod:
   ```sh
   kubectl get pods
   ```
3. Refer to the [MongoDB Setup Guide](https://github.com/sprathmesh/pratham-rassberrypi5-mongo-setup.git) for detailed steps.

## Step 5: Deploy the Application
1. Deploy your application services.
2. Verify running pods using:
   ```sh
   kubectl get po
   ```
   **Expected Output:**
   ```
   NAME                         READY   STATUS    RESTARTS       AGE
   dal-84ddb696dc-pnx9x         1/1     Running   13 (18h ago)   5d22h
   event-app-64c6b87bfc-j5m26   1/1     Running   13 (18h ago)   5d23h
   frontend-7d647d9776-v5449    1/1     Running   23 (18h ago)   5d22h
   mongo-6b476d694-xxchc        1/1     Running   13 (18h ago)   6d16h
   raven-poi-5fc66b47bc-99ckz   1/1     Running   13 (18h ago)   4d22h
   ```

## Step 6: Default Ingress Controller in K3s
- K3s provides a built-in **Traefik** ingress controller instead of **Nginx Ingress**.
- The ingress controller runs under the **kube-system** namespace.
- To check the **Traefik service**, run:
   ```sh
   kubectl get svc -n kube-system
   ```

## Conclusion
This guide provides a step-by-step process for setting up a **K3s Kubernetes cluster** on a **Raspberry Pi 5**, deploying **MongoDB**, and deploying an application. The **built-in Traefik ingress controller** simplifies ingress management, making it a lightweight and efficient Kubernetes solution for ARM64 devices.

