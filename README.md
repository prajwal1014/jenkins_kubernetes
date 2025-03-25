# Jenkins Pipeline with Kubernetes CLI Plugin

This guide explains how to deploy a Kubernetes YAML file from a GitHub repository using the Kubernetes CLI Plugin in Jenkins.

## Prerequisites
- **Jenkins Server**: Installed and running.
- **Kubernetes Cluster**: Consists of a Master and a Worker node.
- **Jenkins Kubernetes CLI Plugin**: Installed in Jenkins.
- **GitHub Repository**: Contains the YAML file (e.g., `ClusterIP.yml`).
- **Kubeconfig File**: Configured and stored in Jenkins credentials.

## Step 1: Install the Kubernetes CLI Plugin
1. Go to **Jenkins Dashboard** → **Manage Jenkins** → **Manage Plugins**.
2. In the **Available Plugins** tab, search for `Kubernetes CLI`.
3. Install the plugin and restart Jenkins.

## Step 2: Configure Kubernetes Credentials in Jenkins
1. Navigate to **Jenkins Dashboard** → **Manage Jenkins** → **Manage Credentials**.
2. Click **(global) -> Add Credentials**.
3. Select **Secret file** and upload your `kubeconfig` file.
4. Give it an **ID** (e.g., `k8s-kubeconfig`).
5. Save the credentials.

## Step 3: Create a Pipeline in Jenkins
1. Open **Jenkins Dashboard**.
2. Click **New Item** → Select **Pipeline**.
3. Name the pipeline (e.g., `k8s-deployment`) and click **OK**.
4. Scroll down to the **Pipeline** section and select **Pipeline script from SCM**.
5. Enter your **GitHub repository URL**.
6. Click **Save**.

## Step 4: Run the Pipeline in Jenkins
1. Go to **Jenkins Dashboard** → **Your Pipeline**.
2. Click **Build Now**.
3. Monitor the console output for success messages.

## Step 5: Verify Deployment in Kubernetes
Run these commands in the **Kubernetes Master Node**:
```sh
kubectl get pods
kubectl get deployments
kubectl get services
