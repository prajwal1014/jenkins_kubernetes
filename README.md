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

## Step 2: Configure Kubernetes Credentials (`admin.conf`) in Jenkins  
To allow Jenkins to authenticate with Kubernetes, we need to store the `admin.conf` file as a **Secret File** in Jenkins credentials.

### **Step 2.1: Locate the `admin.conf` File**  
On the **Kubernetes Master Node**, the default kubeconfig file (`admin.conf`) is located at:  
```sh
sudo cat /etc/kubernetes/admin.conf
```
Copy the entire contents of this file(as admin.conf/admin.txt in your pc).

### **Step 2.2: Add `admin.conf` as a Secret File in Jenkins**  
1. Open **Jenkins Dashboard**.  
2. Go to **Manage Jenkins** → **Manage Credentials**.  
3. Click **(global) → Add Credentials**.  
4. Set the following:  
   - **Kind**: Select **Secret file**.  
   - **File**: Upload the copied `admin.conf` contents as a file(admin.conf/admin.txt).  
   - **ID**: Enter a recognizable name (e.g., `k8s-kubeconfig`).  
   - **Description**: (Optional) Add a note like `"Kubernetes admin.conf for authentication"`.  
5. Click **OK** to save the credentials.

This will allow Jenkins to use `admin.conf` when executing `kubectl` commands.


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
```
![image](https://github.com/user-attachments/assets/438dd4bb-d6a4-497b-ab06-d3963e411a40)
![image](https://github.com/user-attachments/assets/6142b296-9437-44ca-9479-0c57660cdf2f)
