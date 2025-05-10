# Rearchitecting-Web-App-on-AWS-Cloud-PAAS-SAAS


## 1. Create Security Group and Key Pair

- Create inbound rule for all traffic from SG of that created SG because of internal traffic only

![alt text](image.png)

![alt text](image-1.png)

## 2. Create RDS

#### 2.1 Create Parameter Group

![alt text](image-2.png)


#### 2.2 Create Subnet Group

- Use private subnet

#### 2.3 Create Database

![alt text](image-3.png)

![alt text](image-4.png)

- Add DB instance identifier

- Use micro type

- Use created resources for VPC,DB Subnet Group, Security Group

- Choose 'No' for public access

- Set initial database

![alt text](image-5.png)

- Create Database


## 3. Create Elastic Cache

#### 3.1 Create Parameter Group

![alt text](image-6.png)


#### 3.2 Create Subnet Group

- Use private subnet

![alt text](image-7.png)


#### 3.2 Create Elastic Cache

![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)



## 4. Create ActiveMQ brokers

![alt text](image-11.png)


![alt text](image-12.png)

![alt text](image-13.png)

![alt text](image-14.png)

![alt text](image-15.png)


## 5. Create EC2

![alt text](image-16.png)

#### 5.1 Clone DB Schema from Github

```
sudo - i
apt update && apt install mysql-client git -y
```



#### 5.2 Update Security Group of Backend

- Add 3306 port from SG of EC2 to SG of backend

![alt text](image-17.png)


#### 5.3 Log in Mysql Client

```
mysql -h tkk-vprofile-rds-rearch.cbimh6vjs3bt.ap-southeast-1.rds.amazonaws.com -u admin -p accounts
exit
```

```
git clone https://github.com/hkhcoder/vprofile-project.git
cd vprofile-project/
git checkout awsrefactor
ls src/main/resources/
```

![alt text](image-18.png)


```
mysql -h tkk-vprofile-rds-rearch.cbimh6vjs3bt.ap-southeast-1.rds.amazonaws.com -u admin -p accounts < src/main/resources/db_backup.sql
mysql -h tkk-vprofile-rds-rearch.cbimh6vjs3bt.ap-southeast-1.rds.amazonaws.com -u admin -p accounts
show tables;
exit
```

![alt text](image-19.png)

#### 5.4 Delete EC2 and Delete Security Group

![alt text](image-20.png)


## 6. Create IAM Roles

#### 6.1 Create IAM Role with the following roles

![alt text](image-21.png)

#### 6.2 Create Elastic Beanstalk

![alt text](image-22.png)

![alt text](image-23.png)

![alt text](image-24.png)

![alt text](image-25.png)

![alt text](image-26.png)

- Choose Virtual Private Cloud (VPC)

![alt text](image-27.png)

![alt text](image-28.png)

- Leave SG because it will create new one

![alt text](image-29.png)

![alt text](image-30.png)

![alt text](image-31.png)

![alt text](image-32.png)

- Enable Stickiness

![alt text](image-33.png)

![alt text](image-34.png)

- Click Next and Submit

## 7. Update Security Group and ELB

- Add Eleastic Beanstalk Security Group to Backend SG

![alt text](image-35.png)

## 8. Build and Deploy Artifacts

#### 8.1 Git Clone to Your Local

```
git clone https://github.com/hkhcoder/vprofile-project.git
cd vprofile-project
```

#### 8.2 Update application properties by using information of resources

![alt text](image-36.png)

#### 8.3 Install mvn a

```
wget https://downloads.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
sudo tar -xzf apache-maven-3.9.9-bin.tar.gz -C /opt
sudo ln -sfn /opt/apache-maven-3.9.9 /opt/maven
source /etc/profile.d/maven.sh 2>/dev/null || source ~/.bashrc
export M2_HOME=/opt/maven
export PATH=$M2_HOME/bin:$PATH
mvn -v
mvn -install
```

#### 8.4 Upload Artifacts

![alt text](image-37.png)


![alt text](image-38.png)

![alt text](image-39.png)

- check elasticbeanstolk

![alt text](image-40.png)

#### 8.5 Add HTTPS Target Group and Certificate for Security


![alt text](image-41.png)

- click apply

![alt text](image-42.png)


#### 9. Add Cloudfront

![alt text](image-43.png)

![alt text](image-44.png)

![alt text](image-45.png)

![alt text](image-46.png)

![alt text](image-47.png)


------
**_That's it!.You have finished How To Configure AWS Cloud for Project Set Up Lift and Shift.Special Thanks to Sir Imran Teli_**
-----
