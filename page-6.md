# Page 6

## Install Devtron OSS

### Introduction

| Installation Option               | What Is Included                                            | When To Use                                                                            |
| --------------------------------- | ----------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Minimal**                       | Dashboard + Resource Browser + Core operator configurations | A unified view of Helm apps, FluxCD apps, ArgoCD apps, and their related K8s resources |
| **With CI/CD**                    | Everything in Minimal + Build and Deploy (CI/CD) module     | You need a complete CI-CD pipeline for your custom apps (a.k.a Devtron Apps)           |
| **With CI/CD + GitOps (Argo CD)** | Everything in CI/CD + GitOps (Argo CD) module               | You need automated, Git-driven deployments                                             |

{% hint style="success" %}
#### Not Sure What To Choose?

Begin with the **Minimal** version. You can always install CI/CD and GitOps integrations later from Devtron Stack Manager.
{% endhint %}

***

### Prerequisites

* Kubernetes cluster v1.16 or later (cloud or local)
* [Helm v3.8+ installed](https://helm.sh/docs/intro/install/)
* For production, meet [Infrastructure Recommendations](https://docs.devtron.ai/prod-infra)

{% hint style="warning" %}
#### Cluster created on AWS? Is your EKS version 1.23 or above?

If you are using EKS version 1.23 or above on AWS, you must also install ['AWS EBS CSI' driver](https://docs.aws.amazon.com/eks/latest/userguide/ebs-csi.html) using the following command:

```bash
helm repo add aws-ebs-csi-driver \
https://kubernetes-sigs.github.io/aws-ebs-csi-driver \
helm repo update \
helm upgrade --install aws-ebs-csi-driver \
--namespace kube-system aws-ebs-csi-driver/aws-ebs-csi-driver
```
{% endhint %}

***

### Steps to Install Devtron OSS

#### Step 1: Add Devtron Helm Repository

```bash
helm repo add devtron https://helm.devtron.ai
helm repo update devtron
```

#### Step 2: Choose an Installation Option

{% tabs %}
{% tab title="Minimal" %}
**Command**

```bash
helm install devtron devtron/devtron-operator \
--create-namespace --namespace devtroncd
```
{% endtab %}

{% tab title="With CI/CD" %}
**Command**

```bash
helm install devtron devtron/devtron-operator \
--create-namespace --namespace devtroncd \
--set installer.modules={cicd}
```
{% endtab %}

{% tab title="With CI/CD + GitOps (Argo CD)" %}
**Command**

```bash
helm install devtron devtron/devtron-operator \
--create-namespace --namespace devtroncd \
--set installer.modules={cicd} \
--set argo-cd.enabled=true
```
{% endtab %}
{% endtabs %}

#### Step 3: Obtain the Dashboard URL

{% tabs %}
{% tab title="For EKS/AKS/GKE" %}
Run the following command to get the Dashboard URL:

```bash
kubectl get svc -n devtroncd devtron-service -o jsonpath='{.status.loadBalancer.ingress}'
```

> <mark style="color:green;">**The Dashboard URL will be the LoadBalancer URL displayed in the output of the above command.**</mark>
{% endtab %}

{% tab title="MicroK8s/Kind/K3s" %}
**Accessing the Dashboard locally (MicroK8s/Kind/K3s)**

To obtain the Dashboard URL when MicroK8s/Kind/K3s running locally, run the following command to port-forward the devtron service to port `8000`

```bash
kubectl -n devtroncd port-forward service/devtron-service 8000:80
```

> **The Dashboard URL will be `http://127.0.0.1:8000`**

**Accessing the Dashboard via NodePort**

To obtain the Dashboard URL on MicroK8s/Kind/K3s using NodePort, run the following command to retrieve the port number assigned to the service:

```bash
kubectl get svc -n devtroncd devtron-service -o jsonpath='{.spec.ports[0].nodePort}'
```

> **The Dashboard URL will be: `http://<HOST_IP>:<NODEPORT>/dashboard`**

**Accessing the Dashboard locally from a remote VM (Port Forwarding via Kubeconfig)**

To obtain the Dashboard URL if Devtron is installed on a remote VM (e.g., AWS EC2, Azure VM, GCP Compute Engine) using MicroK8s, Kind, or K3s, run the following commands:

```bash
scp user@cloud-vm-ip:/path/to/kubeconfig ~/.kube/config 
# Export the kubeconfig file from the remote VM to your local system.

kubectl config use-context <context-name>
# Set the correct context.

kubectl -n devtroncd port-forward service/devtron-service 8000:80
# This command will forward traffic from the service running on the 
# remote VM's MicroK8s, Kind, or K3s cluster to your local system’s port.
```

> **The Dashboard URL will be `http://127.0.0.1:8000` and accessible on your local machine.**
{% endtab %}

{% tab title="Minikube" %}
To access the dashboard on Minikube cluster, run the following command:

```bash
minikube service devtron-service --namespace devtroncd
```

**This will directly open the dashboard URL on your browser**
{% endtab %}

{% tab title="Cloud VMs" %}
**Accessing the Dashboard via NodePort**

To obtain the dashboard URL on Cloud VMs using NodePort, run the following command to retrieve the port number assigned to the service:

```bash
kubectl get svc -n devtroncd devtron-service -o jsonpath='{.spec.ports[0].nodePort}'
```

> **The Dashboard URL will be `http://<HOST_IP>:<NODEPORT>/dashboard`**

**Accessing the Dashboard locally from a remote VM (Port Forwarding via Kubeconfig)**

To obtain the Dashboard URL if Devtron is installed on a remote VM (e.g., AWS EC2, Azure VM, GCP Compute Engine) using MicroK8s, Kind, or K3s, run the following commands:

```bash
scp user@cloud-vm-ip:/path/to/kubeconfig ~/.kube/config 
# Export the kubeconfig file from the remote VM to your local system.

kubectl config use-context <context-name>
# Set the correct context.

kubectl -n devtroncd port-forward service/devtron-service 8000:80
# This command will forward traffic from the service running on the 
# remote VM's MicroK8s, Kind, or K3s cluster to your local system’s port.
```

> **The Dashboard URL will be `http://127.0.0.1:8000` accessible from your local machine.**
{% endtab %}
{% endtabs %}

#### Step 4: Log in to Devtron

1. Open the dashboard URL (obtained in the previous step) in your browser. You will be greeted with a login page.
2. Initially, log in with the administrator credentials. By default, the username is **admin**.
3. Run the following command to get the admin password:

```bash
kubectl -n devtroncd get secret devtron-secret \
-o jsonpath='{.data.ADMIN_PASSWORD}' | base64 -d
```

4. You should see the **Devtron Dashboard** post successful login.

{% hint style="info" %}
#### Note

When you install Devtron for the first time, it creates a default admin user and password (with unrestricted access to Devtron). You can use it anytime to log in as an administrator.

However, after the initial login, we recommend you set up an Single Sign-On (SSO) service like Google, GitHub, etc., and then add other members (including yourself). Thereafter, all the users can log in using your configured SSO.
{% endhint %}
