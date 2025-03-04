## Creating an EC2 Instance in AWS and Installing Docker

To begin, log in to AWS Console.

### Task-1:  Launching EC2 instances and Connecting to EC2 Instances using SSH

* Manually Launch a `t2.micro` instance with OS version as `Ubuntu 24.04 LTS` 
* Enable `SSH`, `HTTP`, `HTTPS` and `edit`.
* Type : `Custom TCP`     Source Type: `Anywhere`    Port Range : `8080-8090`
* Create a new key pair Name:`yourname_kp` Format:`.pem`
* Configure Storage: `10 GiB`
* Once Launched, Connect to the Instance using CloudShell.

### Steps to Connect via CloudShell
* Upload Your SSH Key to CloudShell
  * In CloudShell, click on "Actions" → "Upload file".
  * Select your private key file (.pem) from your computer.
  * Run the following command to move and set proper permissions:
  ```
  mkdir -p ~/.ssh
  ```
  
  ```
  mv <your-key-file>.pem ~/.ssh/
  ```
  
  ```
  chmod 400 ~/.ssh/<your-key-file>.pem
  ```
* Connect to the EC2 Instance
```
ssh -i ~/.ssh/<your-key-file>.pem ubuntu@<EC2_PUBLIC_IP>
```


### Task-2: Installing Docker on Ubuntu 18.04 operating system 
```
sudo hostnamectl set-hostname docker
```
Refresh the Shell 
```
bash
```
Switch to Root user
```
sudo su
```
```
apt update -y
```
```
apt install curl -y
```
Download and install Docker via Script
```
curl -SSL https://get.docker.com/ | sh
```
Check the status of docker daemon
```
service docker status   # Or systemctl status docker
```
If the service is not active, then we need to start the service
```
service docker start    # Or systemctl start docker
```
To add ubuntu user to docker group, if you are not working as the root user
```
sudo usermod -aG docker ubuntu
```
Note : **Reconnect after modifications**

Verify Docker Installation
```
docker --version
```
### Docker Commands
```
docker run hello-world
```
```
docker images
```
```
docker ps
```
```
docker ps -a
```
```
docker run --help
```
```
docker pull ubuntu
```
```
docker run -it ubuntu bash
```
```
docker run -d nginx
```
