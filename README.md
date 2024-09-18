![Screenshot (730)](https://github.com/user-attachments/assets/9277c96f-d3a9-4d31-8349-c45bc6c06d42)KOPS (KUBERNETES OPERATIONS)

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

                 
 

STEP-3: INSTALL KOPS & KUBECTL
KUBECTL SETUP
                   curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
PERMISSIONS: chmod +x kubectl
mv kubectl /usr/local/bin/
Check Version: kubectl  Version
             
KOPS  SETUP
                   curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops
Check version: kops version

           

STEP-4: CREATE IAM ROLE WITH ADMIN PERMISSIONS AND ATTACH IT TO OUR INSTANCE,
                

SELECT INSTANCE >>> ACTIONS >>> SECURITY >>>> MODIFY IAM ROLE

                  
STEP-5: CREATE INFRA SETUP
                   TO CREATE BUCKET: aws s3 mb s3://praveen.kopsbucket. k8s.local
                                                                                 ( bucket name)   

                      

                Enable Bucket Versioning                                       
                           

EXPORT CLUSTER DATA INTO BUCKET:
                            export KOPS_STATE_STORE=s3://praveen.kopsbucket.k8s.local
                                                                                         (bucket name) 
                                                        
 
CREATE CLUSTER 
       kops create cluster --name praveen.k8s.local --zones ap-south-1a --master-size t2.medium --node-size t2.micro --master-count 1 --node-count 2
 
             
                 Kops update cluster –name praveen.k8s.local –yes –admin  (Execute this command)

Creation of Cluster is completed
 



      


