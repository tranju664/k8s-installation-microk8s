# KUBERNETES INSTALLATION STEPS

## STEP 1: MASTER NODE INSTALLATION

- Create EC2 Instance from UBUNTU AMI with type t2.medium (2 core CPU and 4GB Ram)
- Github URL: https://github.com/tranju664/k8s-installation-microk8s.git

### COMMANDS:
```
git clone https://github.com/tranju664/k8s-installation-microk8s.git
cd k8s-installation-microk8s
bash install-microk8s.sh

# Ensure MicroK8s is running
#microk8s status --wait-ready

# Create .kube directory if it doesn't exist
#mkdir -p ~/.kube

# Generate kubeconfig for MicroK8s
#sudo microk8s config > ~/.kube/config

# Set correct permissions
#sudo chown -R $(whoami) ~/.kube

# Verify configuration
#kubectl config view

#microk8s status
#microk8s start
#microk8s stop
```

## STEP 2: Worker NODE INSTALLATION

- Create EC2 Instance from UBUNTU AMI with type t2.micro (1 core CPU and 1GB Ram)
- Github URL: https://github.com/tranju664/k8s-installation-microk8s.git

### COMMANDS:
```
git clone https://github.com/tranju664/k8s-installation-microk8s.git
cd k8s-installation-microk8s
bash install-microk8s.sh

# Ensure MicroK8s is running
#microk8s status --wait-ready

# Create .kube directory if it doesn't exist
#mkdir -p ~/.kube

# Generate kubeconfig for MicroK8s
#sudo microk8s config > ~/.kube/config

# Set correct permissions
#sudo chown -R $(whoami) ~/.kube

# Verify configuration
#kubectl config view

```

## STEP 3: Login back to Master instance created in STEP 1

### Generate microk8s join command for worker node -1

```
microk8s add-node
```
>Note: Copy the command with --worker flag, we need to run this command on worker nodes

## STEP 4: Initialize this step for  WORKER NODE -1 [ssh to worker nodes created from STEP 2]

```
microk8s join <TOKEN> --worker [Command from STEP 3] --> To connect worker node to Master

```

### Generate microk8s join command for worker node -2 in Master instance to have token, because it would b expired

```
microk8s add-node
```
>Note: Copy the command with --worker flag, we need to run this command on worker nodes

## STEP 4: Initialize this step for  WORKER NODE -2 [ssh to worker nodes created from STEP 2]

```
microk8s join <TOKEN> --worker [Command from STEP 3] --> To connect worker node to Master
```
## STEP 5: Login back to Master instance created in STEP 1
```
mkctl get nodes   or kubectl get nodes
```
