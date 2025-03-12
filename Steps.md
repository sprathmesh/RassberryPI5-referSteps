# Raspberry Pi 5 - K3s Kubernetes Cluster Setup

## 1. Booting Raspberry Pi 5 with Ubuntu 24.10 (ARM64)
1. Download the official Ubuntu 24.10 (ARM64) image from the official Raspberry Pi website.
2. Use the **Raspberry Pi Imager** tool to create a bootable USB drive.
3. During the imaging process, configure WiFi connectivity by entering the WiFi SSID and password.
4. Once the bootable USB drive is ready, safely eject it and insert it into the Raspberry Pi 5.

## 2. Initial Setup on Raspberry Pi 5
1. Boot up the Raspberry Pi 5 with the prepared USB drive.
2. Attach a monitor and open the terminal.
3. Update system packages:
   ```sh
   sudo apt-get update && sudo apt-get upgrade -y
   ```

## 3. Installing K3s Kubernetes Cluster (Single Node)
1. Install K3s using the following steps:
   ```sh
   curl -sfL https://get.k3s.io | sh -
   ```
2. Validate the installation:
   ```sh
   sudo kubectl get nodes
   ```
3. Refer to the official documentation for further setup details:  
   [K3s Setup Guide](https://github.com/sprathmesh/k3ssetup-pratham.git)

## 4. Deploying MongoDB (Standalone)
1. Deploy a standalone MongoDB pod:
   ```sh
   kubectl apply -f mongo-deployment.yaml
   ```
2. Verify that the MongoDB pod is running:
   ```sh
   kubectl get pods
   ```
3. Refer to the MongoDB setup guide for Raspberry Pi 5:  
   [MongoDB Setup Guide](https://github.com/sprathmesh/pratham-rassberrypi5-mongo-setup.git)

## 5. Deploying the Application
1. Deploy the application services.
2. Verify the running pods:
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

## 6. Default Ingress Controller in K3s
- Instead of using **Nginx Ingress**, K3s provides a built-in service called **Traefik**.
- The default ingress controller runs under the **kube-system** namespace.
- To check the Traefik service:
   ```sh
   kubectl get svc -n kube-system
   ```

## Conclusion
This guide provides a step-by-step approach to setting up a **K3s Kubernetes cluster on a Raspberry Pi 5**, deploying **MongoDB**, and deploying applications. K3s comes with a built-in **Traefik ingress controller**, simplifying ingress management.

