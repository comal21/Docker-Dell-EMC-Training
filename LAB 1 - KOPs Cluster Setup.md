## Cluster Setup using Kops

### Task-1:  Launching EC2 instances and Connecting to EC2 Instances using SSH

* Manually Launch a `t2.micro` instance with OS version as `Ubuntu 22.04 LTS` in North Virginia (us-east-1) Region.
* Enable `SSH`, `HTTP`, `HTTPS` and `edit`.
* Configure Storage: `10 GiB`
* Once Launched, Connect to the Instance using `Cloudshell` or `EC2 Instance Connect` with username "`ubuntu`".

### Task 2: Create an IAM role

* Create an IAM role named "kops-admin-role" with the "AdministratorAccess" policy attached.
* Now, associate the IAM role "kops-admin-role" with your EC2 instance named "kops" by following these steps:
  ** Navigate to the EC2 console and select the "kops" instance.
  ** Click on "Action" > "Security" > "Modify IAM role."
  ** Search for the "kops-admin-role" role, select it, and click "Update IAM role."

### Task 3: Setting up a Kubernetes Cluster
Set the hostname to "kops"
```
sudo hostnamectl set-hostname kops
```
Open a new bash shell
```
bash
```
Create Kops script file
```
vi kops.sh
```
Add the below code in the script file
```bash
#!/bin/bash

echo "Let's get started with Kubernetes cluster creation using KOPS!"
echo "Enter your name:"
read username
lower_username=$(echo -e $username | sed 's/ //g' | tr '[:upper:]' '[:lower:]')
date_now=$(date "+%F-%H-%m")
clname=$(echo $lower_username-$date_now.k8s.local)
echo "Your Kubernetes cluster name will be $clname"

TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

az=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/placement/availability-zone)
region=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/placement/region)

sudo sed -i "/$nrconf{restart}/d" /etc/needrestart/needrestart.conf
echo "\$nrconf{restart} = 'a';" | sudo tee -a /etc/needrestart/needrestart.conf
export DEBIAN_FRONTEND=noninteractive
export NEEDRESTART_MODE=a

sudo apt update -y
sudo apt install nano curl python3-pip -y
sudo snap install aws-cli --classic

# Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# Install kops
curl -LO "https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64"
chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops

# Generate SSH key
ssh-keygen -t rsa -N "" -f $HOME/.ssh/id_rsa

# Create S3 bucket for kops state store
aws s3 mb s3://$clname --region $region

# Set KOPS_STATE_STORE environment variable
export KOPS_STATE_STORE=s3://$clname

# Create Kubernetes cluster
kops create cluster --node-count=2 --master-size="t2.medium" --node-size="t2.medium" --master-volume-size=20 --node-volume-size=20 --zones $az --name $clname --ssh-public-key ~/.ssh/id_rsa.pub --yes
kops update cluster $clname --yes

# Export KOPS_STATE_STORE to bashrc
echo "export KOPS_STATE_STORE=s3://$clname" >> /home/ubuntu/.bashrc
source /home/ubuntu/.bashrc

# Export kubectl configuration
kops export kubecfg --admin

# Validate cluster
for (( x=0 ; x < 30 ; x++ )); do
  echo "Validating Cluster"
  if kops validate cluster > status.txt 2>/dev/null && grep -q "is ready" status.txt; then
    echo "Your Cluster is now ready!"
    break
  else
    sleep 20
    echo "x: $x"
  fi
done


```
save the file using `ESCAPE + :wq!`

Execute the Kops script
```
. ./kops.sh
```
Retrieve information about the existing clusters
```
kops get cluster
```
Get information about the Kubernetes nodes in the cluster
```
kubectl get nodes
```
