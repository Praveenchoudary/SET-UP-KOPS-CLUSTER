
STEP-1: LAUNCH INSTANCE WITH T2.MICRO AND 20 GB SSD
        ![image](https://github.com/user-attachments/assets/81f58625-c28d-4f6a-a19c-735c7752b77c)
              
STEP-2: INSTALL AWS CLI
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
TO  CHECK VERSION: /usr/local/bin/aws --version
TO SET PATH: vim .bashrc
export PATH=$PATH:/usr/local/bi
source .bash
aws –version

![image](https://github.com/user-attachments/assets/aa2863d2-36f6-4050-a338-999c17f9efac)
![image](https://github.com/user-attachments/assets/75666d86-f8ec-43d4-872e-608a0d9d063c)

STEP-3: INSTALL KOPS & KUBECTL
KUBECTL SETUP
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"              chmod +x kubectl
mv kubectl /usr/local/bin/
kubectl  Version
![image](https://github.com/user-attachments/assets/c7e1aae8-3b28-4d2b-b5e6-6b4d2a4299aa)

KOPS  SETUP:

curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl shttps://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops
![image](https://github.com/user-attachments/assets/bb1cd67a-0773-4163-b9b2-bae248805d7d)
STEP-4: CREATE IAM ROLE WITH ADMIN PERMISSIONS AND ATTACH IT TO OUR INSTANCE:
![image](https://github.com/user-attachments/assets/0ab4a3e2-3cbf-4a32-a89f-6bff2b0c57f0)
SELECT INSTANCE >>> ACTIONS >>> SECURITY >>>> MODIFY IAM ROLE
![image](https://github.com/user-attachments/assets/581de945-3c18-4a56-939a-0f54578297e5)

STEP-5: CREATE INFRA SETUP
TO CREATE BUCKET: 
                  aws s3 mb s3://praveen.kopsbucket. k8s.local
                                   ( bucket name)   
![image](https://github.com/user-attachments/assets/9f7c574f-4c11-4d2c-bafc-c7fd2bbf2d25)
Enable Bucket Versioning:
![image](https://github.com/user-attachments/assets/24ff1361-89cd-4149-ad7d-d00498db2da9)

EXPORT CLUSTER DATA INTO BUCKET:
       export KOPS_STATE_STORE=s3://praveen.kopsbucket.k8s.local

       ![image](https://github.com/user-attachments/assets/bdeae941-4c5d-4809-b81e-d90849551fd5)
CREATE CLUSTER 
kops create cluster --name praveen.k8s.local --zones ap-south-1a --master-size t2.medium --node-size t2.micro --master-count 1 --node-count 2
![image](https://github.com/user-attachments/assets/de541025-9809-4241-a340-4675bc3e8ee3)
kops update cluster –name praveen.k8s.local –yes –admin  
![image](https://github.com/user-attachments/assets/f8650b18-f626-43c3-8ebe-03f4d20eb44d)
![image](https://github.com/user-attachments/assets/7faa5488-7103-404f-a95d-37772cb4ca8e)
